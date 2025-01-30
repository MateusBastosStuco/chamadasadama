<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <style>
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
        }

        .container {
            background: rgba(255, 255, 255, 0.95);
            border-radius: 15px;
            padding: 30px;
            box-shadow: 0 8px 25px rgba(0, 0, 0, 0.3);
            max-width: 900px;
            width: 100%;
            color: black;
        }

        .btn-primary, .btn-info, .btn-success, .btn-danger, .btn-warning {
            border-radius: 8px;
            font-weight: bold;
            transition: all 0.3s ease-in-out;
        }

        .btn-primary:hover, .btn-info:hover, .btn-success:hover, .btn-danger:hover, .btn-warning:hover {
            opacity: 0.85;
            transform: scale(1.05);
        }

        .calendar-header {
            font-weight: bold;
            background: #6a11cb;
            color: white;
            padding: 12px;
            border-radius: 8px;
            font-size: 16px;
            transition: background-color 0.3s ease;
        }

        .calendar {
            display: grid;
            grid-template-columns: repeat(5, 1fr);
            gap: 20px;
            text-align: center;
            margin-top: 20px;
        }

        .calendar-cell {
            background: #fff;
            padding: 20px;
            border-radius: 10px;
            min-height: 150px;
            box-shadow: 0 6px 15px rgba(0, 0, 0, 0.2);
            transition: all 0.3s ease;
        }

        .calendar-cell:hover {
            transform: scale(1.05);
            box-shadow: 0 10px 20px rgba(0, 0, 0, 0.3);
        }

        .aluno-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 10px;
            border-bottom: 1px solid #ddd;
            margin-bottom: 10px;
            transition: all 0.3s ease;
        }

        .aluno-item:hover {
            background: #f1f1f1;
            transform: scale(1.02);
        }

        .periodo-separador {
            border-top: 2px solid #ddd;
            margin: 20px 0;
            padding: 10px;
            text-align: center;
            color: #666;
        }

        .form-control, .form-select {
            border-radius: 10px;
            transition: border-color 0.3s ease;
        }

        .form-control:focus, .form-select:focus {
            border-color: #6a11cb;
            box-shadow: 0 0 5px rgba(106, 17, 203, 0.5);
        }

        .btn-sm {
            margin-left: 5px;
            border-radius: 50%;
            width: 30px;
            height: 30px;
            padding: 0;
        }

        .historico-modal .modal-body p {
            margin: 5px 0;
            font-size: 16px;
        }

    </style>
</head>
<body>

    <!-- Tela de Login/Cadastro -->
    <div class="container" id="auth">
        <h2 class="text-center">Acesso</h2>
        <div class="auth-button-container mb-3">
            <button class="btn btn-primary" onclick="toggleForm('login')">Login</button>
            <button class="btn btn-secondary" onclick="toggleForm('signup')">Cadastro</button>
        </div>

        <div id="loginForm">
            <input type="text" id="loginNome" class="form-control mb-2" placeholder="Nome">
            <input type="password" id="loginSenha" class="form-control mb-3" placeholder="Senha">
            <button class="btn btn-success w-100" onclick="login()">Entrar</button>
        </div>

        <div id="signupForm" class="d-none">
            <input type="text" id="signupNome" class="form-control mb-2" placeholder="Nome Completo">
            <input type="password" id="signupSenha" class="form-control mb-3" placeholder="Senha">
            <button class="btn btn-info w-100" onclick="signup()">Cadastrar</button>
        </div>
    </div>

    <!-- Tela do Administrador -->
    <div class="container d-none" id="admin">
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

            <div id="cell-segunda" class="calendar-cell"></div>
            <div id="cell-terca" class="calendar-cell"></div>
            <div id="cell-quarta" class="calendar-cell"></div>
            <div id="cell-quinta" class="calendar-cell"></div>
            <div id="cell-sexta" class="calendar-cell"></div>
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
            document.getElementById('loginForm').classList.toggle('d-none', formType !== 'login');
            document.getElementById('signupForm').classList.toggle('d-none', formType !== 'signup');
        }

        function login() {
            alert("Login realizado com sucesso!");
            document.getElementById('auth').classList.add('d-none');
            document.getElementById('admin').classList.remove('d-none');
        }

        function signup() {
            alert("Cadastro realizado com sucesso!");
            document.getElementById('auth').classList.add('d-none');
            document.getElementById('admin').classList.remove('d-none');
        }

        function adicionarAluno() {
            const nomeAluno = document.getElementById('nomeAluno').value.trim();
            const diaSemana = document.getElementById('diaSemana').value;
            const periodo = document.getElementById('periodo').value;

            if (!nomeAluno || !diaSemana || !periodo) {
                alert("Preencha todos os campos.");
                return;
            }

            alunoNome = nomeAluno;  // Armazena o nome do aluno

            const cell = document.getElementById(`cell-${diaSemana}`);
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
                document.getElementById('historicoNome').textContent = `Nome do Aluno: ${alunoNome}`;
                document.getElementById('historicoPresencas').textContent = `Presenças: ${presencas}`;
                document.getElementById('historicoFaltas').textContent = `Faltas: ${faltas}`;
                new bootstrap.Modal(document.getElementById('historicoModal')).show();
            };

            const btnExcluir = document.createElement('button');
            btnExcluir.textContent = "🗑️";
            btnExcluir.classList.add("btn", "btn-warning", "btn-sm");
            btnExcluir.onclick = () => alunoItem.remove();

            alunoItem.append(nomeSpan, btnPresente, btnFalta, btnHistorico, btnExcluir);
            cell.appendChild(alunoItem);
        }

        function logout() {
            document.getElementById('admin').classList.add('d-none');
            document.getElementById('auth').classList.remove('d-none');
        }

        function atualizarHistorico() {
            // Atualiza o histórico de presenças e faltas
        }
    </script>

</body>
</html>
