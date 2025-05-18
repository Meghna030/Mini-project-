<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>MedMate</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 0;
      padding: 0;
    }

    header {
      background-color: #333;
      color: #fff;
      padding: 1em;
      text-align: center;
    }

    nav ul {
      list-style: none;
      margin: 0;
      padding: 0;
      display: flex;
      justify-content: center;
      gap: 2em;
    }

    nav a {
      color: #fff;
      text-decoration: none;
    }

    main {
      display: flex;
      flex-direction: column;
      align-items: center;
      padding: 2em;
    }

    section {
      background-color: #f7f7f7;
      padding: 1em;
      margin: 1em 0;
      width: 80%;
      max-width: 600px;
      box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
    }

    h1 {
      margin-top: 0;
    }

    label {
      display: block;
      margin-top: 10px;
    }

    input, select, button {
      width: 100%;
      padding: 0.5em;
      margin-top: 5px;
      box-sizing: border-box;
    }

    button {
      background-color: #4CAF50;
      color: white;
      border: none;
      cursor: pointer;
      margin-top: 10px;
    }

    button:hover {
      background-color: #45a049;
    }

    #reminders-list {
      list-style: none;
      padding: 0;
      margin-top: 1em;
    }

    #reminders-list li {
      padding: 10px;
      border-bottom: 1px solid #ccc;
    }

    #pharmacy-results {
      padding: 10px;
      margin-top: 1em;
    }

    ul {
      padding-left: 20px;
    }

    ul li {
      margin-bottom: 0.5em;
    }

    /* Background Slideshow Styles */
    #home {
      position: relative;
      height: 400px;
      width: 100%;
      color: white;
      display: flex;
      align-items: center;
      justify-content: center;
      text-align: center;
      background-size: cover;
      background-position: center;
      animation: backgroundSlideshow 20s infinite ease-in-out;
      box-shadow: 0 0 10px rgba(0,0,0,0.3);
    }

    .slideshow-overlay {
      background-color: rgba(0, 0, 0, 0.5);
      padding: 2em;
      width: 100%;
    }

    @keyframes backgroundSlideshow {
      0%   { background-image: url('https://images.unsplash.com/photo-1666886573197-bf6600d15bce?q=80&w=2070&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D'); }
      33%  { background-image: url('https://plus.unsplash.com/premium_photo-1675807264002-74250202f195?q=80&w=2070&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D'); }
      66%  { background-image: url('https://plus.unsplash.com/premium_photo-1681995460558-738a8856313c?q=80&w=2070&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D'); }
      100% { background-image: url('https://images.unsplash.com/photo-1576671081837-49000212a370?q=80&w=1998&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D'); }
    }
  </style>
</head>
<body>
  <header>
    <nav>
      <ul>
        <li><a href="#home">Home</a></li>
        <li><a href="#reminders">Reminders</a></li>
        <li><a href="#pharmacy">Pharmacy</a></li>
        <li><a href="#about">About</a></li>
      </ul>
    </nav>
  </header>

  <main>
    <section id="home">
      <div class="slideshow-overlay">
        <h1>Welcome to MedMate</h1>
        <p>Your smart health companion! MedMate helps you manage your medications effortlessly, sending you reminders and locating nearby pharmacies with just a few clicks. Stay healthy, stay on track — MedMate has you covered!</p>
      </div>
    </section>

    <section id="reminders">
      <h1>Medicine Reminders</h1>
      <form id="reminder-form">
        <label for="medicine-name">Medicine Name:</label>
        <input type="text" id="medicine-name" required>
        <label for="dosage">Dosage:</label>
        <input type="text" id="dosage" required>
        <label for="frequency">Frequency:</label>
        <select id="frequency" required>
          <option value="daily">Daily</option>
          <option value="weekly">Weekly</option>
          <option value="monthly">Monthly</option>
        </select>
        <button type="submit" id="add-reminder">Add Reminder</button>
      </form>
      <ul id="reminders-list"></ul>
    </section>

    <section id="pharmacy">
      <h1>Nearest Pharmacy</h1>
      <form id="pharmacy-form">
        <label for="pharmacy-medicine-name">Medicine Name:</label>
        <input type="text" id="pharmacy-medicine-name" required>
        <button type="submit" id="find-pharmacy">Find Pharmacy</button>
      </form>
      <div id="pharmacy-results"></div>
    </section>

    <section id="about">
      <h1>About MedMate</h1>
      <p><strong>MedMate</strong> is your intelligent health companion — designed to simplify your medication routine and help you stay on track. Whether it's daily pill reminders or finding the nearest pharmacy, MedMate makes managing your health effortless and stress-free.</p>

      <h2>Why Choose MedMate?</h2>
      <ul>
        <li>💊 Easy-to-set medication reminders (Premium Feature)</li>
        <li>📍 Quickly locate nearby pharmacies with your medicine</li>
        <li>🔔 Smart notification alerts to keep you on schedule</li>
        <li>📱 Simple, mobile-friendly interface</li>
        <li>🗂️ Stores your medication history for better tracking</li>
      </ul>
    </section>
  </main>

  <script>
    const remindersList = document.getElementById('reminders-list');
    const reminderForm = document.getElementById('reminder-form');
    const pharmacyForm = document.getElementById('pharmacy-form');
    const pharmacyResults = document.getElementById('pharmacy-results');

    let reminders = JSON.parse(localStorage.getItem('reminders')) || [];

    function saveReminders() {
      localStorage.setItem('reminders', JSON.stringify(reminders));
    }

    function renderReminders() {
      remindersList.innerHTML = '';
      reminders.forEach((reminder) => {
        const li = document.createElement('li');
        li.textContent = `${reminder.medicineName} - ${reminder.dosage} - ${reminder.frequency}`;
        remindersList.appendChild(li);
      });
    }

    function requestNotificationPermission() {
      if ('Notification' in window && Notification.permission !== 'granted') {
        Notification.requestPermission();
      }
    }

    function showNotification(title, body) {
      if ('Notification' in window && Notification.permission === 'granted') {
        new Notification(title, { body });
      }
    }

    reminderForm.addEventListener('submit', (e) => {
      e.preventDefault();
      alert("To set medicine reminders, you must have a Premium Membership.");

      // Premium logic (disabled for non-premium users)
      /*
      const medicineName = document.getElementById('medicine-name').value;
      const dosage = document.getElementById('dosage').value;
      const frequency = document.getElementById('frequency').value;

      const reminder = { medicineName, dosage, frequency };
      reminders.push(reminder);
      saveReminders();
      renderReminders();
      showNotification('New Reminder Added', `${medicineName} - ${dosage} (${frequency})`);
      */

      reminderForm.reset();
    });

    pharmacyForm.addEventListener('submit', (e) => {
      e.preventDefault();
      const medicine = document.getElementById('pharmacy-medicine-name').value;
      pharmacyResults.innerHTML = `<p>Searching for pharmacies with "${medicine}"...</p>`;
      setTimeout(() => {
        pharmacyResults.innerHTML = `
          <p><strong>PharmaPlus</strong> - 123 Health St.</p>
          <p><strong>WellCare</strong> - 456 Med Ave.</p>
          <p><strong>HealthHub</strong> - 789 Cure Blvd.</p>
        `;
      }, 1000);
      pharmacyForm.reset();
    });

    renderReminders();
    requestNotificationPermission();
  </script>
</body>
</html>

