<!DOCTYPE html>
<html lang="pt-br">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Gestão de Salas - Senai</title>
  <style>
    /* Cores e estilo do Senai com nova identidade visual */
    body {
            font-family: Arial, sans-serif;
            background-color: #e6f0ff;
            color: #333;
            margin: 0;
            display: flex;
            flex-direction: column;
            align-items: center;
        }

        .header {
            text-align: center;
            padding: 30px;
            background-color: #003366;
            color: white;
            width: 100%;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
            position: relative; /* Para o posicionamento do logo */
        }

        .header h1 {
            margin: 0;
        }

        .logo {
            position: absolute; /* Faz a imagem flutuar sobre a header */
            top: 15px; /* Alinha ao topo */
            left: 50px; /* Alinha à direita */
            width: 100px; /* Defina a largura desejada */
            height: auto; /* Mantém a proporção */
        }

        .menu {
            display: flex;
            justify-content: space-around;
            padding: 15px;
            background-color: #002244;
            width: 100%;
        }

        .menu a {
            color: white;
            text-decoration: none;
            padding: 10px 20px;
            font-weight: bold;
            transition: background-color 0.3s;
        }

        .menu a:hover {
            background-color: #0055a5;
            border-radius: 5px;
        }

        .search-bar {
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
            width: 100%;
        }

        .search-input {
            width: 60%;
            padding: 10px;
            font-size: 18px;
            border: 2px solid #0055a5;
            border-radius: 25px;
            transition: border-color 0.3s;
        }

        .search-input:focus {
            border-color: #003366;
            outline: none;
        }

        .search-icon {
            font-size: 20px;
            margin-left: -35px;
            color: #0055a5;
            cursor: pointer;
        }

        .container {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
            gap: 20px;
            padding: 20px;
            width: 100%;
            max-width: 1200px;
        }

        .room-card {
            background-color: #0055a5;
            color: white;
            padding: 25px;
            border-radius: 10px;
            text-align: center;
            cursor: pointer;
            transition: transform 0.3s, box-shadow 0.3s;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
        }

        .room-card:hover {
            transform: scale(1.05);
            box-shadow: 0 8px 16px rgba(0, 0, 0, 0.3);
        }

        .room-card img {
            border-radius: 8px;
            max-height: 150px;
            margin-bottom: 15px;
            width: 100%;
            object-fit: cover;
        }

        .room-card h3 {
            font-size: 20px;
            margin: 10px 0;
        }

        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.5);
            justify-content: center;
            align-items: center;
        }

        .modal-content { 
            background-color: white; 
            margin: 5% auto; 
            padding: 20px; 
            max-width: 400px; 
            border-radius: 15px; 
            box-shadow: 0 5px 15px rgba(0,0,0,0.3); 
        }

        .close {
            color: #aaa;
            float: right;
            font-size: 28px;
            font-weight: bold;
            cursor: pointer;
        }

        .close:hover {
            color: #0055a5;
        }

        .button {
            background-color: #0055a5;
            color: white;
            padding: 10px 25px;
            border: none;
            border-radius: 5px;
            font-size: 16px;
            cursor: pointer;
            transition: background-color 0.3s;
        }

        .button:hover {
            background-color: #003366;
        }

        .form-input { 
            width: 100%; 
            max-width: 350px; 
            padding: 12px; 
            margin: 10px 0; 
            border: 2px solid #ccc; 
            border-radius: 15px; 
            font-size: 16px; 
            transition: border 0.3s; 
        }

        .form-input:focus {
            border-color: #0055a5;
            outline: none;
        }

        /* Estilo para exibir agendas */
        .schedules-container {
            padding: 20px;
            width: 100%;
            max-width: 1200px;
        }

        .schedules-container h2 {
            margin: 20px 0;
        }

        .schedules-container ul {
            list-style: none;
            padding: 0;
        }

        .schedules-container li { 
            margin: 10px 0; 
            padding: 10px; 
            background-color: #e0f0ff; 
            border-radius: 10px; 
            box-shadow: 0 2px 5px rgba(0,0,0,0.2); 
        }
    </style>
</head>
<body>
    <div class="header">
        <h1>Gestão de Salas - Senai</h1>
        <img src="./URL_DA_LOGO_DO_SENAI.png" alt="Logo" class="logo"> <!-- Imagem no canto superior direito -->
    </div>

<div class="menu">
  <a href="Para a tv.html" id="my-agendas-link">Para a Tv</a>
  <a href="minhas-agendas.html" id="my-agendas-link">Minhas Agendas</a>
  <a href="salas-reservadas.html" id="reserved-rooms-link">Salas Reservadas</a>
  <a href="suporte.html">Algum Erro? Suporte Aqui</a>
</div>

<div class="search-bar">
  <input type="text" id="search-input" class="search-input" placeholder="Pesquisar sala..." onkeyup="filterRooms()">
  <span class="search-icon">&#128269;</span>
