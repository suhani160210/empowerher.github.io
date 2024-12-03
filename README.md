 <!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>EmpowerHer</title>
    <script src="https://www.gstatic.com/firebasejs/9.6.1/firebase-app.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.6.1/firebase-database.js"></script>
    <script src="https://maps.googleapis.com/maps/api/js?key=AIzaSyA3MoeZz6x7PDsHxtuiydBDi7ICwjCgg5A&callback=initMap" async defer></script>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #ffdcc5; /* Background color */
            margin: 0;
            color: black; /* Text color */
        }

        header {
            background-color: #e2906e; /* Header color */
            color: white;
            padding: 15px 20px;
            text-align: center;
        }

        header h1 {
            color: black; /* EmpowerHer text color */
            text-transform: uppercase; /* Make text uppercase */
            font-size: 36px; /* Increase text size */
            margin: 0;
        }

        header nav a {
            color: #9c4639; /* Color for Home, Purpose, and Help links */
            text-decoration: none;
            margin: 0 15px;
            font-weight: bold;
            cursor: pointer;
        }

        header nav a:hover {
            text-decoration: underline;
        }

        section {
            display: none;
            padding: 20px;
        }

        section.active {
            display: block;
        }

        h2 {
            color: #9c4639; /* Section headings color */
            margin-bottom: 15px;
        }

        .content-box {
            padding: 15px;
            background-color: #e2906e;
            border-radius: 8px;
            color: white;
            margin-bottom: 20px;
        }

        .faq-box textarea {
            width: 100%;
            height: 80px;
            margin-top: 10px;
            padding: 8px;
            border-radius: 5px;
            border: 1px solid #ccc;
        }

        .thin-line {
            border-top: 1px solid black;
            margin: 20px 0;
        }

        footer {
            margin-top: 30px;
            text-align: center;
            color: black;
            font-size: 14px;
        }

        #map {
            height: 400px;
            width: 100%;
        }
    </style>
