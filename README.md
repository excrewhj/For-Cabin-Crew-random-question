<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Foreign Airline Cabin Crew Interview</title>
    <style>
        body { font-family: Arial, sans-serif; text-align: center; background-color: #f8f9fa; }
        .container { margin: 50px auto; padding: 20px; background: white; border-radius: 10px; width: 50%; box-shadow: 0 0 10px rgba(0,0,0,0.1); }
        .btn { display: block; width: 80%; margin: 10px auto; padding: 10px; font-size: 18px; border: none; border-radius: 5px; cursor: pointer; }
        .purple-btn { background-color: #9370DB; color: white; }
        .purple-btn:hover { background-color: #7B68EE; }
        .hidden { display: none; }
        #timer { font-size: 20px; font-weight: bold; margin-top: 10px; }
        .copyright { font-size: 14px; color: gray; margin-top: 10px; }
    </style>
</head>
<body>
    <div class="container" id="mainPage">
        <h2>Foreign Airline Cabin Crew Interview</h2>
        <button class="btn purple-btn" onclick="startQuiz()">Start Random Questions</button>
    </div>

    <div class="container hidden" id="quizPage">
        <h2 id="question"></h2>
        <div id="timer">Remaining Time: 100 seconds</div>
        <button class="btn purple-btn hidden" id="nextBtn" onclick="nextQuestion()">Next Question</button>
        <button class="btn purple-btn hidden" id="returnBtn" onclick="returnToMain()">Return to Main Page</button>
    </div>

    <script>
        const questions = [
            "Describe yourself in three words.", "Why do you want to be a cabin crew?", "How do you handle stressful situations?",
            "Tell us about a time you provided excellent customer service.", "What do you know about our airline?",
            "How would you deal with a difficult passenger?", "What do you think is the most important quality of a cabin crew?",
            "How do you handle cultural differences while working internationally?", "What are your strengths and weaknesses?",
            "What would you do if a passenger refuses to follow safety instructions?"
        ];

        let selectedQuestions = [];
        let currentQuestionIndex = 0;
        let timer;

        function startQuiz() {
            document.getElementById('mainPage').classList.add('hidden');
            document.getElementById('quizPage').classList.remove('hidden');
            selectedQuestions = questions.sort(() => 0.5 - Math.random()).slice(0, 2);
            currentQuestionIndex = 0;
            showQuestion();
        }

        function showQuestion() {
            if (currentQuestionIndex < selectedQuestions.length) {
                document.getElementById('question').innerText = selectedQuestions[currentQuestionIndex];
                document.getElementById('nextBtn').classList.remove('hidden');
                startTimer();
            } else {
                document.getElementById('question').innerText = "Questions are over!";
                document.getElementById('nextBtn').classList.add('hidden');
                document.getElementById('returnBtn').classList.remove('hidden');
            }
        }

        function nextQuestion() {
            clearInterval(timer);
            currentQuestionIndex++;
            showQuestion();
        }

        function startTimer() {
            let timeLeft = 100;
            document.getElementById('timer').innerText = `Remaining Time: ${timeLeft} seconds`;
            timer = setInterval(() => {
                timeLeft--;
                document.getElementById('timer').innerText = `Remaining Time: ${timeLeft} seconds`;
                if (timeLeft <= 0) {
                    clearInterval(timer);
                    currentQuestionIndex++;
                    showQuestion();
                }
            }, 1000);
        }

        function returnToMain() {
            location.reload();
        }
    </script>
</body>
</html>