</div>

  
<div id="salas" class="container">
  <div class="room-card" onclick="openModal('Sala 101 - Informática')" data-room-name="Sala 101 - Informática">
    <img src="./SENAI.jpg" alt="Sala 101">
    <h3>Sala 101 - Informática</h3>
  </div>
  <div class="room-card" onclick="openModal('Sala 102 - Eletrônica')" data-room-name="Sala 102 - Eletrônica">
    <img src="./lest area de login.webp" alt="Sala 102">
    <h3>Sala 102 - Eletrônica</h3>
  </div>
  <div class="room-card" onclick="openModal('Sala 103 - Mecânica')" data-room-name="Sala 103 - Mecânica">
    <img src="./SENAI.jpg" alt="Sala 103">
    <h3>Sala 103 - Mecânica</h3>
  </div>
  <div class="room-card" onclick="openModal('Sala 104 - Química')" data-room-name="Sala 104 - Química">
    <img src="./lest area de login.webp" alt="Sala 104">
    <h3>Sala 104 - Química</h3>
  </div>
  <div class="room-card" onclick="openModal('Sala 105 - Física')" data-room-name="Sala 105 - Física">
    <img src="./Sala01.png" alt="Sala 105">
    <h3>Sala 105 - Física</h3>
  </div>
  <div class="room-card" onclick="openModal('Sala 105 - Física')" data-room-name="Sala 105 - Física">
    <img src="./SENAI.jpg" alt="Sala 105">
    <h3>Sala 105 - Progamação</h3>
  </div>
  <div class="room-card" onclick="openModal('Sala 105 - Física')" data-room-name="Sala 105 - Física">
    <img src="./Sala01.png" alt="Sala 105">
    <h3>Sala 105 - Matematica</h3>
  </div>
  <div class="room-card" onclick="openModal('Sala 105 - Física')" data-room-name="Sala 105 - Física">
    <img src="./lest area de login.webp" alt="Sala 105">
    <h3>Sala 105 - Logis</h3>
  </div>
</div>

<div id="modal" class="modal">
  <div class="modal-content">
    <span class="close" onclick="closeModal()">&times;</span>
    <h2 id="modal-room-name"></h2>
    <label for="instructor-name">Nome do Instrutor</label>
    <input type="text" id="instructor-name" class="form-input" placeholder="Digite o nome do instrutor">
    <label for="modal-capacity">Capacidade: 30 pessoas</label><br>
    <textarea id="modal-notes" class="form-input" placeholder="Observações"></textarea>
    <label for="start-date">Data e Hora de Início</label>
    <input type="datetime-local" id="start-date" class="form-input" min="" required>
    <label for="end-date">Data e Hora de Término</label>
    <input type="datetime-local" id="end-date" class="form-input" required>
    <button class="button" onclick="scheduleRoom()">Agendar</button>
  </div>
</div>

<div class="schedules-container" id="schedules-container" style="display: none;">
  <h2>Minhas Agendas</h2>
  <ul id="schedules-list"></ul>
</div>

<script>

  document.addEventListener("DOMContentLoaded", function() {
    const now = new Date();
    const minDate = now.toISOString().slice(0, 16);
    document.getElementById("start-date").setAttribute("min", minDate);
    document.getElementById("end-date").setAttribute("min", minDate);
  });

  const schedules = [];

  function openModal(roomName) {
    document.getElementById('modal-room-name').innerText = roomName;
    document.getElementById('modal').style.display = 'flex';
  }

  function closeModal() {
    document.getElementById('modal').style.display = 'none';
    document.getElementById('instructor-name').value = '';
    document.getElementById('modal-notes').value = '';
    document.getElementById('start-date').value = '';
    document.getElementById('end-date').value = '';
  }

  function scheduleRoom() {
    const instructorName = document.getElementById('instructor-name').value;
    const notes = document.getElementById('modal-notes').value;
    const startDate = document.getElementById('start-date').value;
    const endDate = document.getElementById('end-date').value;
    const roomName = document.getElementById('modal-room-name').innerText;

    if (new Date(startDate) >= new Date(endDate)) {
        alert('A data de início deve ser anterior à data de término.');
        return;
    }

    const existingSchedules = JSON.parse(localStorage.getItem('schedules')) || [];
    const conflict = existingSchedules.some(schedule => 
        schedule.roomName === roomName && (
            (new Date(startDate) < new Date(schedule.endDate) && new Date(endDate) > new Date(schedule.startDate))
        )
    );

    if (conflict) {
        alert('Já existe um agendamento para esta sala neste horário.');
        return;
    }

    const schedule = { roomName, instructorName, notes, startDate, endDate };
    schedules.push(schedule);  // Adiciona o agendamento ao array local
    existingSchedules.push(schedule);  // Salva no localStorage
    localStorage.setItem('schedules', JSON.stringify(existingSchedules));

    alert(`Sala ${roomName} agendada com sucesso!`);
    closeModal();
    displaySchedules();
}
   

  function displaySchedules() {
    const schedulesList = document.getElementById('schedules-list');
    schedulesList.innerHTML = '';
    schedules.forEach(schedule => {
      const li = document.createElement('li');
      li.innerText = `${schedule.roomName} - ${schedule.instructorName} (${schedule.startDate} a ${schedule.endDate})`;
      schedulesList.appendChild(li);
    });
    document.getElementById('schedules-container').style.display = schedules.length > 0 ? 'block' : 'none';
  }

  function filterRooms() {
    const input = document.getElementById('search-input');
    const filter = input.value.toLowerCase();
    const roomCards = document.querySelectorAll('.room-card');

    roomCards.forEach(card => {
      const roomName = card.getAttribute('data-room-name').toLowerCase();
      card.style.display = roomName.includes(filter) ? '' : 'none';
    });
  }
</script>
</body>
</html>
