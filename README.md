# hgzy-demo-
ঠিক আছে 😎 আমরা এখন একটা সরাসরি মোবাইল/ওয়েব অ্যাপের মতো Hgzy demo বানাতে পারি।
আমরা HTML + JavaScript + CSS ব্যবহার করব, যাতে তুমি এটাকে মোবাইল ব্রাউজারে অ্যাপের মতো ব্যবহার করতে পারো।

আমি একটি সম্পূর্ণ মোবাইল-ফ্রেন্ডলি অ্যাপ ভার্সন বানাচ্ছি:


---

Hgzy Mobile App Demo (hgzy_app.html)

<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Hgzy Mobile Demo App</title>
<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
<style>
    body {
        font-family: Arial, sans-serif;
        background: linear-gradient(to right, #1e3c72, #2a5298);
        color: #fff;
        text-align: center;
        padding: 10px;
    }
    h1 { margin-bottom: 10px; font-size: 1.8rem; }
    .balance { font-size: 1.5rem; margin: 10px 0; padding: 10px; background: rgba(0,0,0,0.3); border-radius: 10px; display: inline-block; min-width: 120px; }
    input, button { padding: 12px; font-size: 16px; margin: 5px; border-radius: 8px; border: none; }
    button { cursor: pointer; font-weight: bold; }
    button.place { background-color: #28a745; color: #fff; }
    button.cashout { background-color: #ffc107; color: #000; }
    #result { margin-top: 15px; font-size: 1.2rem; padding: 8px; background: rgba(0,0,0,0.3); border-radius: 8px; }
    canvas { background: rgba(0,0,0,0.2); border-radius: 10px; margin-top: 20px; width: 100%; }
</style>
</head>
<body>

<h1>Hgzy Mobile Demo</h1>
<div class="balance">Balance: $<span id="balance">1000</span></div>
<br>
<input type="number" id="bet" placeholder="Bet Amount">
<br>
<button class="place" onclick="placeBet()">Place Bet</button>
<button class="cashout" onclick="cashOut()">Cash Out</button>
<div id="result"></div>
<canvas id="crashChart" height="200"></canvas>

<script>
let balance = 1000;
let bet = 0;
let multiplier = 1;
let crashed = false;
let data = [];
let labels = [];
let betActive = false;

const ctx = document.getElementById('crashChart').getContext('2d');
const chart = new Chart(ctx, {
    type: 'line',
    data: { labels: labels, datasets: [{ label: 'Multiplier', data: data, borderColor: 'lime', borderWidth: 2, fill: false, tension: 0.4 }] },
    options: { responsive: true, scales: { x: { display: false }, y: { min: 1 } } }
});

function animateCrash() {
    multiplier = 1;
    data = [];
    labels = [];
    crashed = false;
    betActive = true;
    document.getElementById('result').innerText = '';
    
    let interval = setInterval(() => {
        if (crashed) { clearInterval(interval); return; }
        multiplier += Math.random() * 0.1;
        multiplier = Math.round(multiplier * 100)/100;
        data.push(multiplier);
        labels.push('');
        chart.data.labels = labels;
        chart.data.datasets[0].data = data;
        chart.update();

        if (Math.random() < 0.02) { // Random crash
            crashed = true;
            endRound(false);
            clearInterval(interval);
        }
    }, 100);
}

function placeBet() {
    if (betActive) { alert("Already running! Cash out or wait for crash."); return; }
    bet = parseInt(document.getElementById('bet').value);
    if (!bet || bet <= 0) { alert("Enter bet amount!"); return; }
    if (bet > balance) { alert("Not enough balance!"); return; }
    animateCrash();
}

function cashOut() {
    if (!betActive) { alert("Place a bet first!"); return; }
    endRound(true);
}

function endRound(cashedOut) {
    betActive = false;
    let earned = 0;
    if (cashedOut) {
        let cashMultiplier = multiplier.toFixed(2);
        earned = Math.round(bet * cashMultiplier);
        balance += earned - bet;
        document.getElementById('result').innerText = `🎉 Cash Out at ${cashMultiplier}x! Won $${earned}`;
    } else {
        balance -= bet;
        document.getElementById('result').innerText = `💥 Crashed at ${multiplier.toFixed(2)}x! Lost $${bet}`;
    }
    document.getElementById('balance').innerText = balance;
}
</script>

</body>
</html>


---

🔹 বৈশিষ্ট্যসমূহ

1. মোবাইল ফ্রেন্ডলি ডিজাইন


2. রিয়েল টাইম ক্র্যাশ গ্রাফ


3. Place Bet + Cash Out বাটন


4. Random crash points


5. ব্যালেন্স আপডেট এবং ফল দেখাবে




---

তুমি চাইলে আমি এটাকে আরও Hgzy-এর মতো গ্রাফিক্স + colorful animations + history log + sound effects সহ বানিয়ে দিতে পারি, যেন আসল অ্যাপের মতো অনুভূতি পাওয়া যায়।

চাও কি আমি সেটা করি?

