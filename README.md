# Danton-Christian-association-
Danton Christian association
<!DOCTYPE html><html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Danton Christian Association</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <script src="https://www.gstatic.com/firebasejs/9.6.10/firebase-app-compat.js"></script>
  <script src="https://www.gstatic.com/firebasejs/9.6.10/firebase-auth-compat.js"></script>
</head>
<body class="bg-gray-100 text-gray-800">
  <!-- Navbar with Logo -->
  <header class="bg-blue-800 text-white p-4 flex justify-between items-center">
    <div class="flex items-center space-x-2">
      <img src="https://chat.openai.com/cdn-cgi/image/width=256,quality=100/https://files.oaiusercontent.com/file-XFk6SKSpN4SFaM6EBv1nJ3ZK?se=2025-07-26T21%3A13%3A23Z&sp=r&sv=2021-08-06&sr=b&sig=1QeQXwtm%2BWJWe6hRxguOCz7v3egMCbIkEsDf1oaAgSg%3D" alt="DCA Logo" class="w-10 h-10">
      <h1 class="text-xl font-bold">Danton Christian Association</h1>
    </div>
    <nav class="space-x-4">
      <a href="#" class="hover:underline">Home</a>
      <a href="#bible" class="hover:underline">Bible</a>
      <a href="#prayer" class="hover:underline">Prayer</a>
      <a href="#videos" class="hover:underline">Videos</a>
      <a href="#guides" class="hover:underline">Guides</a>
      <a href="#kids" class="hover:underline">Kids</a>
      <a href="#login" class="hover:underline">Login</a>
    </nav>
  </header>  <main class="p-6 space-y-6">
    <!-- Login Section -->
    <section id="login" class="bg-white p-4 rounded shadow">
      <h2 class="text-xl font-semibold mb-2">🔐 Login / Sign Up</h2>
      <input id="email" type="email" placeholder="Email" class="border p-2 w-full mb-2">
      <input id="password" type="password" placeholder="Password" class="border p-2 w-full mb-2">
      <div class="flex gap-2">
        <button onclick="login()" class="bg-blue-600 text-white px-4 py-2 rounded">Login</button>
        <button onclick="signup()" class="bg-green-600 text-white px-4 py-2 rounded">Sign Up</button>
        <button onclick="logout()" class="bg-red-600 text-white px-4 py-2 rounded">Logout</button>
      </div>
      <p id="authStatus" class="mt-2 text-sm text-green-600"></p>
    </section><!-- Other sections (Daily Verse, Streak, End Signs, etc.) -->
<section class="bg-white p-4 rounded shadow">
  <h2 class="text-xl font-semibold mb-2">📖 Daily Bible Verse</h2>
  <p id="dailyVerse">Loading verse...</p>
</section>

<section class="bg-white p-4 rounded shadow">
  <h2 class="text-xl font-semibold mb-2">🔥 Your Visit Streak</h2>
  <p>You have visited this site <span id="streak">0</span> day(s) in a row.</p>
</section>

<section id="videos" class="bg-white p-4 rounded shadow">
  <h2 class="text-xl font-semibold mb-2">🎥 Gospel Videos</h2>
  <iframe width="100%" height="315" src="https://www.youtube.com/embed/sz81dIfwf4Y" frameborder="0" allowfullscreen></iframe>
</section>

<section id="bible" class="bg-white p-4 rounded shadow">
  <h2 class="text-xl font-semibold mb-2">📚 Bible Chapters</h2>
  <a class="text-blue-600 underline" href="https://www.biblegateway.com/" target="_blank">Read Bible on BibleGateway</a>
