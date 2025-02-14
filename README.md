<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Gerenciamento de Presença</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/css/bootstrap.min.css" rel="stylesheet">
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/js/bootstrap.bundle.min.js"></script>

    <style>
        /* Fundo com gradiente suave */
        body {
            background: linear-gradient(135deg, #6a11cb, #2575fc);
            color: white;
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
            font-family: 'Arial', sans-serif;
            background-size: cover;
            margin: 0;
        }

        /* Estilização do container da tela de login */
        #auth-container {
    background: rgba(255, 255, 255, 0.95);
    padding: 40px;
    border-radius: 12px;
    box-shadow: 0px 10px 30px rgba(0, 0, 0, 0.3);
    max-width: 400px;
    width: 100%;
    text-align: center;
    animation: fadeIn 0.5s ease-in-out;
    color: black;
    position: absolute; /* Alinha o container em relação à página */
    top: 50%; /* Move o container para o meio da tela */
    left: 50%; /* Move o container para o meio da tela */
    transform: translate(-50%, -50%); /* Ajusta o container para ficar centralizado */
}


        /* Botões de login e cadastro */
        .auth-buttons {
            display: flex;
            justify-content: space-between;
            margin-bottom: 15px;
        }

        .auth-buttons .btn {
            flex: 1;
            margin: 0 5px;
            padding: 12px;
            font-size: 16px;
            font-weight: bold;
            transition: all 0.3s ease-in-out;
        }

        .auth-buttons .btn:hover {
            transform: scale(1.05);
            opacity: 0.9;
        }

        /* Estilização dos campos de input */
        .form-control {
            border-radius: 8px;
            padding: 12px;
            font-size: 16px;
            transition: all 0.3s ease-in-out;
            border: 2px solid transparent;
        }

        .form-control:focus {
            border-color: #6a11cb;
            box-shadow: 0 0 8px rgba(106, 17, 203, 0.5);
        }

        /* Botão de login e cadastro */
        .btn-success,
        .btn-info {
            padding: 12px;
            font-size: 18px;
            font-weight: bold;
            transition: all 0.3s ease-in-out;
            border-radius: 8px;
        }

        .btn-success:hover,
        .btn-info:hover {
            transform: scale(1.05);
            opacity: 0.9;
        }

        /* Efeito de fade-in para animação */
        @keyframes fadeIn {
            from {
                opacity: 0;
                transform: translateY(-20px);
            }

            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        /* Ocultar formulários inicialmente */
        .hidden {
            display: none;
        }

        /* Estilo do conteúdo da página de administração */
        .container-admin {
            background: rgba(255, 255, 255, 0.95);
            border-radius: 15px;
            padding: 30px;
            box-shadow: 0 8px 25px rgba(0, 0, 0, 0.3);
            color: black;
            max-width: 1200px;
            width: 100%;
        }

        /* Estilos para o calendário */
        .calendar {
            display: grid;
            grid-template-columns: repeat(5, 1fr);
            gap: 20px;
            text-align: center;
            margin-top: 20px;
        }

        .calendar-header {
            background: #6a11cb;
            color: white;
            padding: 12px;
            border-radius: 8px;
            font-size: 16px;
        }

        .calendar-cell {
            background: #fff;
            padding: 20px;
            border-radius: 10px;
            min-height: 150px;
            box-shadow: 0 6px 15px rgba(0, 0, 0, 0.2);
            display: flex;
            flex-direction: column;
            justify-content: space-between;
        }

        /* Linha divisória entre manhã e tarde */
        .divider {
            border-top: 2px solid #6a11cb;
            margin: 10px 0;
        }

        .periodo {
            font-weight: bold;
            margin-bottom: 10px;
        }

        .aluno-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 10px;
            border-bottom: 1px solid #ddd;
            margin-bottom: 10px;
        }

        .btn-sm {
            margin-left: 5px;
            border-radius: 50%;
            width: 30px;
            height: 30px;
            padding: 0;
        }
    </style>
