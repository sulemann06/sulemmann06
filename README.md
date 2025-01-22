<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Quiz App</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background-color: #f4f4f9;
            text-align: center;
        }
        header {
            background-color: #4CAF50;
            color: white;
            padding: 10px 0;
        }
        .container {
            max-width: 600px;
            margin: 20px auto;
            background: white;
            padding: 20px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }
        .question {
            font-size: 1.2em;
        }
        .options {
            list-style-type: none;
            padding: 0;
        }
        .options li {
            margin: 10px 0;
        }
        .btn {
            background-color: #4CAF50;
            color: white;
            border: none;
            padding: 10px 20px;
            cursor: pointer;
            font-size: 1em;
        }
        .btn:hover {
            background-color: #45a049;
        }
    </style>
</head>
<body>
    <header>
        <h1>Quiz App</h1>
    </header>
    <div class="container">
        <div id="quiz-container">
            <p class="question" id="question">Loading question...</p>
            <ul class="options" id="options"></ul>
            <button class="btn" id="submit-btn" onclick="submitAnswer()">Submit</button>
        </div>
        <div id="result-container" style="display: none;">
            <h2>Your Result</h2>
            <p id="score"></p>
            <button class="btn" onclick="restartQuiz()">Restart</button>
        </div>
    </div>

    <script>
        const questions = [
            {
                question: "What are the two main types of software?",
                options: ["System software and Application software", "Hardware and Middleware", "Operating Systems and Utilities"],
                correct: 0
            },
            {
                question: "Which sphere of influence helps individuals improve personal effectiveness?",
                options: ["Personal sphere", "Workgroup sphere", "Enterprise sphere"],
                correct: 0
            },
            {
                question: "What is a primary function of an operating system?",
                options: ["Manage system memory", "Store data permanently", "Enhance user interface only"],
                correct: 0
            }
        ];

        let currentQuestionIndex = 0;
        let score = 0;

        function loadQuestion() {
            const questionData = questions[currentQuestionIndex];
            document.getElementById("question").textContent = questionData.question;
            const optionsContainer = document.getElementById("options");
            optionsContainer.innerHTML = "";

            questionData.options.forEach((option, index) => {
                const li = document.createElement("li");
                li.innerHTML = `<label><input type="radio" name="option" value="${index}"> ${option}</label>`;
                optionsContainer.appendChild(li);
            });
        }

        function submitAnswer() {
            const selectedOption = document.querySelector('input[name="option"]:checked');
            if (!selectedOption) {
                alert("Please select an answer!");
                return;
            }

            const answer = parseInt(selectedOption.value);
            if (answer === questions[currentQuestionIndex].correct) {
                score++;
            }

            currentQuestionIndex++;

            if (currentQuestionIndex < questions.length) {
                loadQuestion();
            } else {
                showResult();
            }
        }

        function showResult() {
            document.getElementById("quiz-container").style.display = "none";
            document.getElementById("result-container").style.display = "block";
            document.getElementById("score").textContent = `You scored ${score} out of ${questions.length}`;
        }

        function restartQuiz() {
            currentQuestionIndex = 0;
            score = 0;
            document.getElementById("quiz-container").style.display = "block";
            document.getElementById("result-container").style.display = "none";
            loadQuestion();
        }

        // Load the first question on page load
        loadQuestion();
    </script>
</body>
</html>
