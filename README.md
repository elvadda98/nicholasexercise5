<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vocabulary Game: Practical & Specialized Terms</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #ff6b6b 0%, #ff8e53 100%);
            min-height: 100vh;
            padding: 20px;
            color: #333;
        }

        .container {
            max-width: 1000px;
            margin: 0 auto;
            background: white;
            border-radius: 20px;
            box-shadow: 0 15px 35px rgba(0,0,0,0.2);
            overflow: hidden;
        }

        .header {
            background: linear-gradient(135deg, #ff6b6b, #ff8e53);
            color: white;
            padding: 30px;
            text-align: center;
            position: relative;
        }

        .header::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: url('data:image/svg+xml,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 100 100"><circle cx="20" cy="20" r="2" fill="rgba(255,255,255,0.1)"/><circle cx="80" cy="30" r="1.5" fill="rgba(255,255,255,0.1)"/><circle cx="40" cy="70" r="1" fill="rgba(255,255,255,0.1)"/><circle cx="90" cy="80" r="2.5" fill="rgba(255,255,255,0.1)"/></svg>');
        }

        .header h1 {
            font-size: 2.5em;
            margin-bottom: 10px;
            position: relative;
            z-index: 1;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.2);
        }

        .header p {
            font-size: 1.2em;
            opacity: 0.9;
            position: relative;
            z-index: 1;
        }

        .nav-buttons {
            display: flex;
            justify-content: center;
            gap: 10px;
            padding: 20px;
            background: #f8f9fa;
            flex-wrap: wrap;
        }

        .nav-btn {
            padding: 12px 24px;
            border: none;
            border-radius: 25px;
            cursor: pointer;
            font-size: 16px;
            font-weight: bold;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(0,0,0,0.1);
        }

        .nav-btn.active {
            background: linear-gradient(135deg, #ff6b6b, #ff8e53);
            color: white;
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(255,107,107,0.4);
        }

        .nav-btn:not(.active) {
            background: white;
            color: #666;
        }

        .nav-btn:hover:not(.active) {
            background: #e9ecef;
            transform: translateY(-1px);
        }

        .game-section {
            display: none;
            padding: 30px;
            min-height: 400px;
        }

        .game-section.active {
            display: block;
            animation: fadeIn 0.5s ease-in;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .word-bank {
            background: linear-gradient(135deg, #f5f7fa, #e8f4f2);
            padding: 25px;
            border-radius: 15px;
            margin-bottom: 25px;
            border: 2px solid #ff6b6b;
            box-shadow: 0 4px 15px rgba(255,107,107,0.2);
        }

        .word-bank h3 {
            color: #ff6b6b;
            margin-bottom: 15px;
            text-align: center;
            font-size: 1.4em;
        }

        .word-options {
            display: flex;
            flex-wrap: wrap;
            gap: 12px;
            justify-content: center;
        }

        .word-option {
            background: linear-gradient(135deg, #ff6b6b, #ff8e53);
            color: white;
            padding: 10px 18px;
            border-radius: 20px;
            font-weight: bold;
            font-size: 16px;
            box-shadow: 0 3px 10px rgba(255,107,107,0.3);
            transition: all 0.3s ease;
            cursor: default;
        }

        .word-option:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(255,107,107,0.4);
        }

        .question {
            background: #f8f9fa;
            padding: 25px;
            border-radius: 15px;
            margin-bottom: 20px;
            border-left: 5px solid #ff6b6b;
            box-shadow: 0 4px 15px rgba(0,0,0,0.05);
        }

        .question h3 {
            color: #ff6b6b;
            margin-bottom: 15px;
            font-size: 1.3em;
        }

        .fill-blank {
            background: #fff;
            border: 2px solid #ddd;
            border-radius: 8px;
            padding: 8px 12px;
            font-size: 16px;
            margin: 0 5px;
            min-width: 120px;
            transition: border-color 0.3s ease;
        }

        .fill-blank.correct {
            border-color: #4CAF50;
            background: #e8f5e8;
        }

        .fill-blank.incorrect {
            border-color: #f44336;
            background: #ffeaea;
        }

        .options {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 15px;
            margin-top: 15px;
        }

        .option {
            padding: 15px 20px;
            border: 2px solid #ddd;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.3s ease;
            background: white;
            text-align: center;
            font-weight: 500;
        }

        .option:hover {
            border-color: #ff6b6b;
            transform: translateY(-2px);
            box-shadow: 0 4px 15px rgba(255,107,107,0.2);
        }

        .option.selected {
            background: #ff6b6b;
            color: white;
            border-color: #ff6b6b;
        }

        .option.correct {
            background: #4CAF50;
            color: white;
            border-color: #4CAF50;
        }

        .option.incorrect {
            background: #f44336;
            color: white;
            border-color: #f44336;
        }

        .matching-container {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 30px;
            margin-top: 20px;
        }

        .match-column h4 {
            text-align: center;
            margin-bottom: 15px;
            color: #ff6b6b;
            font-size: 1.2em;
        }

        .match-item {
            padding: 15px;
            margin: 8px 0;
            border: 2px solid #ddd;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.3s ease;
            background: white;
            text-align: center;
            font-weight: 500;
        }

        .match-item:hover {
            border-color: #ff6b6b;
            transform: translateY(-1px);
            box-shadow: 0 4px 15px rgba(255,107,107,0.2);
        }

        .match-item.selected {
            background: #e8f4f2;
            border-color: #ff6b6b;
        }

        .match-item.matched {
            background: #4CAF50;
            color: white;
            border-color: #4CAF50;
            cursor: default;
        }

        .check-btn {
            background: linear-gradient(135deg, #ff6b6b, #ff8e53);
            color: white;
            border: none;
            padding: 15px 30px;
            border-radius: 25px;
            cursor: pointer;
            font-size: 16px;
            font-weight: bold;
            margin: 20px auto;
            display: block;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(255,107,107,0.3);
        }

        .check-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(255,107,107,0.4);
        }

        .feedback {
            margin-top: 15px;
            padding: 15px;
            border-radius: 10px;
            font-weight: bold;
            text-align: center;
            animation: slideIn 0.3s ease;
        }

        @keyframes slideIn {
            from { transform: translateX(-20px); opacity: 0; }
            to { transform: translateX(0); opacity: 1; }
        }

        .feedback.correct {
            background: #d4edda;
            color: #155724;
            border: 1px solid #c3e6cb;
        }

        .feedback.incorrect {
            background: #f8d7da;
            color: #721c24;
            border: 1px solid #f5c6cb;
        }

        .score {
            position: fixed;
            top: 20px;
            right: 20px;
            background: linear-gradient(135deg, #ff6b6b, #ff8e53);
            color: white;
            padding: 15px 20px;
            border-radius: 25px;
            font-weight: bold;
            box-shadow: 0 4px 15px rgba(255,107,107,0.3);
            z-index: 1000;
        }

        @media (max-width: 768px) {
            .matching-container {
                grid-template-columns: 1fr;
                gap: 20px;
            }
            
            .nav-buttons {
                flex-direction: column;
                align-items: center;
            }
            
            .nav-btn {
                width: 200px;
            }
            
            .score {
                position: static;
                margin: 20px auto;
                display: block;
                width: fit-content;
            }
        }
    </style>
</head>
<body>
    <div class="score">Score: <span id="score">0</span>/30</div>
    
    <div class="container">
        <div class="header">
            <h1>🌟 Practical & Specialized Vocabulary</h1>
            <p>Practice these useful English expressions!</p>
        </div>

        <div class="nav-buttons">
            <button class="nav-btn active" onclick="showSection('fill-gaps')">Fill in the Gaps</button>
            <button class="nav-btn" onclick="showSection('matching')">Match Meanings</button>
            <button class="nav-btn" onclick="showSection('multiple-choice')">Multiple Choice</button>
        </div>

        <!-- Fill in the Gaps Section -->
        <div id="fill-gaps" class="game-section active">
            <div class="word-bank">
                <h3>📝 Word Bank - Choose from these words:</h3>
                <div class="word-options">
                    <span class="word-option">draining</span>
                    <span class="word-option">knowledge base</span>
                    <span class="word-option">tied</span>
                    <span class="word-option">stake</span>
                    <span class="word-option">seek</span>
                    <span class="word-option">clean</span>
                    <span class="word-option">load</span>
                    <span class="option">light</span>
                    <span class="word-option">worth it</span>
                    <span class="word-option">DIY</span>
                </div>
            </div>

            <div class="question">
                <h3>Question 1:</h3>
                <p>After the heavy meal, I prefer to eat something <input type="text" class="fill-blank" data-answer="light" placeholder="answer"> for dinner.</p>
                <div class="feedback" id="feedback-1" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 2:</h3>
                <p>As a major investor, she has a significant <input type="text" class="fill-blank" data-answer="stake" placeholder="answer"> in the company's success.</p>
                <div class="feedback" id="feedback-2" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 3:</h3>
                <p>Employee satisfaction is closely <input type="text" class="fill-blank" data-answer="tied" placeholder="answer"> to workplace environment and management style.</p>
                <div class="feedback" id="feedback-3" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 4:</h3>
                <p>I enjoy <input type="text" class="fill-blank" data-answer="DIY" placeholder="answer"> projects like building furniture and home repairs.</p>
                <div class="feedback" id="feedback-4" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 5:</h3>
                <p>Many graduates <input type="text" class="fill-blank" data-answer="seek" placeholder="answer"> employment opportunities abroad.</p>
                <div class="feedback" id="feedback-5" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 6:</h3>
                <p>Our company's <input type="text" class="fill-blank" data-answer="knowledge base" placeholder="answer"> contains detailed documentation of all our processes.</p>
                <div class="feedback" id="feedback-6" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 7:</h3>
                <p>Please make sure to <input type="text" class="fill-blank" data-answer="clean" placeholder="answer"> your workstation before leaving for the day.</p>
                <div class="feedback" id="feedback-7" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 8:</h3>
                <p>The 12-hour workday was physically and emotionally <input type="text" class="fill-blank" data-answer="draining" placeholder="answer">.</p>
                <div class="feedback" id="feedback-8" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 9:</h3>
                <p>The delivery truck can carry a maximum <input type="text" class="fill-blank" data-answer="load" placeholder="answer"> of 5,000 kilograms.</p>
                <div class="feedback" id="feedback-9" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 10:</h3>
                <p>The expensive software was <input type="text" class="fill-blank" data-answer="worth it" placeholder="answer"> because it increased our productivity by 40%.</p>
                <div class="feedback" id="feedback-10" style="display: none;"></div>
            </div>

            <button class="check-btn" onclick="checkFillBlanks()">Check Answers</button>
        </div>

        <!-- Matching Section -->
        <div id="matching" class="game-section">
            <h2 style="text-align: center; margin-bottom: 20px; color: #ff6b6b;">Match the terms with their meanings</h2>
            <div class="matching-container">
                <div class="match-column">
                    <h4>Terms</h4>
                    <div class="match-item" data-word="draining" onclick="selectMatch(this)">draining</div>
                    <div class="match-item" data-word="knowledge base" onclick="selectMatch(this)">knowledge base</div>
                    <div class="match-item" data-word="tied" onclick="selectMatch(this)">tied</div>
                    <div class="match-item" data-word="stake" onclick="selectMatch(this)">stake</div>
                    <div class="match-item" data-word="seek" onclick="selectMatch(this)">seek</div>
                    <div class="match-item" data-word="clean" onclick="selectMatch(this)">clean</div>
                    <div class="match-item" data-word="load" onclick="selectMatch(this)">load</div>
                    <div class="match-item" data-word="light" onclick="selectMatch(this)">light</div>
                    <div class="match-item" data-word="worth it" onclick="selectMatch(this)">worth it</div>
                    <div class="match-item" data-word="DIY" onclick="selectMatch(this)">DIY</div>
                </div>
                <div class="match-column">
                    <h4>Meanings</h4>
                    <div class="match-item" data-meaning="DIY" onclick="selectMatch(this)">Do It Yourself; activities done without professional help</div>
                    <div class="match-item" data-meaning="draining" onclick="selectMatch(this)">Causing extreme physical or mental fatigue</div>
                    <div class="match-item" data-meaning="knowledge base" onclick="selectMatch(this)">A centralized repository for information</div>
                    <div class="match-item" data-meaning="tied" onclick="selectMatch(this)">Connected or linked to something</div>
                    <div class="match-item" data-meaning="stake" onclick="selectMatch(this)">A share or interest in a business or situation</div>
                    <div class="match-item" data-meaning="seek" onclick="selectMatch(this)">To attempt to find or obtain something</div>
                    <div class="match-item" data-meaning="clean" onclick="selectMatch(this)">To make something free from dirt or marks</div>
                    <div class="match-item" data-meaning="load" onclick="selectMatch(this)">A heavy or bulky thing that is being carried</div>
                    <div class="match-item" data-meaning="light" onclick="selectMatch(this)">Not heavy; of little weight</div>
                    <div class="match-item" data-meaning="worth it" onclick="selectMatch(this)">Good or important enough to justify the effort or cost</div>
                </div>
            </div>
            <div class="feedback" id="matching-feedback" style="display: none;"></div>
        </div>

        <!-- Multiple Choice Section -->
        <div id="multiple-choice" class="game-section">
            <div class="question">
                <h3>Question 1: What does "draining" mean?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">Refreshing and energizing</div>
                    <div class="option" onclick="selectOption(this, true)">Causing extreme fatigue</div>
                    <div class="option" onclick="selectOption(this, false)">Related to water systems</div>
                    <div class="option" onclick="selectOption(this, false)">Easy and effortless</div>
                </div>
                <div class="feedback" id="mc-feedback-1" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 2: A "knowledge base" is:</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">A learning management system</div>
                    <div class="option" onclick="selectOption(this, true)">A centralized repository for information</div>
                    <div class="option" onclick="selectOption(this, false)">A university library</div>
                    <div class="option" onclick="selectOption(this, false)">A database of employee skills</div>
                </div>
                <div class="feedback" id="mc-feedback-2" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 3: "Tied" in this context means:</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">Restricted or limited</div>
                    <div class="option" onclick="selectOption(this, true)">Connected or linked to something</div>
                    <div class="option" onclick="selectOption(this, false)">Finished or completed</div>
                    <div class="option" onclick="selectOption(this, false)">Equally balanced</div>
                </div>
                <div class="feedback" id="mc-feedback-3" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 4: A "stake" in a business refers to:</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">A wooden post</div>
                    <div class="option" onclick="selectOption(this, true)">A share or interest</div>
                    <div class="option" onclick="selectOption(this, false)">A risk or danger</div>
                    <div class="option" onclick="selectOption(this, false)">A financial loss</div>
                </div>
                <div class="feedback" id="mc-feedback-4" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 5: "Seek" means:</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">To avoid something</div>
                    <div class="option" onclick="selectOption(this, true)">To attempt to find or obtain</div>
                    <div class="option" onclick="selectOption(this, false)">To hide from view</div>
                    <div class="option" onclick="selectOption(this, false)">To destroy completely</div>
                </div>
                <div class="feedback" id="mc-feedback-5" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 6: What does "clean" mean?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">To organize systematically</div>
                    <div class="option" onclick="selectOption(this, true)">To make free from dirt</div>
                    <div class="option" onclick="selectOption(this, false)">To purify spiritually</div>
                    <div class="option" onclick="selectOption(this, false)">To clear data from a device</div>
                </div>
                <div class="feedback" id="mc-feedback-6" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 7: A "load" refers to:</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">A small amount of something</div>
                    <div class="option" onclick="selectOption(this, true)">A heavy or bulky thing being carried</div>
                    <div class="option" onclick="selectOption(this, false)">A unit of measurement</div>
                    <div class="option" onclick="selectOption(this, false)">An electrical circuit</div>
                </div>
                <div class="feedback" id="mc-feedback-7" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 8: "Light" means:</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">Heavy and difficult to move</div>
                    <div class="option" onclick="selectOption(this, true)">Not heavy; of little weight</div>
                    <div class="option" onclick="selectOption(this, false)">Dark and gloomy</div>
                    <div class="option" onclick="selectOption(this, false)">Bright and illuminating</div>
                </div>
                <div class="feedback" id="mc-feedback-8" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 9: "Worth it" means:</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">Too expensive for the value</div>
                    <div class="option" onclick="selectOption(this, true)">Good enough to justify the effort or cost</div>
                    <div class="option" onclick="selectOption(this, false)">Not valuable</div>
                    <div class="option" onclick="selectOption(this, false)">Questionable value</div>
                </div>
                <div class="feedback" id="mc-feedback-9" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 10: "DIY" stands for:</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">Digital Interface Yield</div>
                    <div class="option" onclick="selectOption(this, true)">Do It Yourself</div>
                    <div class="option" onclick="selectOption(this, false)">Department of Interior Yearning</div>
                    <div class="option" onclick="selectOption(this, false)">Design Initiative Yonder</div>
                </div>
                <div class="feedback" id="mc-feedback-10" style="display: none;"></div>
            </div>
        </div>
    </div>

    <script>
        let score = 0;
        let selectedWord = null;
        let selectedMeaning = null;
        let matchedPairs = [];

        function showSection(sectionId) {
            // Hide all sections
            document.querySelectorAll('.game-section').forEach(section => {
                section.classList.remove('active');
            });
            
            // Remove active class from all buttons
            document.querySelectorAll('.nav-btn').forEach(btn => {
                btn.classList.remove('active');
            });
            
            // Show selected section
            document.getElementById(sectionId).classList.add('active');
            
            // Add active class to clicked button
            event.target.classList.add('active');
        }

        function checkFillBlanks() {
            const blanks = document.querySelectorAll('.fill-blank');
            let correctCount = 0;
            
            blanks.forEach((blank, index) => {
                const userAnswer = blank.value.toLowerCase().trim();
                const correctAnswer = blank.dataset.answer.toLowerCase();
                
                if (userAnswer === correctAnswer) {
                    blank.classList.remove('incorrect');
                    blank.classList.add('correct');
                    correctCount++;
                } else {
                    blank.classList.remove('correct');
                    blank.classList.add('incorrect');
                }
                
                // Show feedback for each question
                const feedback = document.getElementById(`feedback-${index+1}`);
                if (userAnswer === correctAnswer) {
                    feedback.textContent = '✅ Correct!';
                    feedback.className = 'feedback correct';
                } else {
                    feedback.textContent = `❌ Incorrect. The correct answer is: "${blank.dataset.answer}"`;
                    feedback.className = 'feedback incorrect';
                }
                feedback.style.display = 'block';
            });
            
            updateScore();
        }

        function selectMatch(element) {
            if (element.classList.contains('matched')) return;
            
            if (element.dataset.word) {
                // Word selected
                if (selectedWord) selectedWord.classList.remove('selected');
                selectedWord = element;
                element.classList.add('selected');
            } else {
                // Meaning selected
                if (selectedMeaning) selectedMeaning.classList.remove('selected');
                selectedMeaning = element;
                element.classList.add('selected');
            }
            
            // Check if we have both word and meaning selected
            if (selectedWord && selectedMeaning) {
                checkMatch();
            }
        }

        function checkMatch() {
            const feedback = document.getElementById('matching-feedback');
            
            if (selectedWord.dataset.word === selectedMeaning.dataset.meaning) {
                // Correct match
                selectedWord.classList.remove('selected');
                selectedWord.classList.add('matched');
                selectedMeaning.classList.remove('selected');
                selectedMeaning.classList.add('matched');
                
                matchedPairs.push(selectedWord.dataset.word);
                
                feedback.textContent = '✅ Correct match!';
                feedback.className = 'feedback correct';
                
                // Check if all matches are complete
                if (matchedPairs.length === 10) {
                    feedback.textContent = '🎉 Congratulations! You matched all terms correctly!';
                }
            } else {
                // Incorrect match
                feedback.textContent = '❌ Incorrect match. Try again.';
                feedback.className = 'feedback incorrect';
            }
            
            feedback.style.display = 'block';
            selectedWord = null;
            selectedMeaning = null;
            
            updateScore();
        }

        function selectOption(element, isCorrect) {
            // Remove selection from all options in this question
            const options = element.parentElement.querySelectorAll('.option');
            options.forEach(opt => {
                opt.classList.remove('selected');
                opt.classList.remove('correct');
                opt.classList.remove('incorrect');
            });
            
            // Mark the selected option
            element.classList.add('selected');
            
            const questionNumber = element.closest('.question').querySelector('h3').textContent.match(/\d+/)[0];
            const feedback = document.getElementById(`mc-feedback-${questionNumber}`);
            
            if (isCorrect) {
                element.classList.add('correct');
                feedback.textContent = '✅ Correct!';
                feedback.className = 'feedback correct';
            } else {
                element.classList.add('incorrect');
                feedback.textContent = '❌ Incorrect. Try again.';
                feedback.className = 'feedback incorrect';
                
                // Show the correct answer
                options.forEach(opt => {
                    if (opt.onclick.toString().includes('true')) {
                        opt.classList.add('correct');
                    }
                });
            }
            
            feedback.style.display = 'block';
            updateScore();
        }

        function updateScore() {
            // Calculate score for fill-in-the-blank
            let fillScore = 0;
            document.querySelectorAll('.fill-blank.correct').forEach(blank => {
                if (!blank.classList.contains('counted')) {
                    fillScore++;
                    blank.classList.add('counted');
                }
            });
            
            // Calculate score for matching (each pair is 1 point)
            const matchScore = matchedPairs.length;
            
            // Calculate score for multiple choice (each correct is 1 point)
            let mcScore = 0;
            document.querySelectorAll('.option.correct.selected').forEach(opt => {
                mcScore++;
            });
            
            // Total score
            score = fillScore + matchScore + mcScore;
            document.getElementById('score').textContent = score;
        }
    </script>
</body>
</html>
