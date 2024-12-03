<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>EmpowerHer</title>
    <script src="https://www.gstatic.com/firebasejs/9.6.1/firebase-app.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.6.1/firebase-database.js"></script>
    <script src="https://maps.googleapis.com/maps/api/js?key=YOUR_GOOGLE_MAPS_API_KEY&callback=initMap" async defer></script>
    <style>
        /* Your existing CSS */
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
        <div class="content-box">
            <h3>Background</h3>
            <p>India, a land of diversity and culture, has witnessed tragedies...</p>
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
    </section>

    <footer>
        <p>IIT Bombay Sanrakshan TechFest - EmpowerHer</p>
    </footer>

    <script>
        // Firebase configuration (placeholders for sensitive data)
        const firebaseConfig = {
            apiKey: "YOUR_FIREBASE_API_KEY",
            authDomain: "YOUR_FIREBASE_AUTH_DOMAIN",
            databaseURL: "YOUR_FIREBASE_DATABASE_URL",
            projectId: "YOUR_FIREBASE_PROJECT_ID",
            storageBucket: "YOUR_FIREBASE_STORAGE_BUCKET",
            messagingSenderId: "YOUR_FIREBASE_MESSAGING_SENDER_ID",
            appId: "YOUR_FIREBASE_APP_ID",
            measurementId: "YOUR_FIREBASE_MEASUREMENT_ID"
        };

        // Initialize Firebase
        const app = firebase.initializeApp(firebaseConfig);
        const database = firebase.database(app);

        // Initialize Google Map
        let map;

        function initMap() {
            map = new google.maps.Map(document.getElementById('map'), {
                center: { lat: 19.0760, lng: 72.8777 },
                zoom: 10,
            });

            const locationRef = database.ref('locations/user1'); 
            locationRef.once('value')
                .then((snapshot) => {
                    const location = snapshot.val();
                    if (location) {
                        const lat = location.latitude;
                        const lng = location.longitude;

                        const position = new google.maps.LatLng(lat, lng);
                        const marker = new google.maps.Marker({
                            position: position,
                            map: map,
                            title: "Current Location"
                        });

                        map.setCenter(position);
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

