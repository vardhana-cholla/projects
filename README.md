<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Cancer Prediction</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 20px;
      padding: 0;
      background-color: #f4f4f9;
    }
    .container {
      max-width: 600px;
      margin: 0 auto;
      background: #ffffff;
      border-radius: 8px;
      padding: 20px;
      box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
    }
    h1 {
      text-align: center;
      color: #333;
    }
    label {
      font-weight: bold;
      display: block;
      margin-top: 10px;
    }
    input, select, button {
      width: 100%;
      padding: 10px;
      margin-top: 5px;
      border: 1px solid #ddd;
      border-radius: 4px;
    }
    button {
      background: #5cb85c;
      color: white;
      border: none;
      cursor: pointer;
      font-size: 16px;
    }
    button:hover {
      background: #4cae4c;
    }
    .result {
      margin-top: 20px;
      padding: 10px;
      background: #f0f8ff;
      border: 1px solid #cce5ff;
      border-radius: 4px;
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>Cancer Prediction</h1>
    <form id="predictionForm">
      <label for="feature1">Feature 1:</label>
      <input type="number" id="feature1" name="feature1" required>
      
      <label for="feature2">Feature 2:</label>
      <input type="number" id="feature2" name="feature2" required>

      <label for="feature3">Feature 3:</label>
      <input type="number" id="feature3" name="feature3" required>

      <label for="algorithm">Choose Algorithm:</label>
      <select id="algorithm" name="algorithm" required>
        <option value="random_forest">Random Forest</option>
        <option value="svc">Support Vector Classifier (SVC)</option>
        <option value="xgboost">XGBoost</option>
      </select>

      <button type="submit">Predict</button>
    </form>

    <div class="result" id="result" style="display: none;">
      <h3>Prediction Result:</h3>
      <p id="predictionOutput"></p>
    </div>
  </div>

  <script>
    document.getElementById("predictionForm").addEventListener("submit", async function(event) {
      event.preventDefault();

      const formData = {
        feature1: parseFloat(document.getElementById("feature1").value),
        feature2: parseFloat(document.getElementById("feature2").value),
        feature3: parseFloat(document.getElementById("feature3").value),
        algorithm: document.getElementById("algorithm").value,
      };

      try {
        const response = await fetch("http://localhost:5000/predict", {
          method: "POST",
          headers: {
            "Content-Type": "application/json",
          },
          body: JSON.stringify(formData),
        });

        const result = await response.json();
        document.getElementById("result").style.display = "block";
        document.getElementById("predictionOutput").innerText = result.prediction;
      } catch (error) {
        alert("Error occurred while predicting: " + error.message);
      }
    });
  </script>
</body>
</html>
# projects
