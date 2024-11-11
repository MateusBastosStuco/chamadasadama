<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Chamada Online</title>
    <style>
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Arial', sans-serif;
        }

        body {
            min-height: 100vh;
            background: linear-gradient(135deg, #00B4DB, #0083B0);
            color: #fff;
            display: flex;
            flex-direction: column;
            align-items: center;
            padding: 20px;
            overflow-x: hidden;
        }

        h1 {
            font-size: 2.5em;
            text-align: center;
            margin-bottom: 20px;
            font-weight: 700;
            letter-spacing: 1px;
        }

        input,
        select,
        button {
            width: 100%;
            max-width: 400px;
            padding: 12px;
            margin: 10px 0;
            border: 2px solid #ddd;
            border-radius: 8px;
            font-size: 1em;
            outline: none;
        }

        input:focus,
        select:focus,
        button:focus {
            border-color: #4A90E2;
            box-shadow: 0 0 5px rgba(74, 144, 226, 0.8);
        }

        button {
            background-color: #4A90E2;
            color: #ffffff;
            font-weight: bold;
            cursor: pointer;
            transition: background-color 0.3s ease, transform 0.2s;
        }

        button:hover {
            background-color: #357ABD;
            transform: scale(1.05);
        }

        ul {
            list-style-type: none;
            margin: 20px 0;
            padding: 0;
            width: 100%;
            max-width: 450px;
        }

        ul li {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 12px 20px;
            background: #fff;
            margin: 10px 0;
            border-radius: 10px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
            color: #333;
            font-size: 1.1em;
        }

        ul li:hover {
            background-color: #f4f4f4;
        }

        .attendance-buttons {
            display: flex;
            gap: 10px;
        }

        .attendance-buttons button {
            padding: 10px 15px;
            font-size: 1em;
            font-weight: bold;
            color: #fff;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            transition: background-color 0.3s ease, transform 0.2s;
        }

        .presente {
            background-color: #4CAF50;
        }

        .falta {
            background-color: #FF5252;
        }

        .presente:hover {
            background-color: #45a049;
            transform: scale(1.05);
        }

        .falta:hover {
            background-color: #ff3d3d;
            transform: scale(1.05);
        }

        .historico {
            display: none;
            width: 100%;
            max-width: 450px;
            background: #f4f4f4;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
            margin-top: 20px;
            overflow-y: auto;
            max-height: 300px; /* Limita a altura do histórico */
        }

        .historico h2 {
            text-align: center;
            margin-bottom: 15px;
            color: #333;
        }

        .historico ul {
            padding-left: 20px;
        }

        .historico li {
            padding: 8px 0;
            font-size: 1.1em;
            color: #000000;
        }

        .historico .presenca {
            color: #4CAF50;
        }

        .historico .falta {
            color: #000000;
        }

        /* Ajuste para telas menores */
        @media (max-width: 600px) {
            body {
                padding: 15px;
            }
            h1 {
                font-size: 2em;
            }
            input,
            select,
            button {
                max-width: 100%;
            }
            ul li {
                font-size: 1em;
                flex-direction: column;
                align-items: flex-start;
            }
            .attendance-buttons {
                margin-top: 10px;
                justify-content: flex-start;
            }
            .historico {
                padding: 15px;
                max-height: 250px; /* Limita a altura do histórico para telas menores */
            }
            .historico h2 {
                font-size: 1.5em;
            }
            .historico ul li {
                font-size: 1em;
            }
        }
    </style>
</head>

<body>
    <h1>Chamada Online</h1>

    <input type="text" id="nova-turma" placeholder="Nome da Turma">
    <button onclick="adicionarTurma()">Adicionar Turma</button>

    <select id="turma" onchange="mostrarAlunos(this.value)"></select>

    <input type="text" id="novo-aluno" placeholder="Nome do Aluno">
    <button onclick="adicionarAluno()">Adicionar Aluno</button>

    <ul id="lista-alunos"></ul>

    <div id="historico" class="historico">
        <h2>Histórico</h2>
        <ul id="lista-historico"></ul>
    </div>

    <script>
        let turmas = JSON.parse(localStorage.getItem("turmas")) || {};
        const turmaSelect = document.getElementById("turma");
        const listaAlunos = document.getElementById("lista-alunos");
        const listaHistorico = document.getElementById("lista-historico");
        const historicoContainer = document.getElementById("historico");

        carregarTurmas();

        function adicionarTurma() {
            const novaTurma = document.getElementById("nova-turma").value.trim();
            if (novaTurma && !turmas[novaTurma]) {
                turmas[novaTurma] = { alunos: [], historico: {} };
                salvarTurmas();
                carregarTurmas();
                document.getElementById("nova-turma").value = "";
            }
        }

        function carregarTurmas() {
            turmaSelect.innerHTML = "";
            for (const turma in turmas) {
                const option = document.createElement("option");
                option.value = turma;
                option.textContent = turma;
                turmaSelect.appendChild(option);
            }
            mostrarAlunos(turmaSelect.value);
        }

        function adicionarAluno() {
            const turmaSelecionada = turmaSelect.value;
            const novoAluno = document.getElementById("novo-aluno").value.trim();
            if (novoAluno && !turmas[turmaSelecionada].alunos.includes(novoAluno)) {
                turmas[turmaSelecionada].alunos.push(novoAluno);
                salvarTurmas();
                mostrarAlunos(turmaSelecionada);
                document.getElementById("novo-aluno").value = "";
            }
        }

        function salvarTurmas() {
            localStorage.setItem("turmas", JSON.stringify(turmas));
        }

        function mostrarAlunos(turma) {
            listaAlunos.innerHTML = "";
            const alunos = turmas[turma].alunos || [];
            alunos.forEach(aluno => {
                const li = document.createElement("li");
                li.textContent = aluno;

                const btnPresente = document.createElement("button");
                btnPresente.className = "presente";
                btnPresente.textContent = "C";
                btnPresente.onclick = () => marcarPresenca(aluno, "C");

                const btnFalta = document.createElement("button");
                btnFalta.className = "falta";
                btnFalta.textContent = "F";
                btnFalta.onclick = () => marcarPresenca(aluno, "F");

                const btnHistorico = document.createElement("button");
                btnHistorico.textContent = "Histórico";
                btnHistorico.onclick = () => mostrarHistorico(aluno);

                const btnContainer = document.createElement("div");
                btnContainer.className = "attendance-buttons";
                btnContainer.appendChild(btnPresente);
                btnContainer.appendChild(btnFalta);
                btnContainer.appendChild(btnHistorico);
                li.appendChild(btnContainer);

                listaAlunos.appendChild(li);
            });
        }

        function marcarPresenca(aluno, status) {
            const dataHora = new Date().toLocaleString();
            const turma = turmaSelect.value;
            const historico = turmas[turma].historico || {};
            historico[aluno] = historico[aluno] || [];
            historico[aluno].push({ status, dataHora });
            turmas[turma].historico = historico;
            salvarTurmas();
        }

        function mostrarHistorico(aluno) {
            listaHistorico.innerHTML = "";
            const turma = turmaSelect.value;
            const historico = turmas[turma].historico || {};
            const registros = historico[aluno] || [];
            registros.forEach(registro => {
                const li = document.createElement("li");
                li.className = registro.status === "C" ? "presenca" : "falta";
                li.textContent = `${registro.dataHora} - ${registro.status === "C" ? "Presente" : "Falta"}`;
                listaHistorico.appendChild(li);
            });
            historicoContainer.style.display = "block";
        }
    </script>
</body>
</html>
