---
layout: default
title: 9M2PJU Zakat Calculator
---

<style>
  .calculator-container {
    max-width: 700px;
    margin: auto;
    padding: 1rem;
    background: #f9f9f9;
    border-radius: 8px;
    box-shadow: 0 2px 10px rgba(0,0,0,0.05);
  }

  h1 {
    text-align: center;
    color: #007b5e;
  }

  label {
    display: block;
    margin-top: 15px;
    font-weight: 600;
  }

  input {
    width: 100%;
    padding: 10px;
    margin-top: 5px;
    border-radius: 4px;
    border: 1px solid #ccc;
    box-sizing: border-box;
  }

  button {
    width: 100%;
    margin-top: 20px;
    padding: 12px;
    background: #007b5e;
    color: white;
    border: none;
    border-radius: 4px;
    font-size: 1rem;
    cursor: pointer;
  }

  button:hover {
    background: #005f47;
  }

  .results {
    margin-top: 20px;
    background: #e0f7f1;
    padding: 15px;
    border-radius: 5px;
    font-weight: 600;
  }

  @media (max-width: 600px) {
    .calculator-container {
      padding: 0.5rem;
    }

    input, button {
      font-size: 1rem;
    }
  }
</style>

<div class="calculator-container">
  <h1>🕌 9M2PJU Zakat Calculator</h1>
  <p>This calculator includes zakat on cash, gold, silver, business inventory, agricultural produce, and livestock.</p>

  <form id="zakatForm" onsubmit="event.preventDefault(); calculateZakat();">
    <label>💵 Cash (RM):
      <input type="number" id="cash" value="0" step="0.01" />
    </label>

    <label>🏅 Gold (grams):
      <input type="number" id="gold" value="0" step="0.01" />
    </label>
    <label>Gold price per gram (RM):
      <input type="number" id="goldPrice" value="0" step="0.01" readonly />
    </label>

    <label>🥈 Silver (grams):
      <input type="number" id="silver" value="0" step="0.01" />
    </label>
    <label>Silver price per gram (RM):
      <input type="number" id="silverPrice" value="0" step="0.01" readonly />
    </label>

    <label>📦 Business Inventory (RM):
      <input type="number" id="inventory" value="0" step="0.01" />
    </label>

    <label>🌾 Agricultural Produce (RM):
      <input type="number" id="agriculture" value="0" step="0.01" />
    </label>

    <label>🐐 Livestock Value (RM):
      <input type="number" id="livestock" value="0" step="0.01" />
    </label>

    <button type="submit">💰 Calculate Zakat</button>
  </form>

  <div id="results" class="results"></div>
</div>

<script>
  async function fetchPrices() {
    try {
      // Use placeholder API; replace with a real API if hosting allows CORS
      // Example fallback values
      document.getElementById('goldPrice').value = 350.00;
      document.getElementById('silverPrice').value = 3.50;
    } catch (e) {
      alert("Failed to fetch live prices. Using default values.");
      document.getElementById('goldPrice').value = 350.00;
      document.getElementById('silverPrice').value = 3.50;
    }
  }

  function calculateZakat() {
    const cash = parseFloat(document.getElementById('cash').value) || 0;
    const gold = parseFloat(document.getElementById('gold').value) || 0;
    const goldPrice = parseFloat(document.getElementById('goldPrice').value) || 0;
    const silver = parseFloat(document.getElementById('silver').value) || 0;
    const silverPrice = parseFloat(document.getElementById('silverPrice').value) || 0;
    const inventory = parseFloat(document.getElementById('inventory').value) || 0;
    const agriculture = parseFloat(document.getElementById('agriculture').value) || 0;
    const livestock = parseFloat(document.getElementById('livestock').value) || 0;

    const goldValue = gold * goldPrice;
    const silverValue = silver * silverPrice;
    const totalAssets = cash + goldValue + silverValue + inventory + agriculture + livestock;

    const nisabGold = 85 * goldPrice;
    const zakatRate = 0.025;

    let resultsHTML = `<p><strong>Total Assets:</strong> RM ${totalAssets.toFixed(2)}</p>`;
    resultsHTML += `<p><strong>Nisab (85g gold):</strong> RM ${nisabGold.toFixed(2)}</p>`;

    if (totalAssets >= nisabGold) {
      const zakatDue = totalAssets * zakatRate;
      resultsHTML += `<p style="color:green;"><strong>Zakat Due (2.5%): RM ${zakatDue.toFixed(2)}</strong></p>`;
    } else {
      resultsHTML += `<p style="color:red;"><strong>You are below the nisab threshold. No zakat due.</strong></p>`;
    }

    document.getElementById('results').innerHTML = resultsHTML;
  }

  window.onload = fetchPrices;
</script>