</head>
<body>
    <header>
        <h1>EmpowerHer</h1>
        <nav>
            <a onclick="navigateTo('home')">Home</a>
            <a onclick="navigateTo('purpose')">Purpose</a>
            <a onclick="navigateTo('help')">Help</a>
        </nav>
    </header>

    <!-- Home Section -->
    <section id="home" class="active">
        <h2>SOS Contacts</h2>
        <div class="content-box">
            <p><strong>Date, Time</strong></p>
            <p>Your contact XYZ requires your assistance.</p>
        </div>
        <div class="content-box">
            <p><strong>Date, Time</strong></p>
            <p id="location-link">Loading location...</p>
        </div>
        
        <!-- Google Map -->
        <div id="map"></div>
    </section>

    <!-- Purpose Section -->
    <section id="purpose">
        <h2>Our Purpose</h2>

        <!-- Background Section -->
        <div class="content-box">
            <h3>Background</h3>
            <p>India, a land of diversity and culture, has witnessed tragedies that have shaken its soul. The 2012 Nirbhaya case was a horrifying reminder of the vulnerability women face in public spaces, sparking nationwide protests and global outrage. More recently, the case of Dr. Moumita Debnath revealed that even years later, the shadow of fear continues to loom over women. These incidents are not isolated—they represent a grim reality for countless women who live in fear every day.
            Despite advancements in technology, women’s safety often remains neglected, and many existing solutions fail to provide the discreet, immediate help required in emergencies. This inspired us to take action.</p>
        </div>

        <!-- Our Team Section -->
        <div class="content-box">
            <h3>Our Team</h3>
            <div class="thin-line"></div>
            <p>Our team consists of passionate individuals who are dedicated to making a change in society. Each member contributes their expertise, creativity, and vision to the development of EmpowerHer.</p>
        </div>

        <!-- Our Journey Section -->
        <div class="content-box">
            <h3>Our Journey</h3>
            <p>It all started as an ambitious idea for a tech fest competition at IIT Bombay. As 9th graders passionate about technology and social change, we wanted to go beyond theoretical ideas and create something meaningful. Inspired by the stories of countless women and motivated to build a safer India, we developed the EmpowerHer safety accessory—an effective tool designed to empower women and provide immediate help in critical moments. 
            Through countless hours of brainstorming, coding, designing, and testing, we crafted a device that aligns with our vision of a safer and more inclusive future.</p>
        </div>

        <!-- Vision Section -->
        <div class="content-box">
            <h3>Vision</h3>
            <p>To create a future where every woman in India feels secure and empowered to explore her full potential without fear. Our vision is to eliminate the need for vigilance and replace it with confidence—confidence that safety is within reach and that society stands united in protecting its daughters, sisters, and mothers.</p>
        </div>

        <!-- Mission Section -->
        <div class="content-box">
            <h3>Mission</h3>
            <p>To design and deliver accessible and reliable safety solutions that provide immediate support in emergencies, fostering confidence and equality. Through continuous innovation, we aim to protect lives and inspire communities to prioritize the safety and dignity of women everywhere.</p>
        </div>

    </section>

    <!-- Help Section -->
    <section id="help">
        <h2>Help Page</h2>
        <div class="faq-box">
            <h3>FAQs</h3>
            <p>Submit your question below:</p>
            <textarea placeholder="Type your question here..."></textarea>
        </div>
        <h3>How Does It Work?</h3>
        <ol>
            <li>Step 1: Register and set up your profile.</li>
            <li>Step 2: Connect with other women in your community.</li>
            <li>Step 3: Access real-time assistance when needed.</li>
        </ol>
        <div>
            <h3>Watch this video:</h3>
            <iframe 
                width="100%" 
                height="200px" 
                src="https://www.youtube.com/embed/dQw4w9WgXcQ" 
                frameborder="0" 
                allowfullscreen>
            </iframe>
        </div>
    </section>

    <footer>
        <p> IIT Bombay Sanrakshan TechFest - EmpowerHer</p>
    </footer>

    <script>
        // Firebase configuration
        const firebaseConfig = {
            apiKey: "AIzaSyA3MoeZz6x7PDsHxtuiydBDi7ICwjCgg5A",
            authDomain: "empowerher-f841d.firebaseapp.com",
            databaseURL: "https://empowerher-f841d-default-rtdb.firebaseio.com/",
            projectId: "empowerher-f841d",
            storageBucket: "empowerher-f841d.appspot.com",
            messagingSenderId: "YOUR_MESSAGING_SENDER_ID",
            appId: "YOUR_APP_ID",
            measurementId: "YOUR_MEASUREMENT_ID"
        };

        // Initialize Firebase
        const app = firebase.initializeApp(firebaseConfig);
        const database = firebase.database(app);

        // Initialize the Google Map
        let map;

        function initMap() {
            // Default location (Mumbai)
            map = new google.maps.Map(document.getElementById('map'), {
                center: { lat: 19.0760, lng: 72.8777 },
                zoom: 10,
            });

            // Fetch location data from Firebase
            const locationRef = database.ref('locations/user1'); // Adjust the path to your data
            locationRef.once('value')
                .then((snapshot) => {
                    const location = snapshot.val();
                    if (location) {
                        const lat = location.latitude;
                        const lng = location.longitude;

                        // Create a marker for the location
                        const position = new google.maps.LatLng(lat, lng);
                        const marker = new google.maps.Marker({
                            position: position,
                            map: map,
                            title: "Current Location"
                        });

                        // Center the map on the location
                        map.setCenter(position);

                        // Create a link to open the location in Google Maps
                        const locationLink = `https://www.google.com/maps?q=${lat},${lng}`;
                        document.getElementById('location-link').innerHTML = `<a href="${locationLink}" target="_blank">View Location</a>`;
                    } else {
                        document.getElementById('location-link').textContent = "Location not available.";
                    }
                })
                .catch((error) => {
                    console.error('Error fetching location:', error);
                });
        }

        // Navigation function
        function navigateTo(sectionId) {
            document.querySelectorAll('section').forEach(section => {
                section.classList.remove('active');
            });

            const activeSection = document.getElementById(sectionId);
            activeSection.classList.add('active');
        }
    </script>
</body>
</html>
