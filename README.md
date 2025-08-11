<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>Debt Counselling Calculator</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;600&display=swap');

  :root {
    --brand-orange: #f7931e;
    --bg-color: #fff;
    --text-color: #222;
    --input-border: #ccc;
    --input-focus-border: var(--brand-orange);
  }

  * {
    box-sizing: border-box;
  }

  body {
    background: var(--bg-color);
    color: var(--text-color);
    font-family: 'Inter', sans-serif;
    margin: 0;
    padding: 2rem;
    display: flex;
    justify-content: center;
    align-items: flex-start;
    min-height: 100vh;
  }

  .container {
    max-width: 420px;
    width: 100%;
    border: 1px solid #eee;
    padding: 2rem;
    border-radius: 12px;
    box-shadow: 0 6px 18px rgba(247, 147, 30, 0.15);
  }

  .logo {
    display: block;
    margin: 0 auto 1.5rem auto;
    max-width: 180px;
  }

  h1 {
    font-weight: 600;
    font-size: 1.8rem;
    text-align: center;
    margin-bottom: 2rem;
    color: var(--brand-orange);
  }

  label {
    display: block;
    font-weight: 600;
    margin-bottom: 0.5rem;
  }

  input[type="number"] {
    width: 100%;
    padding: 0.75rem 1rem;
    margin-bottom: 1.5rem;
    border: 1.5px solid var(--input-border);
    border-radius: 8px;
    font-size: 1rem;
    transition: border-color 0.3s ease;
  }

  input[type="number"]:focus {
    border-color: var(--input-focus-border);
    outline: none;
  }

  button {
    width: 100%;
    padding: 0.85rem;
    background: var(--brand-orange);
    border: none;
    border-radius: 8px;
    font-size: 1.1rem;
    font-weight: 600;
    color: #fff;
    cursor: pointer;
    transition: background 0.3s ease;
  }

  button:hover {
    background: #d87600;
  }

  .results {
    margin-top: 2rem;
    background: #fff8f1;
    border: 1.5px solid var(--brand-orange);
    border-radius: 10px;
    padding: 1.25rem 1.5rem;
    color: var(--brand-orange);
    font-weight: 600;
    font-size: 1.1rem;
    text-align: center;
    min-height: 3rem;
  }

  .footer {
    margin-top: 3rem;
    font-size: 0.85rem;
    text-align: center;
    color: #aaa;
  }
</style>
</head>
<body>
  <div class="container">
    <img src="https://i.postimg.cc/L55xpLsH/FINMED-LOGO-BLACKORANGE.png" alt="Finmed Logo" class="logo" />
    <h1>Debt Counselling Calculator</h1>
    <form id="calcForm" onsubmit="return calculatePayment();">
      <label for="fullAmount">Full Amount (ZAR)</label>
      <input type="number" id="fullAmount" name="fullAmount" min="0" step="0.01" required placeholder="e.g. 10000" />

      <label for="installment">Installment Amount (ZAR)</label>
      <input type="number" id="installment" name="installment" min="0" step="0.01" required placeholder="e.g. 1500" />

      <button type="submit">Calculate</button>
    </form>
    <div class="results" id="results"></div>
  </div>

<script>
  function calculatePayment() {
    const fullAmount = parseFloat(document.getElementById('fullAmount').value);
    const installment = parseFloat(document.getElementById('installment').value);

    if (installment === 0) {
      alert("Installment must be greater than zero.");
      return false;
    }
    // Calculate term in months before adding 2 months
    let termMonths = 
    Math.ceil((fullAmount + (installment * 2)) / installment);

   

    // Calculate total payable amount
    const totalPayable = installment * termMonths;

    const resultsDiv = document.getElementById('results');
    resultsDiv.innerHTML = `
      Payment Term: <strong>${termMonths} months</strong><br/>
      Total Payable: <strong>ZAR ${totalPayable.toFixed(2)}</strong>
    `;

    return false; // prevent form submission
  }
</script>
</body>
</html>
