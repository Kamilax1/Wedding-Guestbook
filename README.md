# Wedding-Guestbook
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
    <meta http-equiv="Content-Type" content="application/xhtml+xml; charset=UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Księga Gości Weselnych</title>
    <style type="text/css">
        body {
            font-family: 'Arial', sans-serif;
            background-color: #f5f5f5;
            color: #333;
            margin: 0;
            padding: 0;
            overflow-x: hidden;
        }
        header {
            background-color: #f1e4b3; /* Beżowy */
            color: #4b7747; /* Zieleń */
            text-align: center;
            padding: 30px;
            border-bottom: 5px solid #c0c0c0; /* Srebrny */
        }
        header h1 {
            font-size: 3rem;
            margin: 0;
            font-weight: bold;
        }
        .container {
            max-width: 900px;
            margin: 20px auto;
            padding: 20px;
            background-color: #fff;
            border-radius: 10px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        }
        h2 {
            text-align: center;
            color: #4b7747; /* Zieleń */
            font-size: 2rem;
            margin-bottom: 20px;
        }
        .guestbook-form {
            display: flex;
            flex-direction: column;
            align-items: center;
        }
        .guestbook-form input, .guestbook-form textarea {
            width: 80%;
            margin: 10px 0;
            padding: 10px;
            border-radius: 5px;
            border: 1px solid #ccc;
            font-size: 1rem;
        }
        .guestbook-form button {
            background-color: #4b7747; /* Zieleń */
            color: #fff;
            padding: 10px 20px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-size: 1.1rem;
            margin-top: 10px;
        }
        .guestbook-form button:hover {
            background-color: #3e5d3e; /* Ciemniejsza zieleń */
        }
        .guest-entry {
            background-color: #f9f9f9;
            padding: 15px;
            margin-bottom: 20px;
            border-radius: 8px;
            border: 1px solid #ccc;
        }
        .guest-entry h3 {
            color: #4b7747; /* Zieleń */
            margin: 0;
        }
        .guest-entry p {
            font-size: 1.1rem;
            margin-top: 10px;
        }
        .guest-entry img {
            max-width: 100px;
            border-radius: 50%;
            margin-right: 15px;
        }
        .guest-entry .entry-content {
            display: flex;
            align-items: center;
        }
        .guest-entry .entry-content div {
            flex: 1;
        }
        .guest-page {
            padding: 40px 0;
            margin-bottom: 20px;
            border-bottom: 2px solid #e1e1e1;
        }
    </style>
</head>
<body>

    <header>
        <h1>Księga Gości Weselnych</h1>
        <p>Witamy w naszej księdze gości! Prosimy, zostawcie swoje zdjęcia i życzenia.</p>
    </header>

    <div class="container">
        <h2>Dodaj swoje życzenia</h2>

        <!-- Formularz do dodawania zdjęć, podpisu i życzeń -->
        <form action="javascript:void(0);" method="post" class="guestbook-form">
            <input type="file" id="photo" name="photo" accept="image/*" />
            <input type="text" id="name" name="name" placeholder="Twoje imię" required="required" />
            <textarea id="message" name="message" placeholder="Twoje życzenia" rows="4" required="required"></textarea>
            <button type="submit">Dodaj Życzenia</button>
        </form>

        <div id="guestbook-entries">
            <!-- Tutaj będą pojawiać się nowe strony z wpisami -->
        </div>
    </div>

    <script type="text/javascript">
        document.querySelector('.guestbook-form').addEventListener('submit', function(event) {
            event.preventDefault();

            const name = document.getElementById('name').value.trim();
            const message = document.getElementById('message').value.trim();
            const photo = document.getElementById('photo').files[0];

            if (name && message) {
                const guestbookEntry = document.createElement('div');
                guestbookEntry.classList.add('guest-page');

                // Dodajemy zdjęcie, jeśli zostało wybrane
                let photoHTML = '';
                if (photo) {
                    const reader = new FileReader();
                    reader.onload = function(e) {
                        photoHTML = <img src="${e.target.result}" alt="Zdjęcie Gościa" />;
                        createEntry();
                    };
                    reader.readAsDataURL(photo);
                } else {
                    createEntry();
                }

                // Funkcja do tworzenia nowego wpisu jako "strony"
                function createEntry() {
                    guestbookEntry.innerHTML = `
                        <div class="guest-entry">
                            <div class="entry-content">
                                ${photoHTML}
                                <div>
                                    <h3>${name}</h3>
                                    <p>${message}</p>
                                </div>
                            </div>
                        </div>
                    `;
                    document.getElementById('guestbook-entries').appendChild(guestbookEntry);

                    // Przewijanie do nowego wpisu
                    window.scrollTo({
                        top: document.body.scrollHeight,
                        behavior: 'smooth'
                    });

                    // Czyszczenie formularza
                    document.getElementById('name').value = '';
                    document.getElementById('message').value = '';
                    document.getElementById('photo').value = '';
                }
            } else {
                alert('Proszę uzupełnić wszystkie pola!');
            }
        });
    </script>

</body>
</html>
