# math-game-pwa2
<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>МатИгра</title>

  <script src="https://unpkg.com/react@18/umd/react.development.js"></script>
  <script src="https://unpkg.com/react-dom@18/umd/react-dom.development.js"></script>
  <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>

  <style>
    * {
      box-sizing: border-box;
    }

    body {
      margin: 0;
      font-family: Arial, sans-serif;
      background: linear-gradient(135deg, #2563eb, #1e40af);
      color: white;
      min-height: 100vh;
      display: flex;
      justify-content: center;
      align-items: center;
      padding: 20px;
    }

    .game {
      background: rgba(255,255,255,0.1);
      padding: 30px;
      border-radius: 20px;
      width: 100%;
      max-width: 400px;
      text-align: center;
      backdrop-filter: blur(10px);
      box-shadow: 0 10px 30px rgba(0,0,0,0.2);
    }

    h1 {
      margin-bottom: 20px;
    }

    .question {
      font-size: 40px;
      margin: 20px 0;
      font-weight: bold;
    }

    input {
      width: 100%;
      padding: 15px;
      border: none;
      border-radius: 10px;
      font-size: 20px;
      text-align: center;
      margin-bottom: 15px;
    }

    button {
      width: 100%;
      padding: 15px;
      border: none;
      border-radius: 10px;
      background: #22c55e;
      color: white;
      font-size: 18px;
      cursor: pointer;
      transition: 0.3s;
    }

    button:hover {
      background: #16a34a;
    }

    .score {
      margin-top: 20px;
      font-size: 20px;
    }

    .message {
      margin-top: 15px;
      font-size: 18px;
      font-weight: bold;
    }
  </style>
</head>
<body>
  <div id="root"></div>

  <script type="text/babel">
    function App() {
      const [num1, setNum1] = React.useState(0);
      const [num2, setNum2] = React.useState(0);
      const [answer, setAnswer] = React.useState("");
      const [score, setScore] = React.useState(0);
      const [message, setMessage] = React.useState("");

      React.useEffect(() => {
        generateQuestion();
      }, []);

      function generateQuestion() {
        const a = Math.floor(Math.random() * 10) + 1;
        const b = Math.floor(Math.random() * 10) + 1;

        setNum1(a);
        setNum2(b);
        setAnswer("");
      }

      function checkAnswer() {
        const correct = num1 + num2;

        if (Number(answer) === correct) {
          setScore(score + 1);
          setMessage("✅ Правильно!");
        } else {
          setMessage(`❌ Неправильно! Ответ: ${correct}`);
        }

        generateQuestion();
      }

      return (
        <div className="game">
          <h1>🧮 МатИгра</h1>

          <div className="question">
            {num1} + {num2}
          </div>

          <input
            type="number"
            value={answer}
            onChange={(e) => setAnswer(e.target.value)}
            placeholder="Введите ответ"
          />

          <button onClick={checkAnswer}>
            Проверить
          </button>

          <div className="score">
            🏆 Очки: {score}
          </div>

          <div className="message">
            {message}
          </div>
        </div>
      );
    }

    const root = ReactDOM.createRoot(document.getElementById("root"));
    root.render(<App />);
  </script>
</body>
</html>
