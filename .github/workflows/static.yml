<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Survey Form</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
        }

        .container {
            background: white;
            border-radius: 15px;
            box-shadow: 0 20px 40px rgba(0,0,0,0.1);
            padding: 40px;
            max-width: 500px;
            width: 100%;
            text-align: center;
        }

        .screen {
            display: none;
        }

        .screen.active {
            display: block;
        }

        h1 {
            color: #333;
            margin-bottom: 30px;
            font-size: 28px;
        }

        h2 {
            color: #555;
            margin-bottom: 20px;
            font-size: 24px;
        }

        .form-group {
            margin-bottom: 25px;
            text-align: left;
        }

        label {
            display: block;
            margin-bottom: 8px;
            font-weight: 600;
            color: #444;
        }

        input[type="text"], textarea {
            width: 100%;
            padding: 12px;
            border: 2px solid #ddd;
            border-radius: 8px;
            font-size: 16px;
            transition: border-color 0.3s ease;
        }

        input[type="text"]:focus, textarea:focus {
            outline: none;
            border-color: #667eea;
        }

        textarea {
            resize: vertical;
            min-height: 80px;
        }

        .radio-group {
            display: flex;
            flex-direction: column;
            gap: 10px;
        }

        .radio-option {
            display: flex;
            align-items: center;
            padding: 10px;
            border: 2px solid #eee;
            border-radius: 8px;
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .radio-option:hover {
            border-color: #667eea;
            background-color: #f8f9ff;
        }

        .radio-option input[type="radio"] {
            margin-right: 10px;
        }

        .btn {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            border: none;
            padding: 15px 30px;
            border-radius: 8px;
            font-size: 16px;
            font-weight: 600;
            cursor: pointer;
            transition: transform 0.2s ease;
            margin-top: 20px;
        }

        .btn:hover {
            transform: translateY(-2px);
        }

        .btn:disabled {
            opacity: 0.7;
            cursor: not-allowed;
            transform: none;
        }

        .loading-spinner {
            border: 4px solid #f3f3f3;
            border-top: 4px solid #667eea;
            border-radius: 50%;
            width: 50px;
            height: 50px;
            animation: spin 1s linear infinite;
            margin: 20px auto;
        }

        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }

        .success-icon {
            font-size: 60px;
            color: #4CAF50;
            margin-bottom: 20px;
        }

        .results {
            background: #f8f9fa;
            border: 1px solid #ddd;
            border-radius: 8px;
            padding: 20px;
            margin-top: 20px;
            text-align: left;
        }

        .result-item {
            margin-bottom: 15px;
            padding-bottom: 15px;
            border-bottom: 1px solid #eee;
        }

        .result-item:last-child {
            border-bottom: none;
            margin-bottom: 0;
            padding-bottom: 0;
        }

        .result-label {
            font-weight: 600;
            color: #333;
            margin-bottom: 5px;
        }

        .result-value {
            color: #666;
            word-wrap: break-word;
        }
    </style>
</head>
<body>
    <div class="container">
        <!-- Form Screen -->
        <div id="form-screen" class="screen active">
            <h1>Survey Form</h1>
            <form id="survey-form" action="https://formspree.io/f/YOUR_FORM_ID" method="POST">
                <div class="form-group">
                    <label for="question1">What is your favorite hobby and why?</label>
                    <textarea id="question1" name="question1" required placeholder="Please share your thoughts..."></textarea>
                </div>

                <div class="form-group">
                    <label for="question2">Describe a goal you're working towards:</label>
                    <textarea id="question2" name="question2" required placeholder="Tell us about your goal..."></textarea>
                </div>

                <div class="form-group">
                    <label>What best describes your current situation?</label>
                    <div class="radio-group">
                        <div class="radio-option">
                            <input type="radio" id="student" name="situation" value="student" required>
                            <label for="student">Student</label>
                        </div>
                        <div class="radio-option">
                            <input type="radio" id="professional" name="situation" value="professional" required>
                            <label for="professional">Working Professional</label>
                        </div>
                        <div class="radio-option">
                            <input type="radio" id="entrepreneur" name="situation" value="entrepreneur" required>
                            <label for="entrepreneur">Entrepreneur</label>
                        </div>
                        <div class="radio-option">
                            <input type="radio" id="other" name="situation" value="other" required>
                            <label for="other">Other</label>
                        </div>
                    </div>
                </div>

                <button type="submit" class="btn">Submit Survey</button>
            </form>
        </div>

        <!-- Loading Screen -->
        <div id="loading-screen" class="screen">
            <h2>Processing your responses...</h2>
            <div class="loading-spinner"></div>
            <p>Please wait while we save your information.</p>
        </div>

        <!-- Success Screen -->
        <div id="success-screen" class="screen">
            <div class="success-icon">✅</div>
            <h2>Thank you!</h2>
            <p>Your survey has been submitted successfully.</p>
            
            <div class="results" id="results">
                <!-- Results will be populated here -->
            </div>
            
            <button class="btn" onclick="resetForm()">Submit Another Response</button>
        </div>
    </div>

    <script>
        const formScreen = document.getElementById('form-screen');
        const loadingScreen = document.getElementById('loading-screen');
        const successScreen = document.getElementById('success-screen');
        const form = document.getElementById('survey-form');
        const resultsDiv = document.getElementById('results');

        form.addEventListener('submit', function(e) {
            e.preventDefault();
            
            // Show loading screen
            formScreen.classList.remove('active');
            loadingScreen.classList.add('active');
            
            // Collect form data
            const formData = new FormData(form);
            
            // Send to Formspree
            fetch(form.action, {
                method: 'POST',
                body: formData,
                headers: {
                    'Accept': 'application/json'
                }
            })
            .then(response => {
                if (response.ok) {
                    // Success - collect responses for display
                    const responses = {
                        question1: formData.get('question1'),
                        question2: formData.get('question2'),
                        situation: formData.get('situation')
                    };
                    
                    // Display results
                    displayResults(responses);
                    
                    // Show success screen
                    loadingScreen.classList.remove('active');
                    successScreen.classList.add('active');
                    
                    // Log to console
                    console.log('Survey submitted successfully:', responses);
                    
                } else {
                    throw new Error('Form submission failed');
                }
            })
            .catch(error => {
                console.error('Error:', error);
                loadingScreen.classList.remove('active');
                formScreen.classList.add('active');
                alert('Sorry, there was an error submitting your form. Please try again.');
            });
        });

        function displayResults(responses) {
            resultsDiv.innerHTML = `
                <div class="result-item">
                    <div class="result-label">Favorite Hobby Response:</div>
                    <div class="result-value">${responses.question1}</div>
                </div>
                <div class="result-item">
                    <div class="result-label">Goal Description:</div>
                    <div class="result-value">${responses.question2}</div>
                </div>
                <div class="result-item">
                    <div class="result-label">Current Situation:</div>
                    <div class="result-value">${responses.situation}</div>
                </div>
                <div class="result-item">
                    <div class="result-label">Submitted At:</div>
                    <div class="result-value">${new Date().toLocaleString()}</div>
                </div>
            `;
        }

        function resetForm() {
            form.reset();
            successScreen.classList.remove('active');
            formScreen.classList.add('active');
        }

        // Optional: Load previous responses on page load
        window.addEventListener('load', function() {
            const saved = localStorage.getItem('surveyResponses');
            if (saved) {
                console.log('Previous responses found:', JSON.parse(saved));
            }
        });
    </script>
</body>
</html>