</head>

<body>
    <!-- Tela de Login/Cadastro -->
    <div id="auth-container">
        <h2 class="text-center">Acesso</h2>
        <div class="auth-buttons">
            <button class="btn btn-primary" onclick="toggleForm('login')">Login</button>
            <button class="btn btn-secondary" onclick="toggleForm('signup')">Cadastro</button>
        </div>

        <!-- Formulário de Login -->
        <div id="login-form">
            <input type="text" id="login-nome" class="form-control mb-2" placeholder="Nome">
            <input type="password" id="login-senha" class="form-control mb-3" placeholder="Senha">
            <button class="btn btn-success w-100" onclick="login()">Entrar</button>
        </div>

        <!-- Formulário de Cadastro -->
        <div id="signup-form" class="hidden">
            <input type="text" id="signup-nome" class="form-control mb-2" placeholder="Nome Completo">
            <input type="password" id="signup-senha" class="form-control mb-3" placeholder="Senha">
            <button class="btn btn-info w-100" onclick="signup()">Cadastrar</button>
        </div>
    </div>

    <!-- Tela do Administrador -->
    <div class="container-admin hidden" id="admin">
        <h2 class="text-center">Gerenciar Alunos</h2>
        <input type="text" id="nomeAluno" class="form-control my-2" placeholder="Nome do Aluno">
        <select id="diaSemana" class="form-select my-2">
            <option value="">Dia da Semana</option>
            <option value="segunda">Segunda</option>
            <option value="terca">Terça</option>
            <option value="quarta">Quarta</option>
            <option value="quinta">Quinta</option>
            <option value="sexta">Sexta</option>
        </select>
        
        <!-- Separação para Períodos -->
        <div class="periodo-separador">
            <span>Selecione o Período</span>
        </div>
        
        <select id="periodo" class="form-select my-2">
            <option value="">Período</option>
            <option value="manha">Manhã</option>
            <option value="tarde">Tarde</option>
        </select>

        <button class="btn btn-primary w-100" onclick="adicionarAluno()">Adicionar Aluno</button>

        <h3 class="text-center mt-4">Calendário</h3>
        <div class="calendar">
            <div class="calendar-header">Segunda</div>
            <div class="calendar-header">Terça</div>
            <div class="calendar-header">Quarta</div>
            <div class="calendar-header">Quinta</div>
            <div class="calendar-header">Sexta</div>

            <div id="cell-segunda" class="calendar-cell">
                <div class="periodo">Manhã</div>
                <div id="manha-segunda" class="alunos-periodo"></div>
                <div class="divider"></div>
                <div class="periodo">Tarde</div>
                <div id="tarde-segunda" class="alunos-periodo"></div>
            </div>
            <div id="cell-terca" class="calendar-cell">
                <div class="periodo">Manhã</div>
                <div id="manha-terca" class="alunos-periodo"></div>
                <div class="divider"></div>
                <div class="periodo">Tarde</div>
                <div id="tarde-terca" class="alunos-periodo"></div>
            </div>
            <div id="cell-quarta" class="calendar-cell">
                <div class="periodo">Manhã</div>
                <div id="manha-quarta" class="alunos-periodo"></div>
                <div class="divider"></div>
                <div class="periodo">Tarde</div>
                <div id="tarde-quarta" class="alunos-periodo"></div>
            </div>
            <div id="cell-quinta" class="calendar-cell">
                <div class="periodo">Manhã</div>
                <div id="manha-quinta" class="alunos-periodo"></div>
                <div class="divider"></div>
                <div class="periodo">Tarde</div>
                <div id="tarde-quinta" class="alunos-periodo"></div>
            </div>
            <div id="cell-sexta" class="calendar-cell">
                <div class="periodo">Manhã</div>
                <div id="manha-sexta" class="alunos-periodo"></div>
                <div class="divider"></div>
                <div class="periodo">Tarde</div>
                <div id="tarde-sexta" class="alunos-periodo"></div>
            </div>
        </div>

        <button class="btn btn-danger w-100 mt-3" onclick="logout()">Sair</button>
    </div>

    <!-- Modal de Histórico -->
    <div class="modal fade" id="historicoModal" tabindex="-1" aria-labelledby="historicoModalLabel" aria-hidden="true">
        <div class="modal-dialog">
            <div class="modal-content">
                <div class="modal-header">
                    <h5 class="modal-title" id="historicoModalLabel">Histórico de Presença e Falta</h5>
                    <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                </div>
                <div class="modal-body">
                    <p id="historicoNome">Nome do Aluno: </p>
                    <p id="historicoPresencas">Presenças: 0</p>
                    <p id="historicoFaltas">Faltas: 0</p>
                </div>
                <div class="modal-footer">
                    <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Fechar</button>
                </div>
            </div>
        </div>
    </div>

    <script>
        let presencas = 0;
        let faltas = 0;
        let alunoNome = '';

        function toggleForm(formType) {
            if (formType === 'login') {
                document.getElementById('login-form').classList.remove('hidden');
                document.getElementById('signup-form').classList.add('hidden');
            } else {
                document.getElementById('signup-form').classList.remove('hidden');
                document.getElementById('login-form').classList.add('hidden');
            }
        }

        function login() {
            alert("Login realizado com sucesso!");
            document.getElementById('auth-container').classList.add('hidden');
            document.getElementById('admin').classList.remove('hidden');
        }

        function signup() {
            alert("Cadastro realizado com sucesso!");
            document.getElementById('auth-container').classList.add('hidden');
            document.getElementById('admin').classList.remove('hidden');
        }

        function adicionarAluno() {
            const nomeAluno = document.getElementById('nomeAluno').value.trim();
            const diaSemana = document.getElementById('diaSemana').value;
            const periodo = document.getElementById('periodo').value;

            if (!nomeAluno || !diaSemana || !periodo) {
                alert("Preencha todos os campos.");
                return;
            }

            alunoNome = nomeAluno;
            const periodoDiv = document.getElementById(`${periodo}-${diaSemana}`);
            const alunoItem = document.createElement('div');
            alunoItem.classList.add('aluno-item');

            const nomeSpan = document.createElement('span');
            nomeSpan.textContent = nomeAluno;

            const btnPresente = document.createElement('button');
            btnPresente.textContent = "✔️";
            btnPresente.classList.add("btn", "btn-success", "btn-sm");
            btnPresente.onclick = () => {
                presencas++;
                atualizarHistorico();
            };

            const btnFalta = document.createElement('button');
            btnFalta.textContent = "❌";
            btnFalta.classList.add("btn", "btn-danger", "btn-sm");
            btnFalta.onclick = () => {
                faltas++;
                atualizarHistorico();
            };

            const btnHistorico = document.createElement('button');
            btnHistorico.textContent = "📊 ";
            btnHistorico.classList.add("btn", "btn-info", "btn-sm");
            btnHistorico.onclick = () => {
                document.getElementById('historicoNome').textContent = `Nome do Aluno: ${nomeAluno}`;
                document.getElementById('historicoPresencas').textContent = `Presenças: ${presencas}`;
                document.getElementById('historicoFaltas').textContent = `Faltas: ${faltas}`;
                new bootstrap.Modal(document.getElementById('historicoModal')).show();
            };

            alunoItem.append(nomeSpan, btnPresente, btnFalta, btnHistorico);
            periodoDiv.appendChild(alunoItem);

            document.getElementById('nomeAluno').value = '';
        }

        function atualizarHistorico() {
            document.getElementById('historicoPresencas').textContent = `Presenças: ${presencas}`;
            document.getElementById('historicoFaltas').textContent = `Faltas: ${faltas}`;
        }

        function logout() {
            document.getElementById('auth-container').classList.remove('hidden');
            document.getElementById('admin').classList.add('hidden');
        }
    </script>
</body>
