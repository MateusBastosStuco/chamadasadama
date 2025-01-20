    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Gerenciamento de Presença</title>
    <!-- Bootstrap -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/css/bootstrap.min.css" rel="stylesheet">
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/js/bootstrap.bundle.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.4.0/jspdf.umd.min.js"></script>
    <style>
        body {
            background: linear-gradient(135deg, #6a11cb, #2575fc);
            color: white;
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
        }
        .container {
            background: rgba(255, 255, 255, 0.9);
            border-radius: 15px;
            padding: 30px;
            box-shadow: 0 6px 20px rgba(0, 0, 0, 0.3);
            max-width: 800px;
        }
        h1, h2 {
            color: #000000;
        }
        .list-group-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
    </style>
</head>
<body>
    <div class="container">
        <!-- Área de autenticação -->
        <div id="auth">
            <h1 class="text-center">Gerenciamento de Presença</h1>
            <div class="d-flex justify-content-center my-3">
                <button class="btn btn-primary me-2" onclick="toggleForm('login')">Login</button>
                <button class="btn btn-secondary" onclick="toggleForm('signup')">Cadastro</button>
            </div>
            <div id="loginForm" class="mt-3">
                <input type="text" id="loginNome" class="form-control mb-3" placeholder="Nome">
                <input type="password" id="loginPassword" class="form-control mb-3" placeholder="Senha">
                <button class="btn btn-success w-100" onclick="login()">Entrar</button>
            </div>
            <div id="signupForm" class="d-none mt-3">
                <input type="text" id="signupNome" class="form-control mb-3" placeholder="Nome Completo">
                <input type="password" id="signupPassword" class="form-control mb-3" placeholder="Senha">
                <button class="btn btn-info w-100" onclick="signup()">Cadastrar</button>
            </div>
        </div>

        <!-- Área de gerenciamento -->
        <div id="admin" class="d-none">
            <h2 class="text-center">Gerenciar Alunos</h2>
            <input type="text" id="nomeAluno" class="form-control my-2" placeholder="Nome do Aluno">
            <select id="diaSemana" class="form-select my-2">
                <option value="">Dia da Semana</option>
                <option value="Segunda">Segunda</option>
                <option value="Terça">Terça</option>
                <option value="Quarta">Quarta</option>
                <option value="Quinta">Quinta</option>
                <option value="Sexta">Sexta</option>
            </select>
            <select id="periodo" class="form-select my-2">
                <option value="">Período</option>
                <option value="manhã">Manhã</option>
                <option value="tarde">Tarde</option>
            </select>
            <button class="btn btn-primary w-100" onclick="adicionarAluno()">Adicionar Aluno</button>
            <div id="calendario" class="mt-4"></div>
            <button class="btn btn-danger w-100 mt-3" onclick="logout()">Sair</button>
        </div>
    </div>

    <!-- Modal para Histórico -->
    <div class="modal fade" id="historyModal" tabindex="-1" aria-labelledby="historyModalLabel" aria-hidden="true">
        <div class="modal-dialog">
            <div class="modal-content">
                <div class="modal-header">
                    <h5 class="modal-title" id="historyModalLabel">Histórico de Presença</h5>
                    <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                </div>
                <div class="modal-body">
                    <ul id="historyList" class="list-group"></ul>
                </div>
                <div class="modal-footer">
                    <button class="btn btn-success" onclick="exportarCSV()">Exportar CSV</button>
                    <button class="btn btn-danger" onclick="exportarPDF()">Exportar PDF</button>
                </div>
            </div>
        </div>
    </div>

    <script>
        const usuarios = JSON.parse(localStorage.getItem("usuarios") || "[]");
        const turmas = JSON.parse(localStorage.getItem("turmas") || "{}");

        function toggleForm(form) {
            document.getElementById('loginForm').classList.toggle('d-none', form !== 'login');
            document.getElementById('signupForm').classList.toggle('d-none', form !== 'signup');
        }

        function login() {
            const nome = document.getElementById('loginNome').value.trim();
            const senha = document.getElementById('loginPassword').value.trim();

            const usuario = usuarios.find(u => u.nome === nome && u.senha === senha);

            if (usuario) {
                document.getElementById('auth').classList.add('d-none');
                document.getElementById('admin').classList.remove('d-none');
                atualizarCalendario();
            } else {
                alert("Usuário ou senha inválidos!");
            }
        }

        function signup() {
            const nome = document.getElementById('signupNome').value.trim();
            const senha = document.getElementById('signupPassword').value.trim();

            if (!nome || !senha) {
                alert("Preencha todos os campos.");
                return;
            }

            if (usuarios.some(u => u.nome === nome)) {
                alert("Usuário já cadastrado. Escolha outro nome.");
                return;
            }

            usuarios.push({ nome, senha });
            localStorage.setItem("usuarios", JSON.stringify(usuarios));
            alert("Cadastro realizado com sucesso!");
            toggleForm('login');
        }

        function logout() {
            document.getElementById('admin').classList.add('d-none');
            document.getElementById('auth').classList.remove('d-none');
        }

        function adicionarAluno() {
            const nomeAluno = document.getElementById('nomeAluno').value.trim();
            const diaSemana = document.getElementById('diaSemana').value;
            const periodo = document.getElementById('periodo').value;

            if (!nomeAluno || !diaSemana || !periodo) {
                alert("Preencha todos os campos.");
                return;
            }

            if (!turmas[diaSemana]) turmas[diaSemana] = { manhã: [], tarde: [] };

            if (!turmas[diaSemana][periodo].some(a => a.nome === nomeAluno)) {
                turmas[diaSemana][periodo].push({ nome: nomeAluno, historico: [] });
                localStorage.setItem("turmas", JSON.stringify(turmas));
                atualizarCalendario();
            } else {
                alert("Aluno já registrado nesse dia e período.");
            }
        }

        function atualizarCalendario() {
            const calendarioDiv = document.getElementById('calendario');
            calendarioDiv.innerHTML = '';

            for (const dia in turmas) {
                const diaDiv = document.createElement('div');
                diaDiv.innerHTML = `<h4>${dia}</h4>`;

                ['manhã', 'tarde'].forEach(periodo => {
                    if (turmas[dia][periodo].length > 0) {
                        const periodoDiv = document.createElement('div');
                        periodoDiv.innerHTML = `<h5>${periodo}</h5>`;
                        const ul = document.createElement('ul');
                        ul.className = 'list-group';

                        turmas[dia][periodo].forEach((aluno, index) => {
                            const li = document.createElement('li');
                            li.className = 'list-group-item';
                            li.innerHTML = `
                                ${aluno.nome}
                                <div>
                                    <button class="btn btn-success btn-sm" onclick="marcarPresenca('${dia}', '${periodo}', '${aluno.nome}', true)">Presença</button>
                                    <button class="btn btn-danger btn-sm" onclick="marcarPresenca('${dia}', '${periodo}', '${aluno.nome}', false)">Falta</button>
                                    <button class="btn btn-info btn-sm" onclick="visualizarHistorico('${dia}', '${periodo}', '${aluno.nome}')">Histórico</button>
                                    <button class="btn btn-warning btn-sm" onclick="excluirAluno('${dia}', '${periodo}', ${index})">Excluir</button>
                                </div>
                            `;
                            ul.appendChild(li);
                        });

                        periodoDiv.appendChild(ul);
                        diaDiv.appendChild(periodoDiv);
                    }
                });

                calendarioDiv.appendChild(diaDiv);
            }
        }

        function excluirAluno(dia, periodo, index) {
            turmas[dia][periodo].splice(index, 1);
            localStorage.setItem("turmas", JSON.stringify(turmas));
            atualizarCalendario();
        }

        function marcarPresenca(dia, periodo, nomeAluno, presente) {
            const aluno = turmas[dia][periodo].find(a => a.nome === nomeAluno);
            aluno.historico.push({ data: new Date().toLocaleDateString(), presente });
            localStorage.setItem("turmas", JSON.stringify(turmas));
            atualizarCalendario();
        }

        function visualizarHistorico(dia, periodo, nomeAluno) {
            const aluno = turmas[dia][periodo].find(a => a.nome === nomeAluno);
            const historyList = document.getElementById('historyList');
            historyList.innerHTML = '';

            aluno.historico.forEach(entry => {
                const item = document.createElement('li');
                item.className = 'list-group-item';
                item.textContent = `${entry.data} - ${entry.presente ? "Presente" : "Faltou"}`;
                historyList.appendChild(item);
            });

            const modal = new bootstrap.Modal(document.getElementById('historyModal'));
            modal.show();
        }

        function exportarCSV() {
            const historyList = document.getElementById('historyList');
            let csvContent = "Data,Presença\n";

            for (const item of historyList.children) {
                csvContent += item.textContent.replace(' - ', ',') + "\n";
            }

            const blob = new Blob([csvContent], { type: 'text/csv;charset=utf-8;' });
            const url = URL.createObjectURL(blob);

            const link = document.createElement("a");
            link.setAttribute("href", url);
            link.setAttribute("download", "historico_presenca.csv");
            link.style.visibility = 'hidden';
            document.body.appendChild(link);
            link.click();
            document.body.removeChild(link);
        }

        async function exportarPDF() {
            const { jsPDF } = window.jspdf;
            const doc = new jsPDF();

            const title = "Histórico de Presença";
            const historyList = document.getElementById('historyList');

            doc.setFontSize(18);
            doc.text(title, 10, 10);

            let yPosition = 20; // Margem inicial
            doc.setFontSize(12);

            for (const item of historyList.children) {
                doc.text(item.textContent, 10, yPosition);
                yPosition += 10; // Espaço entre linhas
            }

            doc.save("historico_presenca.pdf");
        }
    </script>
</body>
</html>
