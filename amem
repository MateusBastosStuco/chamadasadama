<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Gerenciamento de Presença</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/css/bootstrap.min.css" rel="stylesheet">
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/js/bootstrap.bundle.min.js"></script>
    <style>
        body {
            background: linear-gradient(135deg, #6a11cb, #2575fc);
            color: white;
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            font-family: 'Arial', sans-serif;
            margin: 0;
            padding: 20px;
        }

        #auth-container {
            background: rgba(255, 255, 255, 0.95);
            padding: 40px;
            border-radius: 15px;
            box-shadow: 0px 10px 30px rgba(0, 0, 0, 0.1);
            max-width: 400px;
            width: 100%;
            text-align: center;
            color: #333;
        }

        .container-admin {
            background: rgba(255, 255, 255, 0.9);
            border-radius: 15px;
            padding: 30px;
            box-shadow: 0 8px 25px rgba(0, 0, 0, 0.1);
            color: #333;
            max-width: 1200px;
            width: 100%;
        }

        .hidden {
            display: none;
        }

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
            font-weight: bold;
        }

        .calendar-cell {
            background: #fff;
            padding: 20px;
            border-radius: 10px;
            min-height: 150px;
            box-shadow: 0 6px 15px rgba(0, 0, 0, 0.1);
            transition: transform 0.3s ease;
        }

        .calendar-cell:hover {
            transform: translateY(-5px);
        }

        .status {
            display: flex;
            gap: 10px;
            justify-content: center;
            margin-top: 10px;
        }

        hr {
            border: 0;
            border-top: 2px solid #6a11cb;
            margin: 20px 0;
        }

        .historico {
            display: none;
            background: #f8f9fa;
            padding: 10px;
            margin-top: 10px;
            border-radius: 8px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
            font-size: 14px;
        }

        .aluno:hover .historico {
            display: block;
        }

        .btn-historico {
            background-color: #17a2b8;
            color: white;
            padding: 6px 16px;
            border-radius: 8px;
            font-size: 14px;
            transition: background-color 0.3s;
        }

        .btn-historico:hover {
            background-color: #138496;
        }

        .btn-primary, .btn-danger {
            border-radius: 8px;
            transition: background-color 0.3s, transform 0.2s;
        }

        .btn-primary:hover, .btn-danger:hover {
            transform: translateY(-3px);
        }

        .btn-primary {
            background-color: #007bff;
        }

        .btn-danger {
            background-color: #dc3545;
        }

        .btn-primary:focus, .btn-danger:focus {
            outline: none;
            box-shadow: 0 0 10px rgba(0, 123, 255, 0.5);
        }

        .form-control, .form-select {
            border-radius: 8px;
            padding: 10px;
            margin-bottom: 15px;
            background-color: #f9f9f9;
            border: 1px solid #ddd;
        }

        .form-control:focus, .form-select:focus {
            border-color: #6a11cb;
            box-shadow: 0 0 8px rgba(106, 17, 203, 0.5);
        }

        .calendar-cell .aluno {
            background-color: #f1f1f1;
            padding: 12px;
            border-radius: 8px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.05);
            margin-bottom: 10px;
            font-size: 14px;
            transition: background-color 0.3s, transform 0.2s;
        }

        .calendar-cell .aluno:hover {
            background-color: #e9ecef;
            transform: translateY(-3px);
        }

        .container-admin h2, .container-admin h3 {
            color: #333;
        }

        .container-admin h3 {
            margin-top: 20px;
            font-size: 18px;
        }

        /* Responsividade */
        @media (max-width: 768px) {
            .calendar {
                grid-template-columns: 1fr 1fr;
            }
        }

        @media (max-width: 480px) {
            .calendar {
                grid-template-columns: 1fr;
            }

            #auth-container, .container-admin {
                padding: 20px;
            }
        }
    </style>
