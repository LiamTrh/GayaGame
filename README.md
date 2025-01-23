<!DOCTYPE html>
<html lang="he">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>משחק חיבור וחיסור</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            background-color: #f0f8ff;
            margin: 0;
            padding: 20px;
        }
        .container {
            max-width: 400px;
            margin: 0 auto;
            background: #fff;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
        }
        .question {
            font-size: 24px;
            margin-bottom: 15px;
        }
        input[type="number"] {
            font-size: 18px;
            padding: 5px;
            width: 100px;
            text-align: center;
        }
        button {
            font-size: 18px;
            padding: 10px 20px;
            margin: 10px 5px;
            background-color: #4caf50;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }
        button:hover {
            background-color: #45a049;
        }
        .result {
            margin-top: 20px;
            font-size: 20px;
            font-weight: bold;
        }
    </style>
</head>
<body>
    <h1>משחק חיבור וחיסור</h1>
    <div class="container">
        <div class="question" id="question"></div>
        <input type="number" id="answer" placeholder="תשובה">
        <button onclick="checkAnswer()">בדוק תשובה</button>
        <div class="result" id="result"></div>
    </div>

    <script>
        let num1, num2, operation, correctAnswer;

        function generateQuestion() {
            do {
                num1 = Math.floor(Math.random() * 6); // מספר בין 0 ל-5
                num2 = Math.floor(Math.random() * 6); // מספר בין 0 ל-5
                operation = Math.random() < 0.5 ? '+' : '-'; // חיבור או חיסור

                if (operation === '-' && num1 < num2) {
                    [num1, num2] = [num2, num1]; // למנוע תוצאה שלילית
                }

                correctAnswer = operation === '+' ? num1 + num2 : num1 - num2;
            } while (correctAnswer > 10); // להבטיח שהתוצאה 10 או פחות

            document.getElementById('question').textContent = `${num1} ${operation} ${num2} = ?`;
            document.getElementById('answer').value = '';
            document.getElementById('result').textContent = '';
        }

        function checkAnswer() {
            const userAnswer = parseInt(document.getElementById('answer').value, 10);

            if (isNaN(userAnswer)) {
                document.getElementById('result').textContent = 'אנא הזן מספר תקין.';
                document.getElementById('result').style.color = 'red';
                return;
            }

            if (userAnswer === correctAnswer) {
                document.getElementById('result').textContent = 'תשובה נכונה! כל הכבוד!';
                document.getElementById('result').style.color = 'green';
            } else {
                document.getElementById('result').textContent = `טעות. התשובה הנכונה היא ${correctAnswer}.`;
                document.getElementById('result').style.color = 'red';
            }

            setTimeout(generateQuestion, 2000); // שאלה חדשה אחרי 2 שניות
        }

        generateQuestion(); // יוצרים שאלה ראשונה
    </script>
</body>
</html>


