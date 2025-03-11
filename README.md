# passwordgenerator123
A simple password generator website 
<!DOCTYPE html>
<html lang="hi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>रैंडम पासवर्ड जनरेटर</title>
    <style>
        body {
            font-family: 'Arial', sans-serif;
            background-color: #1a1a1a;
            color: white;
            display: flex;
            flex-direction: column;
            align-items: center;
            min-height: 100vh;
            margin: 0;
            padding: 20px;
        }

        .container {
            background-color: #2d2d2d;
            padding: 30px;
            border-radius: 10px;
            box-shadow: 0 0 20px rgba(0,0,0,0.3);
            width: 90%;
            max-width: 500px;
        }

        h1 {
            color: #4CAF50;
            text-align: center;
            margin-bottom: 30px;
        }

        .password-display {
            background-color: #333;
            padding: 15px;
            border-radius: 5px;
            margin-bottom: 20px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        #password {
            font-size: 1.2em;
            word-break: break-all;
            margin-right: 10px;
        }

        .options {
            margin-bottom: 20px;
        }

        .option-group {
            margin-bottom: 15px;
        }

        label {
            display: block;
            margin-bottom: 5px;
        }

        input[type="number"] {
            width: 100%;
            padding: 8px;
            border-radius: 5px;
            border: 1px solid #555;
            background-color: #333;
            color: white;
        }

        button {
            background-color: #4CAF50;
            color: white;
            border: none;
            padding: 10px 20px;
            border-radius: 5px;
            cursor: pointer;
            transition: background-color 0.3s;
        }

        button:hover {
            background-color: #45a049;
        }

        .copy-btn {
            background-color: #008CBA;
            margin-left: 10px;
        }

        .copy-btn:hover {
            background-color: #007399;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>रैंडम पासवर्ड जनरेटर</h1>
        <div class="password-display">
            <span id="password">क्लिक करके पासवर्ड जनरेट करें</span>
            <button class="copy-btn" onclick="copyPassword()">कॉपी करें</button>
        </div>
        
        <div class="options">
            <div class="option-group">
                <label for="length">पासवर्ड लंबाई:</label>
                <input type="number" id="length" min="4" max="50" value="12">
            </div>
            
            <div class="option-group">
                <label><input type="checkbox" id="uppercase" checked> बड़े अक्षर (A-Z)</label>
            </div>
            
            <div class="option-group">
                <label><input type="checkbox" id="lowercase" checked> छोटे अक्षर (a-z)</label>
            </div>
            
            <div class="option-group">
                <label><input type="checkbox" id="numbers" checked> संख्याएं (0-9)</label>
            </div>
            
            <div class="option-group">
                <label><input type="checkbox" id="symbols"> विशेष चिन्ह (!@#$%^&*)</label>
            </div>
        </div>
        
        <button onclick="generatePassword()">पासवर्ड जनरेट करें</button>
    </div>

    <script>
        function generatePassword() {
            const length = parseInt(document.getElementById('length').value);

            // इनपुट की वैधता जाँच
            if (isNaN(length) || length < 4 || length > 50) {
                document.getElementById('password').textContent = 'कृपया 4 से 50 के बीच की लंबाई चुनें!';
                return;
            }

            const uppercase = document.getElementById('uppercase').checked;
            const lowercase = document.getElementById('lowercase').checked;
            const numbers = document.getElementById('numbers').checked;
            const symbols = document.getElementById('symbols').checked;

            let charset = '';
            if (uppercase) charset += 'ABCDEFGHIJKLMNOPQRSTUVWXYZ';
            if (lowercase) charset += 'abcdefghijklmnopqrstuvwxyz';
            if (numbers) charset += '0123456789';
            if (symbols) charset += '!@#$%^&*()_+~`|}{[];?><,./-=';

            if (!charset) {
                document.getElementById('password').textContent = 'कम से कम एक विकल्प चुनें!';
                return;
            }

            let password = '';
            for (let i = 0; i < length; i++) {
                const randomIndex = Math.floor(Math.random() * charset.length);
                password += charset[randomIndex];
            }

            document.getElementById('password').textContent = password;
        }

        function copyPassword() {
            const passwordField = document.getElementById('password');
            const textArea = document.createElement('textarea');
            textArea.value = passwordField.innerText || passwordField.textContent;
            document.body.appendChild(textArea);
            textArea.select();
            document.execCommand('copy');
            document.body.removeChild(textArea);
            alert('पासवर्ड कॉपी हो गया!');
        }
    </script>
</body>
</html>