</section>

  </main>  <footer class="bg-blue-800 text-white text-center p-4 mt-6">
    <p>&copy; 2025 Danton Christian Association. Publisher: Dantez482 (Danton Mariga)</p>
  </footer>  <script>
    // Firebase config
    const firebaseConfig = {
      apiKey: "YOUR_API_KEY",
      authDomain: "YOUR_PROJECT.firebaseapp.com",
      projectId: "YOUR_PROJECT",
      storageBucket: "YOUR_PROJECT.appspot.com",
      messagingSenderId: "YOUR_SENDER_ID",
      appId: "YOUR_APP_ID"
    };
    firebase.initializeApp(firebaseConfig);
    const auth = firebase.auth();

    function login() {
      const email = document.getElementById("email").value;
      const password = document.getElementById("password").value;
      auth.signInWithEmailAndPassword(email, password)
        .then(() => {
          document.getElementById("authStatus").innerText = "Logged in successfully!";
        })
        .catch(error => alert(error.message));
    }

    function signup() {
      const email = document.getElementById("email").value;
      const password = document.getElementById("password").value;
      auth.createUserWithEmailAndPassword(email, password)
        .then(() => {
          document.getElementById("authStatus").innerText = "Account created successfully!";
        })
        .catch(error => alert(error.message));
    }

    function logout() {
      auth.signOut().then(() => {
        document.getElementById("authStatus").innerText = "Logged out.";
      });
    }

    // Daily Verse
    fetch("https://beta.ourmanna.com/api/v1/get/?format=text")
      .then(response => response.text())
      .then(data => {
        document.getElementById("dailyVerse").innerText = data;
      })
      .catch(() => {
        document.getElementById("dailyVerse").innerText = "Could not load verse. Please try again later.";
      });

    // Streak Tracker
    const today = new Date().toDateString();
    const lastVisit = localStorage.getItem("lastVisit") || "";
    let streak = parseInt(localStorage.getItem("streak") || "0");

    if (lastVisit !== today) {
      if (new Date(lastVisit).getTime() === new Date(new Date().setDate(new Date().getDate() - 1)).getTime()) {
        streak += 1;
      } else {
        streak = 1;
      }
      localStorage.setItem("lastVisit", today);
      localStorage.setItem("streak", streak);
    }

    document.getElementById("streak").innerText = streak;
  </script></body>
</html><!DOCTYPE html><html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Danton Christian Association</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <script src="https://www.gstatic.com/firebasejs/9.6.10/firebase-app-compat.js"></script>
  <script src="https://www.gstatic.com/firebasejs/9.6.10/firebase-auth-compat.js"></script>
</head>
<body class="bg-gray-100 text-gray-800">
  <!-- Navbar with Logo -->
  <header class="bg-blue-800 text-white p-4 flex justify-between items-center">
    <div class="flex items-center space-x-2">
      <img src="https://chat.openai.com/cdn-cgi/image/width=256,quality=100/https://files.oaiusercontent.com/file-XFk6SKSpN4SFaM6EBv1nJ3ZK?se=2025-07-26T21%3A13%3A23Z&sp=r&sv=2021-08-06&sr=b&sig=1QeQXwtm%2BWJWe6hRxguOCz7v3egMCbIkEsDf1oaAgSg%3D" alt="DCA Logo" class="w-10 h-10">
      <h1 class="text-xl font-bold">Danton Christian Association</h1>
    </div>
    <nav class="space-x-4">
      <a href="#" class="hover:underline">Home</a>
      <a href="#bible" class="hover:underline">Bible</a>
      <a href="#prayer" class="hover:underline">Prayer</a>
      <a href="#videos" class="hover:underline">Videos</a>
      <a href="#guides" class="hover:underline">Guides</a>
      <a href="#kids" class="hover:underline">Kids</a>
      <a href="#login" class="hover:underline">Login</a>
    </nav>
  </header>  <main class="p-6 space-y-6">
    <!-- Login Section -->
    <section id="login" class="bg-white p-4 rounded shadow">
      <h2 class="text-xl font-semibold mb-2">🔐 Login / Sign Up</h2>
      <input id="email" type="email" placeholder="Email" class="border p-2 w-full mb-2">
      <input id="password" type="password" placeholder="Password" class="border p-2 w-full mb-2">
      <div class="flex gap-2">
        <button onclick="login()" class="bg-blue-600 text-white px-4 py-2 rounded">Login</button>
        <button onclick="signup()" class="bg-green-600 text-white px-4 py-2 rounded">Sign Up</button>
        <button onclick="logout()" class="bg-red-600 text-white px-4 py-2 rounded">Logout</button>
      </div>
      <p id="authStatus" class="mt-2 text-sm text-green-600"></p>
    </section><!-- Other sections (Daily Verse, Streak, End Signs, etc.) -->