</head>
<body>
    <div id="auth-container">
        <h2 class="text-center">Acesso</h2>
        <button class="btn btn-primary w-100 mb-2" onclick="login()">Entrar</button>
    </div>

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
        <select id="periodo" class="form-select my-2">
            <option value="">Período</option>
            <option value="manha">Manhã</option>
            <option value="tarde">Tarde</option>
        </select>
        <select id="disciplina" class="form-select my-2">
            <option value="">Disciplina</option>
            <option value="voleibol">Voleibol</option>
            <option value="futebol">Futebol</option>
            <option value="street">Street</option>
            <option value="teatro">Teatro</option>
            <option value="ludoteca">Ludoteca</option>
            <option value="eureca">Eureca</option>
            <option value="musica">Música</option>
        </select>
        <button class="btn btn-primary w-100" onclick="adicionarAluno()">Adicionar Aluno</button>

        <hr>

        <h3 class="text-center mt-4">Filtrar por Disciplina</h3>
        <select id="filtroDisciplina" class="form-select my-2" onchange="filtrarPorDisciplina()">
            <option value="">Exibir Todos</option>
            <option value="voleibol">Voleibol</option>
            <option value="futebol">Futebol</option>
            <option value="street">Street</option>
            <option value="teatro">Teatro</option>
            <option value="ludoteca">Ludoteca</option>
            <option value="eureca">Eureca</option>
            <option value="musica">Música</option>
        </select>

        <hr>

        <div class="calendar">
            <div class="calendar-header">Segunda</div>
            <div class="calendar-header">Terça</div>
            <div class="calendar-header">Quarta</div>
            <div class="calendar-header">Quinta</div>
            <div class="calendar-header">Sexta</div>

            <div id="segunda" class="calendar-cell"></div>
            <div id="terca" class="calendar-cell"></div>
            <div id="quarta" class="calendar-cell"></div>
            <div id="quinta" class="calendar-cell"></div>
            <div id="sexta" class="calendar-cell"></div>
        </div>

        <hr>

        <button class="btn btn-danger w-100 mt-3" onclick="logout()">Sair</button>
    </div>

    <!-- Modal de Histórico -->
    <div class="modal fade" id="modalHistorico" tabindex="-1" aria-labelledby="modalHistoricoLabel" aria-hidden="true">
        <div class="modal-dialog">
            <div class="modal-content">
                <div class="modal-header">
                    <h5 class="modal-title" id="modalHistoricoLabel">Histórico de Presença</h5>
                    <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                </div>
                <div class="modal-body" id="historicoModalContent" style="color: black;">
                    <!-- O conteúdo do histórico será inserido aqui -->
                </div>
                <div class="modal-footer">
                    <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Fechar</button>
                </div>
            </div>
        </div>
    </div>

    <script>
        let alunos = [];

        function login() {
            document.getElementById('auth-container').classList.add('hidden');
            document.getElementById('admin').classList.remove('hidden');
        }

        function logout() {
            document.getElementById('auth-container').classList.remove('hidden');
            document.getElementById('admin').classList.add('hidden');
        }

        function adicionarAluno() {
            const nome = document.getElementById('nomeAluno').value;
            const diaSemana = document.getElementById('diaSemana').value;
            const periodo = document.getElementById('periodo').value;
            const disciplina = document.getElementById('disciplina').value;

            if (!nome || !diaSemana || !periodo || !disciplina) {
                alert("Por favor, preencha todos os campos.");
                return;
            }

            const aluno = { nome, diaSemana, periodo, disciplina, presenca: [], historico: [] };
            alunos.push(aluno);
            alert("Aluno adicionado com sucesso!");

            document.getElementById('nomeAluno').value = '';
            document.getElementById('diaSemana').value = '';
            document.getElementById('periodo').value = '';
            document.getElementById('disciplina').value = '';

            renderizarCalendario();
        }

        function renderizarCalendario() {
            const dias = ["segunda", "terca", "quarta", "quinta", "sexta"];
            dias.forEach(dia => {
                document.getElementById(dia).innerHTML = '';
            });

            alunos.forEach(aluno => {
                const cell = document.getElementById(aluno.diaSemana);
                if (cell) {
                    const alunoDiv = document.createElement('div');
                    alunoDiv.classList.add('aluno');
                    alunoDiv.innerHTML = `
                        <strong>${aluno.nome}</strong>
                        <br>
                        <button class="btn btn-historico" data-bs-toggle="modal" data-bs-target="#modalHistorico" onclick="mostrarHistorico('${aluno.nome}')">Histórico</button>
                        <div class="status">
                            <button class="btn btn-success" onclick="marcarPresenca('${aluno.nome}')">Presença</button>
                            <button class="btn btn-danger" onclick="marcarFalta('${aluno.nome}')">Falta</button>
                        </div>
                        <br>
                        <strong>Porcentagem de Faltas: </strong>${calcularPorcentagemFaltas(aluno)}%
                    `;
                    cell.appendChild(alunoDiv);
                }
            });
        }

        function mostrarHistorico(nome) {
            const aluno = alunos.find(a => a.nome === nome);
            if (aluno) {
                const historicoContent = aluno.historico.join('<br>');
                document.getElementById('historicoModalContent').innerHTML = `<strong>${nome}</strong><br>${historicoContent}`;
            }
        }

        function marcarPresenca(nome) {
            const aluno = alunos.find(a => a.nome === nome);
            if (aluno) {
                aluno.presenca.push('Presente');
                aluno.historico.push('Presença');
                renderizarCalendario();
            }
        }

        function marcarFalta(nome) {
            const aluno = alunos.find(a => a.nome === nome);
            if (aluno) {
                aluno.presenca.push('Falta');
                aluno.historico.push('Falta');
                renderizarCalendario();
            }
        }

        function calcularPorcentagemFaltas(aluno) {
            const totalRegistros = aluno.presenca.length;
            if (totalRegistros === 0) {
                return 0;
            }

            const faltas = aluno.presenca.filter(p => p === 'Falta').length;
            return (faltas / totalRegistros) * 100;
        }

        function filtrarPorDisciplina() {
            const disciplinaFiltro = document.getElementById('filtroDisciplina').value;
            const dias = ["segunda", "terca", "quarta", "quinta", "sexta"];
            dias.forEach(dia => {
                document.getElementById(dia).innerHTML = '';
            });

            alunos
                .filter(aluno => !disciplinaFiltro || aluno.disciplina === disciplinaFiltro)
                .forEach(aluno => {
                    const cell = document.getElementById(aluno.diaSemana);
                    if (cell) {
                        const alunoDiv = document.createElement('div');
                        alunoDiv.classList.add('aluno');
                        alunoDiv.innerHTML = `
                            <strong>${aluno.nome}</strong>
                            <br>
                            <button class="btn btn-historico" data-bs-toggle="modal" data-bs-target="#modalHistorico" onclick="mostrarHistorico('${aluno.nome}')">Histórico</button>
                            <div class="status">
                                <button class="btn btn-success" onclick="marcarPresenca('${aluno.nome}')">Presença</button>
                                <button class="btn btn-danger" onclick="marcarFalta('${aluno.nome}')">Falta</button>
                            </div>
                            <br>
                            <strong>Porcentagem de Faltas: </strong>${calcularPorcentagemFaltas(aluno)}%
                        `;
                        cell.appendChild(alunoDiv);
                    }
                });
        }
    </script>
</body>
</html>
