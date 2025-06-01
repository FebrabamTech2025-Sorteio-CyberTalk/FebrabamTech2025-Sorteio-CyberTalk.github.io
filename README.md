<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Security Verification Portal</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #0f1419 0%, #1a2332 50%, #2d3748 100%);
            color: #e2e8f0;
            min-height: 100vh;
            overflow-x: hidden;
        }

        .matrix-bg {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            opacity: 0.03;
            z-index: -1;
            font-family: 'Courier New', monospace;
            font-size: 14px;
            line-height: 14px;
            overflow: hidden;
        }

        .container {
            max-width: 800px;
            margin: 0 auto;
            padding: 2rem;
            position: relative;
            z-index: 1;
        }

        .header {
            text-align: center;
            margin-bottom: 3rem;
            padding: 2rem;
            background: rgba(45, 55, 72, 0.3);
            border-radius: 15px;
            border: 1px solid rgba(0, 255, 157, 0.2);
            box-shadow: 0 8px 32px rgba(0, 0, 0, 0.3);
            backdrop-filter: blur(10px);
        }

        .logo {
            width: 80px;
            height: 80px;
            margin: 0 auto 1rem;
            background: linear-gradient(45deg, #00ff9d, #00d4ff);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 2rem;
            animation: pulse 2s infinite;
        }

        @keyframes pulse {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.05); }
        }

        h1 {
            color: #00ff9d;
            font-size: 2.5rem;
            margin-bottom: 0.5rem;
            text-shadow: 0 0 20px rgba(0, 255, 157, 0.5);
        }

        .subtitle {
            color: #a0aec0;
            font-size: 1.2rem;
            font-weight: 300;
        }

        .main-message {
            background: rgba(0, 0, 0, 0.4);
            border-left: 4px solid #00ff9d;
            padding: 2rem;
            margin: 2rem 0;
            border-radius: 8px;
            box-shadow: 0 4px 20px rgba(0, 255, 157, 0.1);
        }

        .question {
            font-size: 1.8rem;
            color: #00d4ff;
            margin-bottom: 1rem;
            text-align: center;
        }

        .content {
            background: rgba(45, 55, 72, 0.5);
            padding: 2.5rem;
            border-radius: 12px;
            border: 1px solid rgba(0, 212, 255, 0.2);
            margin: 2rem 0;
            backdrop-filter: blur(5px);
        }

        .tips {
            display: grid;
            gap: 1.5rem;
            margin: 2rem 0;
        }

        .tip-item {
            background: rgba(0, 0, 0, 0.3);
            padding: 1.5rem;
            border-radius: 8px;
            border-left: 3px solid #00ff9d;
            transition: all 0.3s ease;
            cursor: pointer;
        }

        .tip-item:hover {
            background: rgba(0, 255, 157, 0.1);
            transform: translateX(5px);
        }

        .tip-title {
            color: #00ff9d;
            font-weight: 600;
            margin-bottom: 0.5rem;
            font-size: 1.1rem;
        }

        .tip-description {
            color: #cbd5e0;
            line-height: 1.6;
        }

        .stats {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 1.5rem;
            margin: 2rem 0;
        }

        .stat-card {
            background: rgba(0, 0, 0, 0.4);
            padding: 1.5rem;
            border-radius: 10px;
            text-align: center;
            border: 1px solid rgba(0, 212, 255, 0.3);
        }

        .stat-number {
            font-size: 2.5rem;
            color: #00d4ff;
            font-weight: bold;
            display: block;
        }

        .stat-label {
            color: #a0aec0;
            font-size: 0.9rem;
            margin-top: 0.5rem;
        }

        .footer {
            text-align: center;
            margin-top: 3rem;
            padding: 2rem;
            background: rgba(0, 0, 0, 0.3);
            border-radius: 10px;
            border: 1px solid rgba(0, 255, 157, 0.1);
        }

        .btn {
            display: inline-block;
            padding: 1rem 2rem;
            background: linear-gradient(45deg, #00ff9d, #00d4ff);
            color: #0f1419;
            text-decoration: none;
            border-radius: 25px;
            font-weight: 600;
            transition: all 0.3s ease;
            margin: 1rem 0.5rem;
            text-transform: uppercase;
            letter-spacing: 1px;
        }

        .btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 10px 25px rgba(0, 255, 157, 0.3);
        }

        .highlight {
            color: #00ff9d;
            font-weight: 600;
        }

        .warning-box {
            background: rgba(255, 193, 7, 0.1);
            border: 1px solid rgba(255, 193, 7, 0.3);
            border-radius: 8px;
            padding: 1.5rem;
            margin: 2rem 0;
        }

        .warning-title {
            color: #ffc107;
            font-weight: 600;
            margin-bottom: 0.5rem;
            display: flex;
            align-items: center;
            gap: 0.5rem;
        }

        @media (max-width: 768px) {
            .container {
                padding: 1rem;
            }
            
            h1 {
                font-size: 2rem;
            }
            
            .question {
                font-size: 1.5rem;
            }
            
            .stats {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>
<body>
    <div class="matrix-bg" id="matrix"></div>
    
    <div class="container">
        <div class="header">
            <div class="logo">🛡️</div>
            <h1>Security Checkpoint</h1>
            <div class="subtitle">Cybersecurity Awareness Portal</div>
        </div>

        <div class="main-message">
            <div class="question">🤔 Did you check the source before clicking?</div>
            <p style="text-align: center; color: #cbd5e0; font-size: 1.1rem; line-height: 1.6;">
                Great job participating in our security awareness exercise! You've just experienced a common scenario that happens every day in the digital world.
            </p>
        </div>

        <div class="content">
            <h2 style="color: #00d4ff; margin-bottom: 1.5rem; text-align: center;">🎯 What Just Happened?</h2>
            <p style="color: #e2e8f0; line-height: 1.7; font-size: 1.1rem; text-align: center;">
                You scanned a QR code and clicked a link without knowing exactly where it would take you. 
                This is a <span class="highlight">completely normal behavior</span> - most people do this daily! 
                The goal isn't to make you feel bad, but to help you develop <span class="highlight">security awareness habits</span>.
            </p>
        </div>

        <div class="stats">
            <div class="stat-card">
                <span class="stat-number">89%</span>
                <div class="stat-label">of people scan QR codes without hesitation</div>
            </div>
            <div class="stat-card">
                <span class="stat-number">3.4B</span>
                <div class="stat-label">phishing emails sent daily</div>
            </div>
            <div class="stat-card">
                <span class="stat-number">15sec</span>
                <div class="stat-label">average time to check a link</div>
            </div>
        </div>

        <div class="content">
            <h2 style="color: #00ff9d; margin-bottom: 1.5rem;">🛡️ Simple Security Habits</h2>
            <div class="tips">
                <div class="tip-item">
                    <div class="tip-title">🔍 Pause & Preview</div>
                    <div class="tip-description">Before clicking any QR code or link, take a moment to preview the URL. Most phones show you the destination before opening it.</div>
                </div>
                
                <div class="tip-item">
                    <div class="tip-title">🏢 Verify the Source</div>
                    <div class="tip-description">Ask yourself: "Do I know who created this QR code?" If it's from an unknown source, be extra cautious.</div>
                </div>
                
                <div class="tip-item">
                    <div class="tip-title">🌐 Check the Domain</div>
                    <div class="tip-description">Look for suspicious domains, misspellings, or unexpected redirects. Legitimate organizations use consistent, recognizable URLs.</div>
                </div>
                
                <div class="tip-item">
                    <div class="tip-title">🤝 When in Doubt, Ask</div>
                    <div class="tip-description">If you receive a QR code or link unexpectedly, verify it through another channel before clicking.</div>
                </div>
            </div>
        </div>

        <div class="warning-box">
            <div class="warning-title">
                ⚡ Remember: You're Not the Problem, You're the Solution
            </div>
            <p style="color: #e2e8f0; line-height: 1.6;">
                Cybersecurity isn't about perfect behavior - it's about building awareness and developing good habits. 
                Every time you pause to think before clicking, you're making the digital world safer for everyone.
            </p>
        </div>

        <div class="footer">
            <h3 style="color: #00ff9d; margin-bottom: 1rem;">🎓 Keep Learning</h3>
            <p style="color: #cbd5e0; margin-bottom: 1.5rem;">
                Security awareness is a journey, not a destination. Small habits make a big difference.
            </p>
            <a href="#" class="btn">Learn More Security Tips</a>
            <a href="#" class="btn">Take Security Quiz</a>
        </div>
    </div>

    <script>
        // Matrix-style background animation
        function createMatrix() {
            const matrix = document.getElementById('matrix');
            const chars = '01';
            const columns = Math.floor(window.innerWidth / 20);
            
            for (let i = 0; i < columns; i++) {
                const column = document.createElement('div');
                column.style.position = 'absolute';
                column.style.left = i * 20 + 'px';
                column.style.animationDelay = Math.random() * 2 + 's';
                column.style.animation = 'matrix 4s linear infinite';
                
                for (let j = 0; j < 50; j++) {
                    const char = document.createElement('div');
                    char.textContent = chars[Math.floor(Math.random() * chars.length)];
                    char.style.color = Math.random() > 0.5 ? '#00ff9d' : '#00d4ff';
                    column.appendChild(char);
                }
                
                matrix.appendChild(column);
            }
        }

        // Add CSS animation for matrix effect
        const style = document.createElement('style');
        style.textContent = `
            @keyframes matrix {
                0% { transform: translateY(-100vh); opacity: 1; }
                100% { transform: translateY(100vh); opacity: 0; }
            }
        `;
        document.head.appendChild(style);

        // Initialize matrix background
        createMatrix();

        // Add interactive hover effects
        document.querySelectorAll('.tip-item').forEach(item => {
            item.addEventListener('mouseenter', function() {
                this.style.boxShadow = '0 5px 20px rgba(0, 255, 157, 0.2)';
            });
            
            item.addEventListener('mouseleave', function() {
                this.style.boxShadow = 'none';
            });
        });

        // Smooth scroll for better UX
        document.querySelectorAll('a[href^="#"]').forEach(anchor => {
            anchor.addEventListener('click', function (e) {
                e.preventDefault();
                const target = document.querySelector(this.getAttribute('href'));
                if (target) {
                    target.scrollIntoView({
                        behavior: 'smooth'
                    });
                }
            });
        });
    </script>
</body>
</html>