<section class="bg-white p-4 rounded shadow">
  <h2 class="text-xl font-semibold mb-2">📖 Daily Bible Verse</h2>
  <p id="dailyVerse">Loading verse...</p>
</section>

<section class="bg-white p-4 rounded shadow">
  <h2 class="text-xl font-semibold mb-2">🔥 Your Visit Streak</h2>
  <p>You have visited this site <span id="streak">0</span> day(s) in a row.</p>
</section>

<section id="videos" class="bg-white p-4 rounded shadow">
  <h2 class="text-xl font-semibold mb-2">🎥 Gospel Videos</h2>
  <iframe width="100%" height="315" src="https://www.youtube.com/embed/sz81dIfwf4Y" frameborder="0" allowfullscreen></iframe>
</section>

<section id="bible" class="bg-white p-4 rounded shadow">
  <h2 class="text-xl font-semibold mb-2">📚 Bible Chapters</h2>
  <a class="text-blue-600 underline" href="https://www.biblegateway.com/" target="_blank">Read Bible on BibleGateway</a>
</section>

  </main>  <footer class="bg-blue-800 text-white text-center p-4 mt-6">
    <p>&copy; 2025 Danton Christian Association. Publisher: Dantez482 (Danton Mariga)</p>
  </footer>  <script>
    // Firebase config
    const firebaseConfig = {
      apiKey: "YOUR_API_KEY",
      authDomain: "YOUR_PROJECT.firebaseapp.com",
      projectId: "YOUR_PROJECT",
      storageBucket: "YOUR_PROJECT.appspot.com",
      messagingSenderId: "YOUR_SENDER_ID",
      appId: "YOUR_APP_ID"
    };
    firebase.initializeApp(firebaseConfig);
    const auth = firebase.auth();

    function login() {
      const email = document.getElementById("email").value;
      const password = document.getElementById("password").value;
      auth.signInWithEmailAndPassword(email, password)
        .then(() => {
          document.getElementById("authStatus").innerText = "Logged in successfully!";
        })
        .catch(error => alert(error.message));
    }

    function signup() {
      const email = document.getElementById("email").value;
      const password = document.getElementById("password").value;
      auth.createUserWithEmailAndPassword(email, password)
        .then(() => {
          document.getElementById("authStatus").innerText = "Account created successfully!";
        })
        .catch(error => alert(error.message));
    }

    function logout() {
      auth.signOut().then(() => {
        document.getElementById("authStatus").innerText = "Logged out.";
      });
    }

    // Daily Verse
    fetch("https://beta.ourmanna.com/api/v1/get/?format=text")
      .then(response => response.text())
      .then(data => {
        document.getElementById("dailyVerse").innerText = data;
      })
      .catch(() => {
        document.getElementById("dailyVerse").innerText = "Could not load verse. Please try again later.";
      });

    // Streak Tracker
    const today = new Date().toDateString();
    const lastVisit = localStorage.getItem("lastVisit") || "";
    let streak = parseInt(localStorage.getItem("streak") || "0");

    if (lastVisit !== today) {
      if (new Date(lastVisit).getTime() === new Date(new Date().setDate(new Date().getDate() - 1)).getTime()) {
        streak += 1;
      } else {
        streak = 1;
      }
      localStorage.setItem("lastVisit", today);
      localStorage.setItem("streak", streak);
    }

    document.getElementById("streak").innerText = streak;
  </script></body>
</html>
