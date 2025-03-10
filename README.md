<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Cadastro de Alunos</title>
    <style>
        /* Estilo geral */
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background-color: #f0f0f0;
        }

        .menu-container {
            background-color: #4CAF50;
            padding: 10px;
            color: white;
            text-align: center;
        }

        .menu {
            font-size: 24px;
            font-weight: bold;
        }

        .calendar-link {
            cursor: pointer;
            font-size: 20px;
            margin-left: 15px;
            color: white;
            text-decoration: none;
        }

        .form-container {
            margin: 20px;
            background-color: white;
            padding: 20px;
            border-radius: 5px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }

        .nome-aluno-container {
            margin-bottom: 20px;
        }

        .input-info {
            margin-bottom: 10px;
        }

        .input-info label {
            font-size: 14px;
            display: block;
        }

        .input-info input {
            width: 100%;
            padding: 8px;
            margin-top: 5px;
            font-size: 14px;
            border-radius: 3px;
            border: 1px solid #ddd;
        }

        .buttons-container {
            margin-top: 20px;
            display: flex;
            justify-content: space-between;
        }

        .button {
            padding: 10px 20px;
            font-size: 16px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            background-color: #4CAF50;
            color: white;
        }

        .button.delete {
            background-color: #f44336;
        }

        .student-list {
            margin: 20px;
            background-color: white;
            padding: 20px;
            border-radius: 5px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }

        .student-list ul {
            list-style-type: none;
            padding: 0;
        }

        .student-list li {
            background-color: #f4f4f4;
            padding: 10px;
            margin-bottom: 10px;
            border-radius: 3px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .student-list li .lupa-icon {
            cursor: pointer;
            font-size: 20px;
            color: #4CAF50;
        }

        .pasta {
            display: none;
            background-color: #f9f9f9;
            padding: 10px;
            border-radius: 5px;
        }

        .pasta-icon {
            cursor: pointer;
            font-size: 20px;
            margin-left: 10px;
        }

        .hidden {
            display: none;
        }

        .feedback {
            background-color: lightgreen;
            color: black;
            padding: 10px;
            margin-top: 10px;
            border-radius: 5px;
        }
    </style>
</head>
<body>

    <!-- Menu com o texto "MENU" -->
    <div class="menu-container">
        <div class="menu">MENU</div>
        <a href="https://mateusbastosstuco.github.io/Chamada-teste/" class="calendar-link" target="_blank">📅 Calendário</a>
    </div>

    <div class="form-container">
        <div class="nome-aluno-container">
            <label for="nome-aluno">Nome do Aluno:</label>
            <input type="text" id="nome-aluno" placeholder="Digite o nome do aluno">
            <span class="pasta-icon" onclick="mostrarPasta()">📁</span>
        </div>
        
        <div class="pasta" id="pasta">
            <h3>Informações do Aluno</h3>
            <div class="input-info">
                <label for="info-idade">Idade:</label>
                <input type="text" id="info-idade" placeholder="Digite a idade">
            </div>
            <div class="input-info">
                <label for="info-turma">Turma:</label>
                <input type="text" id="info-turma" placeholder="Digite a turma">
            </div>
            <div class="input-info">
                <label for="info-endereco">Endereço:</label>
                <input type="text" id="info-endereco" placeholder="Digite o endereço">
            </div>
            <div class="input-info">
                <label for="info-saude">Estado de Saúde:</label>
                <input type="text" id="info-saude" placeholder="Digite o estado de saúde">
            </div>
            <div class="input-info">
                <label for="info-responsavel">Responsável:</label>
                <input type="text" id="info-responsavel" placeholder="Digite o nome do responsável">
            </div>
        </div>

        <div class="buttons-container">
            <button class="button" onclick="adicionarAluno()">Adicionar Aluno</button>
            <button class="button delete" onclick="excluirAluno()">Excluir Aluno</button>
        </div>
    </div>

    <!-- Exibição da lista de alunos -->
    <div class="student-list">
        <h3>Lista de Alunos</h3>
        <ul id="list-alunos"></ul>
    </div>

    <div id="feedback" class="feedback hidden">Aluno Adicionado com Sucesso!</div>

    <script>
        let alunos = [];

        function mostrarPasta() {
            const pasta = document.getElementById("pasta");
            pasta.style.display = pasta.style.display === "block" ? "none" : "block";
        }

        function adicionarAluno() {
            const nomeAluno = document.getElementById("nome-aluno").value.trim();
            if (!nomeAluno) {
                alert("Por favor, insira um nome válido.");
                return;
            }

            // Verifica se há alunos no localStorage e obtém os dados existentes ou cria um array vazio
            let alunos = JSON.parse(localStorage.getItem("alunosCadastro")) || [];
            
            // Adiciona o novo aluno
            alunos.push({ nome: nomeAluno });
            
            // Salva novamente no localStorage
            localStorage.setItem("alunosCadastro", JSON.stringify(alunos));

            // Atualiza a lista na página
            atualizarListaDeAlunos();
            limparCampos();
            mostrarFeedback();
        }

        function excluirAluno() {
            const nomeAluno = document.getElementById("nome-aluno").value.trim();
            alunos = alunos.filter(aluno => aluno.nome !== nomeAluno);
            atualizarListaDeAlunos();
            limparCampos();
        }

        function atualizarListaDeAlunos() {
            const listAlunos = document.getElementById("list-alunos");
            listAlunos.innerHTML = "";
            alunos.forEach(aluno => {
                const li = document.createElement("li");
                li.textContent = `Nome: ${aluno.nome}, Idade: ${aluno.idade}, Turma: ${aluno.turma}`;

                const lupaIcon = document.createElement("span");
                lupaIcon.classList.add("lupa-icon");
                lupaIcon.textContent = "🔍";
                lupaIcon.onclick = () => mostrarInformacoes(aluno);

                li.appendChild(lupaIcon);
                listAlunos.appendChild(li);
            });
        }

        function mostrarInformacoes(aluno) {
            alert(`Nome: ${aluno.nome}\nIdade: ${aluno.idade}\nTurma: ${aluno.turma}\nEndereço: ${aluno.endereco}\nEstado de Saúde: ${aluno.saude}\nResponsável: ${aluno.responsavel}`);
        }

        function limparCampos() {
            document.querySelectorAll(".input-info input").forEach(input => input.value = "");
        }

        function mostrarFeedback() {
            const feedback = document.getElementById("feedback");
            feedback.classList.remove("hidden");
            setTimeout(() => feedback.classList.add("hidden"), 3000);
        }
    </script>

</body>
</html>
