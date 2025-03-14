<!DOCTYPE html>
<html lang="pt-br">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Gerenciamento de Alunos - Sistema de Chamada</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/css/bootstrap.min.css" rel="stylesheet">
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/js/bootstrap.bundle.min.js"></script>

    <style>
        body {
            background: linear-gradient(135deg, #4e54c8, #8f94fb);
            color: #333;
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            font-family: 'Arial', sans-serif;
            padding: 20px;
        }

        .container-admin {
            background: rgba(255, 255, 255, 0.9);
            padding: 30px;
            border-radius: 15px;
            box-shadow: 0px 10px 30px rgba(0, 0, 0, 0.1);
            width: 100%;
            max-width: 1200px;
        }

        .btn-remove,
        .btn-add-calendar,
        .btn-presenca,
        .btn-falta {
            border: none;
            padding: 5px 10px;
            border-radius: 5px;
            cursor: pointer;
            font-size: 12px;
        }

        .btn-remove {
            background: red;
            color: white;
        }

        .btn-presenca {
            background: green;
            color: white;
        }

        .btn-falta {
            background: red;
            color: white;
        }

        .aluno-item {
            display: flex;
            align-items: center;
            justify-content: space-between;
            margin-bottom: 10px;
            padding: 10px;
            background: white;
            border-radius: 5px;
            box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
        }

        .btn-clear-all {
            background-color: #dc3545;
            color: white;
            border: none;
            padding: 10px 20px;
            border-radius: 5px;
            cursor: pointer;
            font-size: 16px;
            margin-top: 20px;
            display: block;
            width: 100%;
        }

        .hidden {
            display: none;
        }

        .status-container {
            display: flex;
            justify-content: flex-start;
            align-items: center;
        }

        .status-container .btn-presenca,
        .status-container .btn-falta {
            margin-left: 10px;
        }

        .btn-status {
            background-color: #f7c500;
            color: white;
            border: none;
            cursor: pointer;
            font-size: 16px;
        }

        .justificativa-falta {
            margin-top: 5px;
            display: none;
        }

        .justificativa-falta textarea {
            width: 100%;
            padding: 10px;
            border: 1px solid #ddd;
            border-radius: 5px;
            font-size: 14px;
        }

        .justificativa-falta button {
            margin-top: 10px;
            background-color: #28a745;
            color: white;
            border: none;
            padding: 5px 10px;
            border-radius: 5px;
        }
    </style>
</head>

<body>

    <div class="container-admin">
        <h2>Gerenciar Alunos - Sistema de Chamada</h2>

        <!-- Filtro de Disciplina -->
        <div class="mb-3">
            <label for="filtroDisciplina" class="form-label">Filtrar por Disciplina</label>
            <select id="filtroDisciplina" class="form-select" onchange="filtrarAlunos()">
                <option value="">Todas as Disciplinas</option>
                <option value="Street Dance">Street Dance</option>
                <option value="Futebol">Futebol</option>
                <option value="Música">Música</option>
                <option value="Ludoteca Segunda e Quarta">Ludoteca Segunda e Quarta</option>
                <option value="Contação de Histórias">Contação de Histórias</option>
                <option value="Ballet">Ballet</option>
                <option value="Vôlei">Vôlei</option>
                <option value="Ludoteca Terça e Quinta">Ludoteca Terça e Quinta</option>
                <option value="Teatro">Teatro</option>
                <option value="Programa Eureka">Programa Eureka</option>
                <option value="Sucatoteca">Sucatoteca</option>
                <option value="Adolescer">Adolescer</option>
            </select>
        </div>

        <!-- Formulário para adicionar aluno -->
        <div class="mb-3">
            <input type="text" id="nomeAluno" class="form-control" placeholder="Nome do Aluno">
        </div>

        <div class="mb-3">
            <label for="disciplina1" class="form-label">Disciplina 1</label>
            <select id="disciplina1" class="form-select">
                <option value="">Selecione a Disciplina</option>
                <option value="Street Dance">Street Dance</option>
                <option value="Futebol">Futebol</option>
                <option value="Música">Música</option>
                <option value="Ludoteca Segunda e Quarta">Ludoteca Segunda e Quarta</option>
                <option value="Contação de Histórias">Contação de Histórias</option>
                <option value="Ballet">Ballet</option>
                <option value="Vôlei">Vôlei</option>
                <option value="Ludoteca Terça e Quinta">Ludoteca Terça e Quinta</option>
                <option value="Teatro">Teatro</option>
                <option value="Programa Eureka">Programa Eureka</option>
                <option value="Sucatoteca">Sucatoteca</option>
                <option value="Adolescer">Adolescer</option>
            </select>
        </div>

        <div class="mb-3">
            <label for="disciplina2" class="form-label">Disciplina 2</label>
            <select id="disciplina2" class="form-select">
                <option value="">Selecione a Disciplina</option>
                <option value="Street Dance">Street Dance</option>
                <option value="Futebol">Futebol</option>
                <option value="Música">Música</option>
                <option value="Ludoteca Segunda e Quarta">Ludoteca Segunda e Quarta</option>
                <option value="Contação de Histórias">Contação de Histórias</option>
                <option value="Ballet">Ballet</option>
                <option value="Vôlei">Vôlei</option>
                <option value="Ludoteca Terça e Quinta">Ludoteca Terça e Quinta</option>
                <option value="Teatro">Teatro</option>
                <option value="Programa Eureka">Programa Eureka</option>
                <option value="Sucatoteca">Sucatoteca</option>
                <option value="Adolescer">Adolescer</option>
            </select>
        </div>

        <div class="mb-3">
            <select id="periodo" class="form-select">
                <option value="">Período</option>
                <option value="Periodo Manha 1">Periodo Manha 1</option>
                <option value="Periodo Manha 2">Periodo Manha 2</option>
                <option value="Periodo Tarde 1">Periodo Tarde 1</option>
                <option value="Periodo Tarde 2">Periodo Tarde 2</option>
            </select>
        </div>

        <div class="mb-3">
            <select id="diaSemana" class="form-select">
                <option value="">Dia da Semana</option>
                <option value="segunda">Segunda</option>
                <option value="terca">Terça</option>
                <option value="quarta">Quarta</option>
                <option value="quinta">Quinta</option>
                <option value="sexta">Sexta</option>
                <option value="Segunda e Quarta">Segunda e Quarta</option>
                <option value="Terça e Quinta">Terça e Quinta</option>
            </select>
        </div>

        <div class="mb-3">
            <input type="text" id="professor" class="form-control" placeholder="Nome do Professor">
        </div>

        <button class="btn btn-primary w-100" onclick="adicionarAluno()">Adicionar Aluno</button>

        <!-- Lista de Alunos -->
        <h4 class="mt-4">Lista de Alunos</h4>
        <button class="btn btn-secondary w-100 mb-3" onclick="toggleAlunos()">Mostrar/Esconder Alunos</button>
        <div id="listaAlunos"></div>

        <!-- Botão para limpar todos os dados -->
        <button class="btn-clear-all" onclick="limparTodosDados()">Limpar Todos os Alunos</button>
    </div>

    <script>
        let alunos = JSON.parse(localStorage.getItem("alunos")) || [];
        let filtroDisciplina = "";

        // Função para limpar filtro de disciplina
        function clearFiltro() {
            document.getElementById("filtroDisciplina").value = "";
            filtroDisciplina = "";
            renderizarListaAlunos();
        }

        // Função para adicionar aluno
        function adicionarAluno() {
            const nome = document.getElementById('nomeAluno').value;
            const disciplina1 = document.getElementById('disciplina1').value;
            const disciplina2 = document.getElementById('disciplina2').value;
            const periodo = document.getElementById('periodo').value;
            const diaSemana = document.getElementById('diaSemana').value;
            const professor = document.getElementById('professor').value;

            if (!nome || (!disciplina1 && !disciplina2) || !periodo || !diaSemana || !professor) {
                alert("Preencha todos os campos.");
                return;
            }

            if (disciplina1) {
                alunos.push({ nome, disciplina: disciplina1, periodo, diaSemana, professor, status: null, justificativa: "" });
            }

            if (disciplina2) {
                alunos.push({ nome, disciplina: disciplina2, periodo, diaSemana, professor, status: null, justificativa: "" });
            }

            localStorage.setItem("alunos", JSON.stringify(alunos));
            renderizarListaAlunos();
        }

        // Função para mostrar ou esconder a lista de alunos
        function toggleAlunos() {
            const lista = document.getElementById("listaAlunos");
            lista.classList.toggle("hidden");
        }

        // Função para renderizar lista de alunos por Período, Dia e Professor
        function renderizarListaAlunos() {
            const listaAlunosDiv = document.getElementById("listaAlunos");
            listaAlunosDiv.innerHTML = "";

            let alunosFiltrados = alunos.filter(aluno => {
                return filtroDisciplina ? aluno.disciplina === filtroDisciplina : true;
            });

            // Agrupar alunos por Período > Dia > Professor
            let alunosAgrupados = alunosFiltrados.reduce((acc, aluno) => {
                if (!acc[aluno.periodo]) acc[aluno.periodo] = {};
                if (!acc[aluno.periodo][aluno.diaSemana]) acc[aluno.periodo][aluno.diaSemana] = {};
                if (!acc[aluno.periodo][aluno.diaSemana][aluno.professor]) {
                    acc[aluno.periodo][aluno.diaSemana][aluno.professor] = [];
                }
                acc[aluno.periodo][aluno.diaSemana][aluno.professor].push(aluno);
                return acc;
            }, {});

            // Exibir a estrutura agrupada
            for (let periodo in alunosAgrupados) {
                const periodoDiv = document.createElement("div");
                periodoDiv.classList.add("periodo");
                periodoDiv.innerHTML = `<h5>Período: ${periodo}</h5>`;

                for (let dia in alunosAgrupados[periodo]) {
                    const diaDiv = document.createElement("div");
                    diaDiv.classList.add("dia");
                    diaDiv.innerHTML = `<h6>Dia: ${dia}</h6>`;

                    for (let professor in alunosAgrupados[periodo][dia]) {
                        const professorDiv = document.createElement("div");
                        professorDiv.classList.add("professor");
                        professorDiv.innerHTML = `<h7>Professor: ${professor}</h7>`;

                        alunosAgrupados[periodo][dia][professor].forEach((aluno, index) => {
                            const alunoDiv = document.createElement("div");
                            alunoDiv.classList.add("aluno-item");

                            alunoDiv.innerHTML = `
                                <span>${aluno.nome} - ${aluno.disciplina}</span>
                                <div class="status-container">
                                    <button class="btn-presenca" onclick="marcarStatus(${index})">Presente</button>
                                    <button class="btn-falta" onclick="marcarStatus(${index})">Faltou</button>
                                    <button class="btn-remove" onclick="removerAluno(${index})">Remover</button>
                                </div>
                            `;

                            professorDiv.appendChild(alunoDiv);
                        });

                        diaDiv.appendChild(professorDiv);
                    }

                    periodoDiv.appendChild(diaDiv);
                }

                listaAlunosDiv.appendChild(periodoDiv);
            }
        }

        // Função para marcar presença ou falta
        function marcarStatus(index) {
            const aluno = alunos[index];
            if (aluno.status === "Presente") {
                aluno.status = "Faltou";
            } else {
                aluno.status = "Presente";
            }
            localStorage.setItem("alunos", JSON.stringify(alunos));
            renderizarListaAlunos();
        }

        // Função para remover aluno
        function removerAluno(index) {
            alunos.splice(index, 1);
            localStorage.setItem("alunos", JSON.stringify(alunos));
            renderizarListaAlunos();
        }

        // Função para limpar todos os dados
        function limparTodosDados() {
            if (confirm("Tem certeza que deseja limpar todos os dados?")) {
                alunos = [];
                localStorage.removeItem("alunos");
                renderizarListaAlunos();
            }
        }

        // Inicializar a renderização do sistema
        renderizarListaAlunos();
    </script>

</body>

</html>
