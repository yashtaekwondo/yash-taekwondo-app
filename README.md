<!doctype html>
<html lang="hi">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Yash Taekwondo Academy</title>
    <style>
      * {
        box-sizing: border-box;
        font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
        margin: 0;
        padding: 0;
      }
      body {
        background-color: #f0f2f5;
        color: #333;
        position: relative;
        min-height: 100vh;
      }

      /* Background Logo / Watermark */
      body::before {
        content: "";
        position: fixed;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        width: 300px;
        height: 300px;
        background-image: url("
        https://via.placeholder.com/300?text=TKD+Logo");
        background-repeat: no-repeat;
        background-position: center;
        background-size: contain;
        opacity: 0.04;
        z-index: -1;
        pointer-events: none;
      }

      /* TOP NAVIGATION BAR */
      .navbar {
        background: #b52b27;
        display: flex;
        justify-content: space-between;
        align-items: center;
        padding: 0 20px;
        position: sticky;
        top: 0;
        z-index: 1000;
        box-shadow: 0 2px 10px rgba(0, 0, 0, 0.2);
      }
      .nav-brand {
        display: flex;
        align-items: center;
        gap: 10px;
        color: white;
        padding: 10px 0;
      }
      .nav-brand img {
        width: 45px;
        height: 45px;
        border-radius: 50%;
        background: white;
      }
      .nav-brand h2 {
        font-size: 18px;
      }

      .menu-toggle {
        display: none;
        font-size: 24px;
        color: white;
        background: none;
        border: none;
        cursor: pointer;
        padding: 5px;
      }

      .nav-menu {
        display: flex;
        list-style: none;
        flex-wrap: wrap;
      }
      .nav-menu li a {
        display: block;
        color: white;
        text-decoration: none;
        padding: 15px 10px;
        font-size: 13px;
        font-weight: 600;
        transition: background 0.3s;
      }
      .nav-menu li a:hover,
      .nav-menu li a.active-link {
        background: #d9534f;
      }

      .container {
        max-width: 1200px;
        margin: 20px auto;
        padding: 0 15px;
      }

      /* HERO IMAGE SLIDER */
      .slider-container {
        position: relative;
        max-width: 1200px;
        margin: 0 auto 20px auto;
        height: 350px;
        overflow: hidden;
        border-radius: 10px;
        box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
        background: #000;
      }
      .slide {
        display: none;
        position: absolute;
        width: 100%;
        height: 100%;
      }
      .slide.active {
        display: block;
      }
      .slide img {
        width: 100%;
        height: 100%;
        object-fit: cover;
      }
      .slide-caption {
        position: absolute;
        bottom: 0;
        background: rgba(0, 0, 0, 0.65);
        color: white;
        width: 100%;
        padding: 15px 20px;
        font-size: 18px;
        font-weight: bold;
      }
      .prev,
      .next {
        cursor: pointer;
        position: absolute;
        top: 50%;
        transform: translateY(-50%);
        padding: 12px 16px;
        color: white;
        font-weight: bold;
        font-size: 18px;
        transition: 0.3s;
        background-color: rgba(0, 0, 0, 0.4);
        border-radius: 0 3px 3px 0;
        user-select: none;
      }
      .next {
        right: 0;
        border-radius: 3px 0 0 3px;
      }
      .prev:hover,
      .next:hover {
        background-color: rgba(0, 0, 0, 0.8);
      }
      .dots-container {
        position: absolute;
        bottom: 10px;
        right: 20px;
        display: flex;
        gap: 5px;
      }
      .dot {
        cursor: pointer;
        height: 12px;
        width: 12px;
        background-color: #bbb;
        border-radius: 50%;
        display: inline-block;
        transition: background-color 0.6s ease;
      }
      .dot.active,
      .dot:hover {
        background-color: #d9534f;
      }

      /* Header inside Portal Views */
      .app-header {
        background: linear-gradient(135deg, #d9534f, #b52b27);
        color: white;
        padding: 15px 20px;
        text-align: center;
        border-radius: 10px;
        margin-bottom: 20px;
        position: relative;
        display: flex;
        align-items: center;
        justify-content: center;
      }
      .logout-btn {
        position: absolute;
        right: 20px;
        background: rgba(255, 255, 255, 0.2);
        color: white;
        border: 1px solid white;
        padding: 6px 12px;
        border-radius: 5px;
        cursor: pointer;
      }
      .logout-btn:hover {
        background: white;
        color: #d9534f;
      }

      /* Auth Card */
      .auth-container {
        max-width: 400px;
        margin: 30px auto;
        background: white;
        padding: 30px;
        border-radius: 10px;
        box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
        text-align: center;
      }
      .auth-container h2 {
        margin-bottom: 20px;
        color: #d9534f;
      }
      .auth-tabs {
        display: flex;
        margin-bottom: 20px;
        border-bottom: 2px solid #ddd;
      }
      .auth-tab {
        flex: 1;
        padding: 10px;
        cursor: pointer;
        font-weight: bold;
        color: #666;
      }
      .auth-tab.active {
        color: #d9534f;
        border-bottom: 3px solid #d9534f;
        margin-bottom: -2px;
      }

      /* Content Sections */
      .content-section {
        background: white;
        padding: 25px;
        border-radius: 8px;
        box-shadow: 0 2px 5px rgba(0, 0, 0, 0.08);
        margin-bottom: 20px;
      }
      .content-section h2 {
        color: #d9534f;
        margin-bottom: 15px;
        border-bottom: 2px solid #f0f2f5;
        padding-bottom: 8px;
      }

      /* Dashboard UI */
      .dashboard {
        display: grid;
        grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
        gap: 15px;
        margin-bottom: 20px;
      }
      .card {
        background: white;
        padding: 15px;
        border-radius: 8px;
        text-align: center;
        box-shadow: 0 2px 5px rgba(0, 0, 0, 0.08);
        border-left: 4px solid #d9534f;
      }
      .card h3 {
        font-size: 13px;
        color: #666;
        margin-bottom: 5px;
      }
      .card p {
        font-size: 22px;
        font-weight: bold;
        color: #333;
      }

      .section-header {
        display: flex;
        justify-content: space-between;
        align-items: center;
        border-bottom: 2px solid #f0f2f5;
        padding-bottom: 10px;
        margin-bottom: 15px;
        flex-wrap: wrap;
        gap: 10px;
      }

      input,
      select,
      button,
      textarea {
        width: 100%;
        padding: 10px;
        border: 1px solid #ccc;
        border-radius: 5px;
        font-size: 14px;
        margin-bottom: 10px;
      }
      button {
        background: #d9534f;
        color: white;
        border: none;
        cursor: pointer;
        font-weight: bold;
      }
      button:hover {
        background: #c9302c;
      }

      .filter-bar {
        display: flex;
        gap: 15px;
        background: #e9ecef;
        padding: 12px;
        border-radius: 8px;
        margin-bottom: 15px;
        flex-wrap: wrap;
        align-items: center;
      }
      .filter-bar label {
        font-weight: bold;
        font-size: 14px;
      }
      .filter-bar select {
        width: auto;
        margin-bottom: 0;
      }

      table {
        width: 100%;
        border-collapse: collapse;
        margin-top: 10px;
        font-size: 13px;
      }
      th,
      td {
        padding: 10px;
        border: 1px solid #e0e0e0;
        text-align: left;
      }
      th {
        background-color: #f8f9fa;
        color: #555;
      }

      .badge {
        padding: 4px 8px;
        border-radius: 4px;
        font-size: 11px;
        color: white;
        font-weight: bold;
        display: inline-block;
      }
      .badge-paid {
        background-color: #007bff;
      }
      .badge-pending {
        background-color: #ffc107;
        color: #333;
      }
      .badge-gold {
        background-color: #ffd700;
        color: #000;
      }
      .badge-silver {
        background-color: #c0c0c0;
        color: #000;
      }
      .badge-bronze {
        background-color: #cd7f32;
        color: #fff;
      }
      .badge-part {
        background-color: #17a2b8;
        color: #fff;
      }

      .btn-sm {
        padding: 5px 8px;
        font-size: 11px;
        margin-right: 3px;
        width: auto;
        display: inline-block;
      }
      .btn-green {
        background-color: #28a745;
      }
      .btn-orange {
        background-color: #dc3545;
      }
      .btn-blue {
        background-color: #007bff;
      }
      .btn-dark {
        background-color: #343a40;
      }
      .btn-excel {
        background-color: #1d6f42;
        width: auto;
        padding: 8px 15px;
        margin-bottom: 0;
      }
      .btn-excel:hover {
        background-color: #155231;
      }

      .hidden {
        display: none !important;
      }

      .profile-card {
        background: #f8f9fa;
        border: 1px solid #ddd;
        padding: 15px;
        border-radius: 8px;
        margin-bottom: 15px;
        display: flex;
        gap: 20px;
        align-items: center;
        flex-wrap: wrap;
      }
      .profile-card img {
        width: 100px;
        height: 100px;
        border-radius: 50%;
        object-fit: cover;
        border: 3px solid #d9534f;
      }
      .profile-info {
        flex: 1;
        min-width: 200px;
      }
      .profile-card h3 {
        color: #d9534f;
        margin-bottom: 10px;
      }
      .profile-grid {
        display: grid;
        grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
        gap: 10px;
        font-size: 14px;
      }

      .student-cell {
        display: flex;
        align-items: center;
        gap: 10px;
      }
      .student-thumb {
        width: 45px;
        height: 45px;
        border-radius: 50%;
        object-fit: cover;
        border: 1px solid #ccc;
      }

      .gallery-grid {
        display: grid;
        grid-template-columns: repeat(auto-fill, minmax(180px, 1fr));
        gap: 15px;
      }
      .gallery-grid img {
        width: 100%;
        height: 150px;
        object-fit: cover;
        border-radius: 8px;
      }

      /* CMS Nav Pills */
      .cms-nav {
        display: flex;
        gap: 8px;
        overflow-x: auto;
        padding-bottom: 10px;
        margin-bottom: 15px;
        border-bottom: 1px solid #eee;
      }
      .cms-pill {
        padding: 6px 12px;
        background: #e9ecef;
        border-radius: 20px;
        font-size: 12px;
        font-weight: bold;
        cursor: pointer;
        white-space: nowrap;
      }
      .cms-pill.active {
        background: #d9534f;
        color: white;
      }

      .admin-slider-grid {
        display: grid;
        grid-template-columns: repeat(auto-fill, minmax(150px, 1fr));
        gap: 10px;
        margin-top: 15px;
      }
      .admin-slider-item {
        border: 1px solid #ddd;
        border-radius: 5px;
        padding: 5px;
        background: #f9f9f9;
        text-align: center;
      }
      .admin-slider-item img {
        width: 100%;
        height: 80px;
        object-fit: cover;
        border-radius: 3px;
      }

      /* RESPONSIVE MEDIA QUERIES */
      @media (max-width: 768px) {
        .menu-toggle {
          display: block;
        }
        .nav-menu {
          display: none;
          width: 100%;
          flex-direction: column;
          background: #b52b27;
          border-top: 1px solid rgba(255, 255, 255, 0.1);
        }
        .nav-menu.show {
          display: flex;
        }
        .nav-menu li a {
          padding: 12px 15px;
          border-bottom: 1px solid rgba(255, 255, 255, 0.05);
        }
        .slider-container {
          height: 220px;
        }
        .slide-caption {
          font-size: 14px;
          padding: 8px 12px;
        }
        .app-header h1 {
          font-size: 18px !important;
        }
        .logout-btn {
          position: static;
          margin-top: 10px;
        }
        .app-header {
          flex-direction: column;
        }
      }
    </style>
  </head>
  <body>
    <!-- TOP NAVIGATION BAR -->
    <nav class="navbar">
      <div class="nav-brand">
        <img src="C:\Users\Siraj\OneDrive\Desktop\HP\yta logo.jpg" alt="Logo" />
        <h2>Yash Taekwondo</h2>
      </div>
      <button class="menu-toggle" onclick="toggleMenu()">☰</button>
      <ul class="nav-menu" id="navMenu">
        <li>
          <a
            href="#"
            onclick="showSection('home')"
            id="link-home"
            class="active-link"
            >Home Page</a
          >
        </li>
        <li><a href="#" onclick="showSection('about')">About Us</a></li>
        <li><a href="#" onclick="showSection('branches')">Our Branches</a></li>
        <li><a href="#" onclick="showSection('players')">Players</a></li>
        <li><a href="#" onclick="showSection('events')">Events</a></li>
        <li><a href="#" onclick="showSection('circulars')">Circulars</a></li>
        <li><a href="#" onclick="showSection('media')">Media</a></li>
        <li><a href="#" onclick="showSection('contact')">Contact Us</a></li>
        <!-- NEW OPTION ADDED BELOW -->
        <li>
          <a href="#" onclick="showSection('champ')" style="color: #ffd700"
            >Champ Management Soft</a
          >
        </li>
        <li><a href="#" onclick="showSection('login')">Login Panel</a></li>
      </ul>
    </nav>

    <!-- DYNAMIC HERO IMAGE SLIDER -->
    <div class="slider-container" id="sliderWrapper">
      <a class="prev" onclick="changeSlide(-1)">&#10094;</a>
      <a class="next" onclick="changeSlide(1)">&#10095;</a>
      <div class="dots-container" id="dotsWrapper"></div>
    </div>

    <!-- MAIN CONTAINER -->
    <div class="container">
      <!-- PUBLIC SECTIONS -->
      <div id="sec-home" class="content-section">
        <h2>Welcome to Yash Taekwondo Academy</h2>
        <p>
          Aapka swagat hai Yash Taekwondo Academy me! Yahan bacho ko martial
          arts, self-defense, aur fitness ki aadhunik training di jaati hai.
        </p>
      </div>

      <div id="sec-about" class="content-section hidden">
        <h2 id="view-about-title">About Us</h2>
        <p id="view-about-desc">
          Yash Taekwondo Academy ek premier institute hai jo disciplined
          athletes tayar karne ke liye dedicated hai.
        </p>
      </div>

      <div id="sec-branches" class="content-section hidden">
        <h2>Our Branches</h2>
        <ul
          id="view-branches-list"
          style="margin-left: 20px; line-height: 1.8"
        ></ul>
      </div>

      <div id="sec-players" class="content-section hidden">
        <h2>Star Players</h2>
        <div id="view-players-list" class="gallery-grid"></div>
      </div>

      <div id="sec-events" class="content-section hidden">
        <h2>Upcoming Events</h2>
        <div id="view-events-list"></div>
      </div>

      <div id="sec-circulars" class="content-section hidden">
        <h2>Official Circulars</h2>
        <div id="view-circulars-list"></div>
      </div>

      <div id="sec-media" class="content-section hidden">
        <h2>Media & Photo Gallery</h2>
        <div id="view-media-list" class="gallery-grid"></div>
      </div>

      <div id="sec-contact" class="content-section hidden">
        <h2>Contact Us</h2>
        <p>
          📞 <strong>Phone:</strong>
          <span id="view-contact-phone">+91 9876543210</span>
        </p>
        <p>
          ✉️ <strong>Email:</strong>
          <span id="view-contact-email">info@yashtaekwondo.com</span>
        </p>
        <p>
          📍 <strong>Address:</strong>
          <span id="view-contact-address"
            >Yash Taekwondo Main Centre, India</span
          >
        </p>
      </div>

      <!-- NEW SECTION: CHAMP MANAGEMENT SOFT PAGE -->
      <div id="sec-champ" class="content-section hidden">
        <h2>🏆 Champ Management Software</h2>
        <p id="view-champ-desc">
          Welcome to Champ Management Soft portal. Yahan se championship,
          tournament scoring aur athlete management tools access karein.
        </p>

        <div
          style="
            margin-top: 20px;
            background: #fff8e7;
            padding: 20px;
            border-left: 4px solid #ffd700;
            border-radius: 5px;
          "
        >
          <h3 style="color: #b52b27; margin-bottom: 10px">
            🏆 Championship Management System
          </h3>
          <p style="font-size: 14px; margin-bottom: 15px">
            Championship scorecards, bout schedules, aur tournament registration
            module live hain.
          </p>
          <a
            id="view-champ-link"
            href="#"
            target="_blank"
            style="
              display: inline-block;
              background: #b52b27;
              color: white;
              padding: 10px 20px;
              text-decoration: none;
              font-weight: bold;
              border-radius: 5px;
            "
            >Launch Champ Soft Software 🚀</a
          >
        </div>
      </div>

      <!-- SECTION: LOGIN PANEL -->
      <div id="sec-login" class="hidden">
        <div id="authScreen" class="auth-container">
          <h2>🥋 Yash Taekwondo Portal Login</h2>
          <div class="auth-tabs">
            <div
              id="tabAdmin"
              class="auth-tab active"
              onclick="switchTab('admin')"
            >
              Admin Login
            </div>
            <div
              id="tabStudent"
              class="auth-tab"
              onclick="switchTab('student')"
            >
              Student Login
            </div>
          </div>

          <form id="adminLoginForm">
            <input
              type="text"
              id="adminUser"
              placeholder="Admin Username"
              required
            />
            <input
              type="password"
              id="adminPass"
              placeholder="Password"
              required
            />
            <button type="submit">Login as Admin</button>
          </form>

          <form id="studentLoginForm" class="hidden">
            <input
              type="tel"
              id="studentMobileLogin"
              placeholder="Registered Mobile Number"
              required
            />
            <button type="submit">Login as Student</button>
          </form>
        </div>

        <!-- MAIN APP DASHBOARD SCREEN -->
        <div id="appScreen" class="hidden">
          <div class="app-header">
            <div>
              <h1 style="font-size: 22px">🥋 Yash Taekwondo Academy Portal</h1>
              <p id="roleTitle">Management System</p>
            </div>
            <button class="logout-btn" onclick="logout()">Logout</button>
          </div>

          <!-- ADMIN VIEW -->
          <div id="adminView" class="hidden">
            <div class="dashboard">
              <div class="card">
                <h3>Total Students</h3>
                <p id="statTotal">0</p>
              </div>
              <div class="card">
                <h3>Selected Month Present</h3>
                <p id="statPresent">0</p>
              </div>
              <div class="card">
                <h3>Selected Month Paid</h3>
                <p id="statPaid">0</p>
              </div>
              <div class="card">
                <h3>Selected Month Pending</h3>
                <p id="statPending">0</p>
              </div>
            </div>

            <!-- ADMIN CMS MANAGER -->
            <div class="content-section" style="border: 2px solid #d9534f">
              <h2>⚙️ Website Content Manager (Top Menu CMS)</h2>

              <div class="cms-nav">
                <span
                  class="cms-pill active"
                  onclick="switchCmsTab('cms-slider')"
                  >🖼️ Slider</span
                >
                <span class="cms-pill" onclick="switchCmsTab('cms-about')"
                  >ℹ️ About Us</span
                >
                <span class="cms-pill" onclick="switchCmsTab('cms-branches')"
                  >🏢 Branches</span
                >
                <span class="cms-pill" onclick="switchCmsTab('cms-players')"
                  >⭐ Players</span
                >
                <span class="cms-pill" onclick="switchCmsTab('cms-events')"
                  >📅 Events</span
                >
                <span class="cms-pill" onclick="switchCmsTab('cms-circulars')"
                  >📄 Circulars</span
                >
                <span class="cms-pill" onclick="switchCmsTab('cms-media')"
                  >📸 Media</span
                >
                <span class="cms-pill" onclick="switchCmsTab('cms-contact')"
                  >📞 Contact</span
                >
                <span class="cms-pill" onclick="switchCmsTab('cms-champ')"
                  >🏆 Champ Soft</span
                >
              </div>

              <!-- CMS: SLIDER -->
              <div id="cms-slider" class="cms-box">
                <h4>Manage Image Slider</h4>
                <form id="addSliderForm">
                  <div
                    style="
                      display: grid;
                      grid-template-columns: repeat(
                        auto-fit,
                        minmax(180px, 1fr)
                      );
                      gap: 10px;
                    "
                  >
                    <input
                      type="url"
                      id="sliderImgUrl"
                      placeholder="Image URL"
                      required
                    />
                    <input
                      type="text"
                      id="sliderCaption"
                      placeholder="Caption"
                      required
                    />
                    <button type="submit" style="background: #28a745">
                      Add Slide
                    </button>
                  </div>
                </form>
                <div id="adminSliderList" class="admin-slider-grid"></div>
              </div>

              <!-- CMS: ABOUT US -->
              <div id="cms-about" class="cms-box hidden">
                <h4>Manage About Us</h4>
                <form id="aboutForm">
                  <input
                    type="text"
                    id="aboutTitleInput"
                    placeholder="Section Title"
                    required
                  />
                  <textarea
                    id="aboutDescInput"
                    rows="3"
                    placeholder="About Details..."
                    required
                  ></textarea>
                  <button type="submit">Update About Us</button>
                </form>
              </div>

              <!-- CMS: BRANCHES -->
              <div id="cms-branches" class="cms-box hidden">
                <h4>Add New Branch</h4>
                <form id="branchForm">
                  <input
                    type="text"
                    id="branchNameInput"
                    placeholder="Branch Name / Location"
                    required
                  />
                  <button type="submit" style="background: #28a745">
                    Add Branch
                  </button>
                </form>
                <div id="adminBranchList" style="margin-top: 10px"></div>
              </div>

              <!-- CMS: PLAYERS -->
              <div id="cms-players" class="cms-box hidden">
                <h4>Add Star Player</h4>
                <form id="playerForm">
                  <input
                    type="text"
                    id="playerNameInput"
                    placeholder="Player Name"
                    required
                  />
                  <input
                    type="text"
                    id="playerRankInput"
                    placeholder="Achievement/Rank (e.g. Gold Medalist)"
                    required
                  />
                  <input
                    type="url"
                    id="playerImgInput"
                    placeholder="Photo URL"
                    required
                  />
                  <button type="submit" style="background: #28a745">
                    Add Player
                  </button>
                </form>
                <div
                  id="adminPlayerList"
                  class="gallery-grid"
                  style="margin-top: 10px"
                ></div>
              </div>

              <!-- CMS: EVENTS -->
              <div id="cms-events" class="cms-box hidden">
                <h4>Add Event</h4>
                <form id="eventForm">
                  <input
                    type="text"
                    id="eventNameInput"
                    placeholder="Event Name"
                    required
                  />
                  <input type="date" id="eventDateInput" required />
                  <textarea
                    id="eventDescInput"
                    placeholder="Event Details"
                    rows="2"
                    required
                  ></textarea>
                  <button type="submit" style="background: #28a745">
                    Add Event
                  </button>
                </form>
                <div id="adminEventList" style="margin-top: 10px"></div>
              </div>

              <!-- CMS: CIRCULARS -->
              <div id="cms-circulars" class="cms-box hidden">
                <h4>Add Circular / Notice</h4>
                <form id="circularForm">
                  <input
                    type="text"
                    id="circTitleInput"
                    placeholder="Notice Title"
                    required
                  />
                  <textarea
                    id="circDescInput"
                    placeholder="Notice Content"
                    rows="2"
                    required
                  ></textarea>
                  <button type="submit" style="background: #28a745">
                    Publish Circular
                  </button>
                </form>
                <div id="adminCircularList" style="margin-top: 10px"></div>
              </div>

              <!-- CMS: MEDIA -->
              <div id="cms-media" class="cms-box hidden">
                <h4>Add Gallery Photo</h4>
                <form id="mediaForm">
                  <input
                    type="url"
                    id="mediaUrlInput"
                    placeholder="Photo URL"
                    required
                  />
                  <button type="submit" style="background: #28a745">
                    Add Photo
                  </button>
                </form>
                <div
                  id="adminMediaList"
                  class="gallery-grid"
                  style="margin-top: 10px"
                ></div>
              </div>

              <!-- CMS: CONTACT -->
              <div id="cms-contact" class="cms-box hidden">
                <h4>Update Contact Details</h4>
                <form id="contactForm">
                  <input
                    type="text"
                    id="contactPhoneInput"
                    placeholder="Phone Number"
                    required
                  />
                  <input
                    type="email"
                    id="contactEmailInput"
                    placeholder="Email Address"
                    required
                  />
                  <textarea
                    id="contactAddressInput"
                    placeholder="Full Address"
                    rows="2"
                    required
                  ></textarea>
                  <button type="submit">Save Contact Details</button>
                </form>
              </div>

              <!-- CMS: CHAMP MANAGEMENT SOFT -->
              <div id="cms-champ" class="cms-box hidden">
                <h4>Update Champ Management Soft Link/Info</h4>
                <form id="champForm">
                  <textarea
                    id="champDescInput"
                    rows="2"
                    placeholder="Software Description"
                    required
                  ></textarea>
                  <input
                    type="url"
                    id="champLinkInput"
                    placeholder="Software External Link (e.g. https://...)"
                    required
                  />
                  <button type="submit">Save Champ Soft Settings</button>
                </form>
              </div>
            </div>

            <!-- New Student Form -->
            <div class="content-section">
              <h2 style="color: #333">➕ New Student Registration</h2>
              <form id="addStudentForm">
                <div
                  style="
                    display: grid;
                    grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
                    gap: 10px;
                  "
                >
                  <input
                    type="text"
                    id="sName"
                    placeholder="Full Name"
                    required
                  />
                  <input type="date" id="sDob" title="Date of Birth" required />
                  <input
                    type="tel"
                    id="sMobile"
                    placeholder="Mobile Number"
                    required
                  />
                  <select id="sBelt" required>
                    <option value="">Present Belt Rank</option>
                    <option value="White Belt">White Belt</option>
                    <option value="Yellow Belt">Yellow Belt</option>
                    <option value="Green Belt">Green Belt</option>
                    <option value="Green One Belt">Green One Belt</option>
                    <option value="Blue Belt">Blue Belt</option>
                    <option value="Blue One Belt">Blue One Belt</option>
                    <option value="Red Belt">Red Belt</option>
                    <option value="Red One Belt">Red One Belt</option>
                    <option value="1st Dan Black Belt">
                      Black Belt 1st Dan
                    </option>
                    <option value="Black Belt">Black Belt 2nd Dan</option>
                  </select>
                  <input
                    type="date"
                    id="sDoj"
                    title="Date of Joining"
                    required
                  />
                  <select id="sBatch" required>
                    <option value="">Batch Timing</option>
                    <option value="Morning">Morning Batch</option>
                    <option value="Evening">Evening Batch</option>
                  </select>
                  <div>
                    <label
                      style="
                        font-size: 12px;
                        color: #666;
                        display: block;
                        margin-bottom: 2px;
                      "
                      >Upload Photo:</label
                    >
                    <input type="file" id="sPhoto" accept="image/*" />
                  </div>
                </div>

                <div
                  style="
                    margin-top: 10px;
                    background: #f9f9f9;
                    padding: 10px;
                    border-radius: 5px;
                    border: 1px solid #eee;
                  "
                >
                  <label style="font-size: 13px; font-weight: bold; color: #555"
                    >🏆 Tournament / Medal Record (Optional):</label
                  >
                  <div
                    style="
                      display: grid;
                      grid-template-columns: repeat(
                        auto-fit,
                        minmax(150px, 1fr)
                      );
                      gap: 10px;
                      margin-top: 5px;
                    "
                  >
                    <input
                      type="text"
                      id="sTourName"
                      placeholder="Tournament Name"
                    />
                    <select id="sMedal">
                      <option value="">Medal / Status</option>
                      <option value="Gold Medal">🥇 Gold Medal</option>
                      <option value="Silver Medal">🥈 Silver Medal</option>
                      <option value="Bronze Medal">🥉 Bronze Medal</option>
                      <option value="Participated">🎗 Participated</option>
                    </select>
                    <input
                      type="number"
                      id="sTourYear"
                      placeholder="Year (e.g. 2026)"
                    />
                  </div>
                </div>

                <textarea
                  id="sAddress"
                  placeholder="Full Address"
                  rows="2"
                  style="margin-top: 10px"
                  required
                ></textarea>
                <button type="submit">Save Student Details</button>
              </form>
            </div>

            <!-- Student Directory Table -->
            <div class="content-section">
              <div class="section-header">
                <h2 style="color: #333">📋 Student Directory & Logs</h2>
                <button class="btn-excel" onclick="exportToExcel()">
                  📥 Export to Excel
                </button>
              </div>

              <div class="filter-bar">
                <label>Month Select Karein:</label>
                <select id="filterMonth" onchange="renderAdminData()">
                  <option value="01">January</option>
                  <option value="02">February</option>
                  <option value="03">March</option>
                  <option value="04">April</option>
                  <option value="05">May</option>
                  <option value="06">June</option>
                  <option value="07">July</option>
                  <option value="08">August</option>
                  <option value="09">September</option>
                  <option value="10">October</option>
                  <option value="11">November</option>
                  <option value="12">December</option>
                </select>

                <label> Select Year:</label>
                <select id="filterYear" onchange="renderAdminData()">
                  <option value="2024">2024</option>
                  <option value="2025">2025</option>
                  <option value="2026" selected>2026</option>
                  <option value="2027">2027</option>
                </select>
              </div>

              <div style="overflow-x: auto">
                <table>
                  <thead>
                    <tr>
                      <th>Student Details</th>
                      <th>DOB / Joining</th>
                      <th>Belt & Batch</th>
                      <th>Tournament Record</th>
                      <th>Address</th>
                      <th>Monthly Fee Status</th>
                      <th>Attendance (Selected Month)</th>
                      <th>Actions</th>
                    </tr>
                  </thead>
                  <tbody id="studentTableBody"></tbody>
                </table>
              </div>
            </div>
          </div>

          <!-- STUDENT VIEW -->
          <div id="studentView" class="hidden">
            <div class="content-section">
              <h2 style="color: #333">👤 My Profile Details</h2>
              <div class="profile-card">
                <img id="stProfileImg" src="" alt="Profile Photo" />
                <div class="profile-info">
                  <h3 id="stProfileName">Name</h3>
                  <div class="profile-grid">
                    <p>
                      <strong>Mobile:</strong>
                      <span id="stProfileMobile"></span>
                    </p>
                    <p>
                      <strong>Date of Birth:</strong>
                      <span id="stProfileDob"></span>
                    </p>
                    <p>
                      <strong>Current Belt:</strong>
                      <span id="stProfileBelt"></span>
                    </p>
                    <p>
                      <strong>Date of Joining:</strong>
                      <span id="stProfileDoj"></span>
                    </p>
                    <p>
                      <strong>Batch:</strong> <span id="stProfileBatch"></span>
                    </p>
                    <p>
                      <strong>Address:</strong>
                      <span id="stProfileAddress"></span>
                    </p>
                  </div>
                  <div
                    style="
                      margin-top: 10px;
                      background: #fff;
                      padding: 8px;
                      border: 1px dashed #ccc;
                      border-radius: 5px;
                    "
                  >
                    <strong>🏆 Tournament Record:</strong>
                    <span id="stProfileTournament">N/A</span>
                  </div>
                </div>
              </div>
            </div>

            <div class="content-section">
              <h2 style="color: #333">📊 My Monthly Fee & Attendance Record</h2>
              <div class="filter-bar">
                <label>Select Year:</label>
                <select id="stFilterYear" onchange="renderStudentDashboard()">
                  <option value="2025">2025</option>
                  <option value="2026" selected>2026</option>
                </select>
              </div>

              <div style="overflow-x: auto">
                <table>
                  <thead>
                    <tr>
                      <th>Month</th>
                      <th>Fee Status</th>
                      <th>Attendance Count (Present)</th>
                    </tr>
                  </thead>
                  <tbody id="studentLogsBody"></tbody>
                </table>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <script>
      /* --- RESPONSIVE MENU TOGGLE --- */
      function toggleMenu() {
        document.getElementById("navMenu").classList.toggle("show");
      }

      function showSection(sectionId) {
        const sections = [
          "home",
          "about",
          "branches",
          "players",
          "events",
          "circulars",
          "media",
          "contact",
          "champ",
          "login",
        ];
        sections.forEach((sec) => {
          document.getElementById("sec-" + sec).classList.add("hidden");
        });
        document
          .querySelectorAll(".nav-menu li a")
          .forEach((a) => a.classList.remove("active-link"));
        document.getElementById("sec-" + sectionId).classList.remove("hidden");
        document.getElementById("navMenu").classList.remove("show");
      }

      /* --- CMS DATA STORAGE & RENDERING --- */
      let cmsData = JSON.parse(localStorage.getItem("yash_taekwondo_cms")) || {
        about: {
          title: "About Us",
          desc: "Yash Taekwondo Academy ek premier institute hai jo disciplined athletes tayar karne ke liye dedicated hai.",
        },
        branches: [
          "Central Sports Complex, Main City",
          "Stadium Road Academy, North Campus",
        ],
        players: [
          {
            name: "Rohan Sharma",
            rank: "Black Belt 1st Dan",
            img: "https://via.placeholder.com/150?text=Rohan",
          },
        ],
        events: [
          {
            name: "Annual Belt Exam",
            date: "2026-09-15",
            desc: "State level belt promotion exam.",
          },
        ],
        circulars: [
          {
            title: "New Timing Notice",
            desc: "Morning batches start from 6:00 AM in Summer.",
          },
        ],
        media: [
          "https://via.placeholder.com/300x200?text=Event+Photo+1",
          "https://via.placeholder.com/300x200?text=Tournament+Photo+2",
        ],
        contact: {
          phone: "+91 9876543210",
          email: "info@yashtaekwondo.com",
          address: "Yash Taekwondo Main Centre, India",
        },
        champ: {
          desc: "Welcome to Champ Management Soft portal. Yahan se championship, tournament scoring aur athlete management tools access karein.",
          link: "#",
        },
      };

      function saveCmsData() {
        localStorage.setItem("yash_taekwondo_cms", JSON.stringify(cmsData));
        renderPublicCms();
      }

      function renderPublicCms() {
        document.getElementById("view-about-title").innerText =
          cmsData.about.title;
        document.getElementById("view-about-desc").innerText =
          cmsData.about.desc;

        const bList = document.getElementById("view-branches-list");
        bList.innerHTML = cmsData.branches.map((b) => `<li>${b}</li>`).join("");

        const pList = document.getElementById("view-players-list");
        pList.innerHTML = cmsData.players
          .map(
            (p) => `
          <div style="border:1px solid #ddd; padding:10px; border-radius:5px; text-align:center;">
            <img src="${p.img}" style="width:100%; height:120px; object-fit:cover; border-radius:4px;">
            <strong style="display:block; margin-top:5px;">${p.name}</strong>
            <small>${p.rank}</small>
          </div>
        `,
          )
          .join("");

        const eList = document.getElementById("view-events-list");
        eList.innerHTML = cmsData.events
          .map(
            (e) => `
          <div style="background:#f9f9f9; padding:10px; margin-bottom:8px; border-left:3px solid #d9534f;">
            <strong>${e.name}</strong> (${e.date})
            <p style="font-size:13px; color:#666;">${e.desc}</p>
          </div>
        `,
          )
          .join("");

        const cList = document.getElementById("view-circulars-list");
        cList.innerHTML = cmsData.circulars
          .map(
            (c) => `
          <div style="background:#fff8e7; padding:10px; margin-bottom:8px; border:1px solid #ffeeba;">
            <strong>📄 ${c.title}</strong>
            <p style="font-size:13px;">${c.desc}</p>
          </div>
        `,
          )
          .join("");

        const mList = document.getElementById("view-media-list");
        mList.innerHTML = cmsData.media.map((m) => `<img src="${m}">`).join("");

        document.getElementById("view-contact-phone").innerText =
          cmsData.contact.phone;
        document.getElementById("view-contact-email").innerText =
          cmsData.contact.email;
        document.getElementById("view-contact-address").innerText =
          cmsData.contact.address;

        // Champ Soft Page Render
        if (cmsData.champ) {
          document.getElementById("view-champ-desc").innerText =
            cmsData.champ.desc || "";
          document.getElementById("view-champ-link").href =
            cmsData.champ.link || "#";
        }
      }

      function switchCmsTab(tabId) {
        document
          .querySelectorAll(".cms-pill")
          .forEach((p) => p.classList.remove("active"));
        document
          .querySelectorAll(".cms-box")
          .forEach((b) => b.classList.add("hidden"));

        event.target.classList.add("active");
        document.getElementById(tabId).classList.remove("hidden");
      }

      /* --- CMS ADMIN SUBMISSIONS --- */
      document
        .getElementById("aboutForm")
        .addEventListener("submit", function (e) {
          e.preventDefault();
          cmsData.about.title =
            document.getElementById("aboutTitleInput").value;
          cmsData.about.desc = document.getElementById("aboutDescInput").value;
          saveCmsData();
          alert("About Us updated!");
        });

      document
        .getElementById("branchForm")
        .addEventListener("submit", function (e) {
          e.preventDefault();
          cmsData.branches.push(
            document.getElementById("branchNameInput").value,
          );
          saveCmsData();
          renderAdminCmsLists();
          this.reset();
        });

      document
        .getElementById("playerForm")
        .addEventListener("submit", function (e) {
          e.preventDefault();
          cmsData.players.push({
            name: document.getElementById("playerNameInput").value,
            rank: document.getElementById("playerRankInput").value,
            img: document.getElementById("playerImgInput").value,
          });
          saveCmsData();
          renderAdminCmsLists();
          this.reset();
        });

      document
        .getElementById("eventForm")
        .addEventListener("submit", function (e) {
          e.preventDefault();
          cmsData.events.push({
            name: document.getElementById("eventNameInput").value,
            date: document.getElementById("eventDateInput").value,
            desc: document.getElementById("eventDescInput").value,
          });
          saveCmsData();
          renderAdminCmsLists();
          this.reset();
        });

      document
        .getElementById("circularForm")
        .addEventListener("submit", function (e) {
          e.preventDefault();
          cmsData.circulars.push({
            title: document.getElementById("circTitleInput").value,
            desc: document.getElementById("circDescInput").value,
          });
          saveCmsData();
          renderAdminCmsLists();
          this.reset();
        });

      document
        .getElementById("mediaForm")
        .addEventListener("submit", function (e) {
          e.preventDefault();
          cmsData.media.push(document.getElementById("mediaUrlInput").value);
          saveCmsData();
          renderAdminCmsLists();
          this.reset();
        });

      document
        .getElementById("contactForm")
        .addEventListener("submit", function (e) {
          e.preventDefault();
          cmsData.contact = {
            phone: document.getElementById("contactPhoneInput").value,
            email: document.getElementById("contactEmailInput").value,
            address: document.getElementById("contactAddressInput").value,
          };
          saveCmsData();
          alert("Contact Details Saved!");
        });

      document
        .getElementById("champForm")
        .addEventListener("submit", function (e) {
          e.preventDefault();
          cmsData.champ = {
            desc: document.getElementById("champDescInput").value,
            link: document.getElementById("champLinkInput").value,
          };
          saveCmsData();
          alert("Champ Soft details saved!");
        });

      function renderAdminCmsLists() {
        document.getElementById("aboutTitleInput").value = cmsData.about.title;
        document.getElementById("aboutDescInput").value = cmsData.about.desc;

        document.getElementById("contactPhoneInput").value =
          cmsData.contact.phone;
        document.getElementById("contactEmailInput").value =
          cmsData.contact.email;
        document.getElementById("contactAddressInput").value =
          cmsData.contact.address;

        if (cmsData.champ) {
          document.getElementById("champDescInput").value =
            cmsData.champ.desc || "";
          document.getElementById("champLinkInput").value =
            cmsData.champ.link || "";
        }

        // Branches
        document.getElementById("adminBranchList").innerHTML = cmsData.branches
          .map(
            (b, i) => `
          <div style="display:flex; justify-content:space-between; margin-bottom:5px; background:#f9f9f9; padding:5px;">
            <span>${b}</span> <button class="btn-sm btn-orange" onclick="deleteCmsItem('branches', ${i})">Delete</button>
          </div>
        `,
          )
          .join("");

        // Players
        document.getElementById("adminPlayerList").innerHTML = cmsData.players
          .map(
            (p, i) => `
          <div style="text-align:center; border:1px solid #ddd; padding:5px;">
            <img src="${p.img}" style="width:100%; height:60px; object-fit:cover;">
            <small>${p.name}</small><br>
            <button class="btn-sm btn-orange" onclick="deleteCmsItem('players', ${i})">Delete</button>
          </div>
        `,
          )
          .join("");

        // Events
        document.getElementById("adminEventList").innerHTML = cmsData.events
          .map(
            (e, i) => `
          <div style="display:flex; justify-content:space-between; margin-bottom:5px; background:#f9f9f9; padding:5px;">
            <span>${e.name} (${e.date})</span> <button class="btn-sm btn-orange" onclick="deleteCmsItem('events', ${i})">Delete</button>
          </div>
        `,
          )
          .join("");

        // Circulars
        document.getElementById("adminCircularList").innerHTML =
          cmsData.circulars
            .map(
              (c, i) => `
          <div style="display:flex; justify-content:space-between; margin-bottom:5px; background:#f9f9f9; padding:5px;">
            <span>${c.title}</span> <button class="btn-sm btn-orange" onclick="deleteCmsItem('circulars', ${i})">Delete</button>
          </div>
        `,
            )
            .join("");

        // Media
        document.getElementById("adminMediaList").innerHTML = cmsData.media
          .map(
            (m, i) => `
          <div style="text-align:center; border:1px solid #ddd; padding:5px;">
            <img src="${m}" style="width:100%; height:60px; object-fit:cover;">
            <button class="btn-sm btn-orange" onclick="deleteCmsItem('media', ${i})">Delete</button>
          </div>
        `,
          )
          .join("");
      }

      function deleteCmsItem(category, index) {
        cmsData[category].splice(index, 1);
        saveCmsData();
        renderAdminCmsLists();
      }

      /* --- SLIDER LOGIC --- */
      const defaultSlides = [
        {
          img: "https://via.placeholder.com/1200x350/d9534f/ffffff?text=Yash+Taekwondo+Academy",
          caption: "🥋 World Class Taekwondo Training",
        },
        {
          img: "https://via.placeholder.com/1200x350/b52b27/ffffff?text=National+Level+Championships",
          caption: "🏆 Our Champions in Action",
        },
      ];
      let sliderData =
        JSON.parse(localStorage.getItem("yash_taekwondo_slides")) ||
        defaultSlides;
      let slideIndex = 0;
      let slideTimer;

      function renderSlider() {
        const sliderWrapper = document.getElementById("sliderWrapper");
        sliderWrapper.innerHTML = `
          <a class="prev" onclick="changeSlide(-1)">&#10094;</a>
          <a class="next" onclick="changeSlide(1)">&#10095;</a>
          <div class="dots-container" id="dotsWrapper"></div>
        `;
        const dotsWrapper = document.getElementById("dotsWrapper");

        sliderData.forEach((slide, idx) => {
          const slideDiv = document.createElement("div");
          slideDiv.className = `slide ${idx === 0 ? "active" : ""}`;
          slideDiv.innerHTML = `<img src="${slide.img}"><div class="slide-caption">${slide.caption}</div>`;
          sliderWrapper.insertBefore(
            slideDiv,
            sliderWrapper.querySelector(".prev"),
          );

          const dot = document.createElement("span");
          dot.className = `dot ${idx === 0 ? "active" : ""}`;
          dot.onclick = () => currentSlide(idx);
          dotsWrapper.appendChild(dot);
        });
        slideIndex = 0;
        showSlides();
      }

      function showSlides() {
        let slides = document.getElementsByClassName("slide");
        let dots = document.getElementsByClassName("dot");
        if (slides.length === 0) return;
        for (let i = 0; i < slides.length; i++)
          slides[i].classList.remove("active");
        for (let i = 0; i < dots.length; i++)
          dots[i].classList.remove("active");
        slideIndex++;
        if (slideIndex > slides.length) slideIndex = 1;
        slides[slideIndex - 1].classList.add("active");
        if (dots[slideIndex - 1]) dots[slideIndex - 1].classList.add("active");
        clearTimeout(slideTimer);
        slideTimer = setTimeout(showSlides, 3000);
      }

      function changeSlide(n) {
        clearTimeout(slideTimer);
        slideIndex += n - 1;
        showSlides();
      }
      function currentSlide(n) {
        clearTimeout(slideTimer);
        slideIndex = n;
        showSlides();
      }

      document
        .getElementById("addSliderForm")
        .addEventListener("submit", function (e) {
          e.preventDefault();
          sliderData.push({
            img: document.getElementById("sliderImgUrl").value.trim(),
            caption: document.getElementById("sliderCaption").value.trim(),
          });
          localStorage.setItem(
            "yash_taekwondo_slides",
            JSON.stringify(sliderData),
          );
          this.reset();
          renderSlider();
          renderAdminSliderList();
        });

      function renderAdminSliderList() {
        document.getElementById("adminSliderList").innerHTML = sliderData
          .map(
            (s, idx) => `
          <div class="admin-slider-item">
            <img src="${s.img}">
            <small style="display:block; text-overflow:ellipsis; overflow:hidden; white-space:nowrap;">${s.caption}</small>
            <button class="btn-sm btn-orange" onclick="deleteSlide(${idx})">Delete</button>
          </div>
        `,
          )
          .join("");
      }

      function deleteSlide(index) {
        sliderData.splice(index, 1);
        localStorage.setItem(
          "yash_taekwondo_slides",
          JSON.stringify(sliderData),
        );
        renderSlider();
        renderAdminSliderList();
      }

      /* --- AUTH & STUDENT LOGIC --- */
      let students =
        JSON.parse(localStorage.getItem("yash_taekwondo_v2_students")) || [];
      let monthlyRecords =
        JSON.parse(localStorage.getItem("yash_taekwondo_v2_records")) || {};
      let currentLoggedInStudent = null;
      const defaultAvatar = "https://via.placeholder.com/100?text=No+Photo";

      const today = new Date();
      document.getElementById("filterMonth").value = String(
        today.getMonth() + 1,
      ).padStart(2, "0");
      document.getElementById("filterYear").value = today.getFullYear();

      function switchTab(type) {
        if (type === "admin") {
          document.getElementById("tabAdmin").classList.add("active");
          document.getElementById("tabStudent").classList.remove("active");
          document.getElementById("adminLoginForm").classList.remove("hidden");
          document.getElementById("studentLoginForm").classList.add("hidden");
        } else {
          document.getElementById("tabStudent").classList.add("active");
          document.getElementById("tabAdmin").classList.remove("active");
          document
            .getElementById("studentLoginForm")
            .classList.remove("hidden");
          document.getElementById("adminLoginForm").classList.add("hidden");
        }
      }

      document
        .getElementById("adminLoginForm")
        .addEventListener("submit", function (e) {
          e.preventDefault();
          if (
            document.getElementById("adminUser").value === "admin" &&
            document.getElementById("adminPass").value === "admin123"
          ) {
            showApp("admin");
          } else {
            alert("Invalid Admin Credentials!");
          }
        });

      document
        .getElementById("studentLoginForm")
        .addEventListener("submit", function (e) {
          e.preventDefault();
          const mob = document
            .getElementById("studentMobileLogin")
            .value.trim();
          const found = students.find((s) => s.mobile === mob);
          if (found) {
            currentLoggedInStudent = found;
            showApp("student");
          } else {
            alert("Mobile Number Not Registered!");
          }
        });

      function showApp(role) {
        document.getElementById("authScreen").classList.add("hidden");
        document.getElementById("appScreen").classList.remove("hidden");
        if (role === "admin") {
          document.getElementById("adminView").classList.remove("hidden");
          document.getElementById("studentView").classList.add("hidden");
          document.getElementById("roleTitle").innerText =
            "Admin / Coach Portal";
          renderAdminData();
          renderAdminSliderList();
          renderAdminCmsLists();
        } else {
          document.getElementById("studentView").classList.remove("hidden");
          document.getElementById("adminView").classList.add("hidden");
          document.getElementById("roleTitle").innerText = "Student Portal";
          renderStudentDashboard();
        }
      }

      function logout() {
        document.getElementById("appScreen").classList.add("hidden");
        document.getElementById("authScreen").classList.remove("hidden");
        currentLoggedInStudent = null;
      }

      document
        .getElementById("addStudentForm")
        .addEventListener("submit", function (e) {
          e.preventDefault();
          const photoFile = document.getElementById("sPhoto").files[0];
          const tourName = document.getElementById("sTourName").value.trim();
          const medal = document.getElementById("sMedal").value;
          const tourYear = document.getElementById("sTourYear").value.trim();

          const createStudentObj = (photoBase64) => {
            students.push({
              id: Date.now(),
              name: document.getElementById("sName").value,
              dob: document.getElementById("sDob").value,
              mobile: document.getElementById("sMobile").value,
              belt: document.getElementById("sBelt").value,
              doj: document.getElementById("sDoj").value,
              batch: document.getElementById("sBatch").value,
              address: document.getElementById("sAddress").value,
              tournament: tourName
                ? { name: tourName, medal: medal, year: tourYear }
                : null,
              photo: photoBase64 || defaultAvatar,
            });
            localStorage.setItem(
              "yash_taekwondo_v2_students",
              JSON.stringify(students),
            );
            this.reset();
            renderAdminData();
          };

          if (photoFile) {
            const reader = new FileReader();
            reader.onloadend = () => createStudentObj(reader.result);
            reader.readAsDataURL(photoFile);
          } else {
            createStudentObj(null);
          }
        });

      function getRecordKey() {
        return `${document.getElementById("filterYear").value}-${document.getElementById("filterMonth").value}`;
      }

      function renderAdminData() {
        const key = getRecordKey();
        if (!monthlyRecords[key]) monthlyRecords[key] = {};
        const tbody = document.getElementById("studentTableBody");
        tbody.innerHTML = "";
        let totalP = 0,
          totalPaid = 0,
          totalPend = 0;

        students.forEach((student) => {
          if (!monthlyRecords[key][student.id])
            monthlyRecords[key][student.id] = {
              feeStatus: "Pending",
              presentDays: 0,
            };
          const record = monthlyRecords[key][student.id];

          if (record.feeStatus === "Paid") totalPaid++;
          else totalPend++;
          totalP += record.presentDays;

          let tourHtml = "<small style='color:#888;'>No Record</small>";
          if (student.tournament && student.tournament.name) {
            tourHtml = `<strong>${student.tournament.name}</strong> (${student.tournament.year || "N/A"})<br><span class="badge badge-gold">${student.tournament.medal}</span>`;
          }

          tbody.appendChild(
            Object.assign(document.createElement("tr"), {
              innerHTML: `
              <td><div class="student-cell"><img src="${student.photo || defaultAvatar}" class="student-thumb"><div><strong>${student.name}</strong><br><small>📱 ${student.mobile}</small></div></div></td>
              <td>DOB: ${student.dob}<br>DOJ: ${student.doj}</td>
              <td><span class="badge" style="background:#6c757d;">${student.belt}</span><br><small>${student.batch}</small></td>
              <td>${tourHtml}</td>
              <td>${student.address}</td>
              <td><span class="badge ${record.feeStatus === "Paid" ? "badge-paid" : "badge-pending"}">${record.feeStatus}</span><br><br><button class="btn-sm btn-blue" onclick="toggleFee('${key}', ${student.id})">Toggle Fee</button></td>
              <td><strong>Days Present: ${record.presentDays}</strong><br><br><button class="btn-sm btn-green" onclick="adjustAttendance('${key}', ${student.id}, 1)">+1</button><button class="btn-sm btn-orange" onclick="adjustAttendance('${key}', ${student.id}, -1)">-1</button></td>
              <td><button class="btn-sm btn-dark" onclick="deleteStudent(${student.id})">Delete</button></td>
            `,
            }),
          );
        });

        document.getElementById("statTotal").innerText = students.length;
        document.getElementById("statPresent").innerText = totalP;
        document.getElementById("statPaid").innerText = totalPaid;
        document.getElementById("statPending").innerText = totalPend;
      }

      function toggleFee(key, id) {
        monthlyRecords[key][id].feeStatus =
          monthlyRecords[key][id].feeStatus === "Paid" ? "Pending" : "Paid";
        localStorage.setItem(
          "yash_taekwondo_v2_records",
          JSON.stringify(monthlyRecords),
        );
        renderAdminData();
      }

      function adjustAttendance(key, id, change) {
        let cur = (monthlyRecords[key][id].presentDays || 0) + change;
        monthlyRecords[key][id].presentDays = Math.max(0, cur);
        localStorage.setItem(
          "yash_taekwondo_v2_records",
          JSON.stringify(monthlyRecords),
        );
        renderAdminData();
      }

      function deleteStudent(id) {
        if (confirm("Delete this student?")) {
          students = students.filter((s) => s.id !== id);
          localStorage.setItem(
            "yash_taekwondo_v2_students",
            JSON.stringify(students),
          );
          renderAdminData();
        }
      }

      function exportToExcel() {
        if (!students.length) return alert("No data to export!");
        const key = getRecordKey();
        let csv =
          "data:text/csv;charset=utf-8,\uFEFFName,Mobile,DOB,Belt,DOJ,Batch,Address,Fee Status,Present Days\n";
        students.forEach((s) => {
          const rec = (monthlyRecords[key] && monthlyRecords[key][s.id]) || {
            feeStatus: "Pending",
            presentDays: 0,
          };
          csv += `"${s.name}","${s.mobile}","${s.dob}","${s.belt}","${s.doj}","${s.batch}","${s.address.replace(/\n/g, " ")}","${rec.feeStatus}","${rec.presentDays}"\n`;
        });
        const link = document.createElement("a");
        link.href = encodeURI(csv);
        link.download = `Students_${key}.csv`;
        link.click();
      }

      function renderStudentDashboard() {
        if (!currentLoggedInStudent) return;
        const s = currentLoggedInStudent;
        document.getElementById("stProfileImg").src = s.photo || defaultAvatar;
        document.getElementById("stProfileName").innerText = s.name;
        document.getElementById("stProfileMobile").innerText = s.mobile;
        document.getElementById("stProfileDob").innerText = s.dob;
        document.getElementById("stProfileBelt").innerText = s.belt;
        document.getElementById("stProfileDoj").innerText = s.doj;
        document.getElementById("stProfileBatch").innerText = s.batch;
        document.getElementById("stProfileAddress").innerText = s.address;

        const year = document.getElementById("stFilterYear").value;
        const tbody = document.getElementById("studentLogsBody");
        tbody.innerHTML = "";
        const months = [
          "01",
          "02",
          "03",
          "04",
          "05",
          "06",
          "07",
          "08",
          "09",
          "10",
          "11",
          "12",
        ];
        const monthNames = [
          "January",
          "February",
          "March",
          "April",
          "May",
          "June",
          "July",
          "August",
          "September",
          "October",
          "November",
          "December",
        ];

        months.forEach((m, idx) => {
          const key = `${year}-${m}`;
          const rec =
            monthlyRecords[key] && monthlyRecords[key][s.id]
              ? monthlyRecords[key][s.id]
              : { feeStatus: "Pending", presentDays: 0 };
          tbody.appendChild(
            Object.assign(document.createElement("tr"), {
              innerHTML: `<td><strong>${monthNames[idx]} ${year}</strong></td><td><span class="badge ${rec.feeStatus === "Paid" ? "badge-paid" : "badge-pending"}">${rec.feeStatus}</span></td><td>${rec.presentDays} Days Present</td>`,
            }),
          );
        });
      }

      // Initialize
      renderSlider();
      renderPublicCms();
    </script>
  </body>
</html>

