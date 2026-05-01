<!-- Sleep Score Calculator Widget -->
<div id="sleep-calculator-container" style="max-width: 400px; margin: 20px auto; padding: 20px; border-radius: 15px; background: #f9f9fb; box-shadow: 0 4px 15px rgba(0,0,0,0.1); font-family: sans-serif; color: #333;">
    <h2 style="text-align: center; color: #2c3e50; margin-top: 0;">Sleep Score Calculator</h2>
    
    <div style="margin-bottom: 15px;">
        <label style="display: block; margin-bottom: 5px; font-weight: bold;">Hours Slept:</label>
        <input type="number" id="hoursSlept" step="0.1" placeholder="e.g. 7.5" style="width: 100%; padding: 10px; border: 1px solid #ddd; border-radius: 8px; box-sizing: border-box;">
    </div>

    <div style="margin-bottom: 15px;">
        <label style="display: block; margin-bottom: 5px; font-weight: bold;">Minutes to fall asleep:</label>
        <input type="number" id="latency" placeholder="e.g. 20" style="width: 100%; padding: 10px; border: 1px solid #ddd; border-radius: 8px; box-sizing: border-box;">
    </div>

    <div style="margin-bottom: 20px;">
        <label style="display: block; margin-bottom: 5px; font-weight: bold;">Times woken up:</label>
        <input type="number" id="awakenings" placeholder="e.g. 1" style="width: 100%; padding: 10px; border: 1px solid #ddd; border-radius: 8px; box-sizing: border-box;">
    </div>

    <button onclick="calculateSleepScore()" style="width: 100%; padding: 12px; background-color: #4a90e2; color: white; border: none; border-radius: 8px; font-size: 16px; cursor: pointer; transition: background 0.3s;">
        Calculate My Score
    </button>

    <div id="sleepResult" style="margin-top: 20px; text-align: center; display: none;">
        <div style="font-size: 14px; color: #666;">Your Sleep Score</div>
        <div id="scoreDisplay" style="font-size: 48px; font-weight: bold; color: #4a90e2;">0</div>
        <p id="scoreMessage" style="font-weight: bold; margin-top: 5px;"></p>
    </div>
</div>

<script>
function calculateSleepScore() {
    const hours = parseFloat(document.getElementById('hoursSlept').value);
    const latency = parseInt(document.getElementById('latency').value);
    const awake = parseInt(document.getElementById('awakenings').value);

    if (isNaN(hours) || isNaN(latency) || isNaN(awake)) {
        alert("Please fill in all fields.");
        return;
    }

    // 1. Duration Score (Max 50)
    let durationPoints = 0;
    if (hours >= 7 && hours <= 9) {
        durationPoints = 50;
    } else {
        let diff = Math.min(Math.abs(7 - hours), Math.abs(9 - hours));
        durationPoints = Math.max(0, 50 - (diff * 12));
    }

    // 2. Latency Score (Max 25)
    let latencyPoints = 5;
    if (latency <= 20) latencyPoints = 25;
    else if (latency <= 45) latencyPoints = 15;

    // 3. Efficiency Score (Max 25)
    let efficiencyPoints = Math.max(0, 25 - (awake * 7));

    const totalScore = Math.round(durationPoints + latencyPoints + efficiencyPoints);

    // Display Logic
    const resultDiv = document.getElementById('sleepResult');
    const scoreDisplay = document.getElementById('scoreDisplay');
    const message = document.getElementById('scoreMessage');

    resultDiv.style.display = 'block';
    scoreDisplay.innerText = totalScore;

    if (totalScore >= 85) {
        message.innerText = "Excellent Rest!";
        message.style.color = "#27ae60";
    } else if (totalScore >= 70) {
        message.innerText = "Good Quality.";
        message.style.color = "#f39c12";
    } else {
        message.innerText = "Needs Improvement.";
        message.style.color = "#e74c3c";
    }
}
</script>
