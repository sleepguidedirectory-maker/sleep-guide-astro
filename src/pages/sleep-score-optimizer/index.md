---
// src/pages/sleep-score-optimizer.astro
---
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Sleep Score Optimizer — Find Your Sleep Score | SleepGuide.com.au</title>
  <meta name="description" content="Take our free 2-minute Australian sleep quiz and get a personalised sleep score with expert recommendations on mattresses, pillows and sleep habits." />
  <link rel="preconnect" href="https://fonts.googleapis.com" />
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
  <link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,600;0,700;1,400&family=DM+Sans:opsz,wght@9..40,300;9..40,400;9..40,500&display=swap" rel="stylesheet" />
  <style>
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
    :root {
      --navy: #1B2B4B;
      --gold: #C49A45;
      --cream: #FAF8F3;
      --warm: #F2EDE3;
      --muted: #6B7B8A;
      --white: #ffffff;
      --green: #2D6A4F;
      --amber: #B7791F;
      --red: #9B2C2C;
    }
    body { font-family: 'DM Sans', sans-serif; background: var(--cream); color: var(--navy); line-height: 1.6; min-height: 100vh; }
    a { text-decoration: none; color: inherit; }

    /* NAV */
    nav { background: var(--navy); padding: 1rem 2rem; display: flex; justify-content: space-between; align-items: center; }
    .nav-logo { font-family: 'Playfair Display', serif; font-size: 1.2rem; color: var(--cream); font-weight: 600; }
    .nav-logo span { color: var(--gold); }
    .nav-links { display: flex; gap: 1.8rem; list-style: none; }
    .nav-links a { font-size: 0.85rem; color: rgba(250,248,243,0.7); transition: color 0.2s; }
    .nav-links a:hover { color: var(--gold); }
    @media (max-width: 640px) { .nav-links { display: none; } }

    /* HERO */
    .quiz-hero { background: var(--navy); padding: 3rem 2rem; text-align: center; position: relative; overflow: hidden; }
    .quiz-hero::before { content: ''; position: absolute; top: -80px; left: -80px; width: 280px; height: 280px; border-radius: 50%; background: rgba(196,154,69,0.06); }
    .quiz-hero::after { content: ''; position: absolute; bottom: -60px; right: -60px; width: 200px; height: 200px; border-radius: 50%; background: rgba(196,154,69,0.04); }
    .hero-tag { display: inline-block; font-size: 0.68rem; font-weight: 500; letter-spacing: 2px; text-transform: uppercase; color: var(--gold); border: 1px solid rgba(196,154,69,0.35); padding: 5px 14px; border-radius: 20px; margin-bottom: 1.2rem; }
    .quiz-hero h1 { font-family: 'Playfair Display', serif; font-size: clamp(1.8rem, 4vw, 2.6rem); font-weight: 700; color: var(--cream); line-height: 1.2; margin-bottom: 1rem; }
    .quiz-hero h1 em { color: var(--gold); font-style: italic; }
    .quiz-hero p { font-size: 0.95rem; color: rgba(250,248,243,0.65); font-weight: 300; max-width: 460px; margin: 0 auto 1.5rem; line-height: 1.75; }
    .hero-stats { display: flex; justify-content: center; gap: 2.5rem; flex-wrap: wrap; }
    .hero-stat { text-align: center; }
    .hero-stat strong { display: block; font-size: 1.4rem; font-weight: 600; color: var(--gold); font-family: 'Playfair Display', serif; }
    .hero-stat span { font-size: 0.75rem; color: rgba(250,248,243,0.5); }

    /* QUIZ CONTAINER */
    .quiz-outer { max-width: 680px; margin: 0 auto; padding: 3rem 1.5rem 5rem; }

    /* PROGRESS */
    .progress-wrap { margin-bottom: 2.5rem; }
    .progress-header { display: flex; justify-content: space-between; align-items: center; margin-bottom: 0.6rem; }
    .progress-label { font-size: 0.8rem; color: var(--muted); font-weight: 500; }
    .progress-count { font-size: 0.8rem; color: var(--gold); font-weight: 500; }
    .progress-bar { height: 4px; background: rgba(27,43,75,0.1); border-radius: 4px; overflow: hidden; }
    .progress-fill { height: 100%; background: var(--gold); border-radius: 4px; transition: width 0.5s ease; }

    /* QUESTION CARD */
    .question-card { background: var(--white); border-radius: 16px; border: 1px solid rgba(27,43,75,0.08); padding: 2.5rem; box-shadow: 0 4px 24px rgba(27,43,75,0.06); animation: slideIn 0.35s ease; }
    @keyframes slideIn { from { opacity: 0; transform: translateY(12px); } to { opacity: 1; transform: translateY(0); } }
    .q-number { font-size: 0.7rem; font-weight: 500; letter-spacing: 2px; text-transform: uppercase; color: var(--gold); margin-bottom: 0.8rem; }
    .q-text { font-family: 'Playfair Display', serif; font-size: clamp(1.1rem, 2.5vw, 1.35rem); font-weight: 600; color: var(--navy); line-height: 1.4; margin-bottom: 0.5rem; }
    .q-sub { font-size: 0.85rem; color: var(--muted); margin-bottom: 2rem; font-weight: 300; }

    /* OPTIONS */
    .options { display: flex; flex-direction: column; gap: 10px; }
    .option-btn {
      display: flex; align-items: center; gap: 14px;
      background: var(--cream); border: 1.5px solid rgba(27,43,75,0.1);
      border-radius: 10px; padding: 1rem 1.2rem;
      cursor: pointer; transition: all 0.2s; text-align: left;
      font-family: 'DM Sans', sans-serif; font-size: 0.92rem; color: var(--navy);
      width: 100%;
    }
    .option-btn:hover { border-color: var(--gold); background: rgba(196,154,69,0.06); transform: translateX(3px); }
    .option-btn.selected { border-color: var(--gold); background: rgba(196,154,69,0.1); color: var(--navy); }
    .option-icon { font-size: 1.1rem; flex-shrink: 0; width: 28px; text-align: center; }
    .option-text { flex: 1; }
    .option-label { font-weight: 500; display: block; }
    .option-desc { font-size: 0.78rem; color: var(--muted); font-weight: 300; margin-top: 2px; }

    /* NAV BUTTONS */
    .q-nav { display: flex; justify-content: space-between; align-items: center; margin-top: 2rem; }
    .btn-back { background: transparent; border: 1.5px solid rgba(27,43,75,0.15); color: var(--muted); padding: 10px 22px; border-radius: 8px; font-size: 0.85rem; cursor: pointer; font-family: inherit; transition: all 0.2s; }
    .btn-back:hover { border-color: var(--navy); color: var(--navy); }
    .btn-next { background: var(--gold); color: var(--navy); border: none; padding: 11px 28px; border-radius: 8px; font-size: 0.9rem; font-weight: 600; cursor: pointer; font-family: inherit; transition: opacity 0.2s; }
    .btn-next:hover { opacity: 0.88; }
    .btn-next:disabled { opacity: 0.35; cursor: not-allowed; }

    /* RESULTS */
    .results-card { background: var(--white); border-radius: 16px; border: 1px solid rgba(27,43,75,0.08); padding: 2.5rem; box-shadow: 0 4px 24px rgba(27,43,75,0.06); animation: slideIn 0.4s ease; }
    .results-header { text-align: center; margin-bottom: 2.5rem; }
    .score-ring-wrap { margin: 0 auto 1.5rem; width: 130px; height: 130px; position: relative; }
    .score-ring-wrap svg { transform: rotate(-90deg); }
    .score-number { position: absolute; inset: 0; display: flex; flex-direction: column; align-items: center; justify-content: center; }
    .score-num { font-family: 'Playfair Display', serif; font-size: 2.2rem; font-weight: 700; line-height: 1; }
    .score-max { font-size: 0.7rem; color: var(--muted); }
    .score-label { font-size: 0.75rem; font-weight: 500; letter-spacing: 1.5px; text-transform: uppercase; margin-top: 2px; }
    .results-header h2 { font-family: 'Playfair Display', serif; font-size: 1.6rem; font-weight: 700; color: var(--navy); margin-bottom: 0.5rem; }
    .results-header p { font-size: 0.92rem; color: var(--muted); font-weight: 300; line-height: 1.7; max-width: 420px; margin: 0 auto; }

    /* RESULT SECTIONS */
    .result-sections { display: flex; flex-direction: column; gap: 1.2rem; margin-bottom: 2rem; }
    .result-section { border-radius: 12px; padding: 1.4rem; border: 1px solid; }
    .result-section.good { background: rgba(45,106,79,0.06); border-color: rgba(45,106,79,0.2); }
    .result-section.warn { background: rgba(183,121,31,0.06); border-color: rgba(183,121,31,0.2); }
    .result-section.alert { background: rgba(155,44,44,0.06); border-color: rgba(155,44,44,0.2); }
    .rs-header { display: flex; align-items: center; gap: 10px; margin-bottom: 0.6rem; }
    .rs-icon { font-size: 1rem; }
    .rs-title { font-weight: 500; font-size: 0.9rem; }
    .result-section.good .rs-title { color: var(--green); }
    .result-section.warn .rs-title { color: var(--amber); }
    .result-section.alert .rs-title { color: var(--red); }
    .rs-text { font-size: 0.85rem; color: #3A4A5C; line-height: 1.65; font-weight: 300; }

    /* RECOMMENDATIONS */
    .recommendations { margin-bottom: 2rem; }
    .rec-title { font-family: 'Playfair Display', serif; font-size: 1.1rem; font-weight: 600; color: var(--navy); margin-bottom: 1rem; }
    .rec-cards { display: grid; grid-template-columns: 1fr 1fr; gap: 12px; }
    @media (max-width: 500px) { .rec-cards { grid-template-columns: 1fr; } }
    .rec-card { background: var(--cream); border: 1px solid rgba(27,43,75,0.1); border-radius: 10px; padding: 1.1rem; transition: box-shadow 0.2s, transform 0.2s; }
    .rec-card:hover { box-shadow: 0 4px 16px rgba(27,43,75,0.1); transform: translateY(-2px); }
    .rec-card a { display: block; }
    .rec-tag { font-size: 0.65rem; font-weight: 500; letter-spacing: 1.5px; text-transform: uppercase; color: var(--gold); margin-bottom: 0.4rem; }
    .rec-card h4 { font-size: 0.88rem; font-weight: 500; color: var(--navy); line-height: 1.4; margin-bottom: 0.3rem; }
    .rec-card p { font-size: 0.78rem; color: var(--muted); font-weight: 300; line-height: 1.5; }
    .rec-arrow { font-size: 0.78rem; color: var(--gold); margin-top: 0.5rem; display: block; }

    /* SHARE / RETRY */
    .result-actions { display: flex; gap: 12px; flex-wrap: wrap; }
    .btn-share { flex: 1; min-width: 140px; background: var(--navy); color: var(--cream); border: none; padding: 12px 20px; border-radius: 8px; font-size: 0.88rem; font-weight: 500; cursor: pointer; font-family: inherit; transition: opacity 0.2s; }
    .btn-share:hover { opacity: 0.88; }
    .btn-retry { flex: 1; min-width: 140px; background: transparent; color: var(--navy); border: 1.5px solid rgba(27,43,75,0.2); padding: 12px 20px; border-radius: 8px; font-size: 0.88rem; cursor: pointer; font-family: inherit; transition: border-color 0.2s; }
    .btn-retry:hover { border-color: var(--navy); }
    .share-confirm { font-size: 0.78rem; color: var(--green); text-align: center; margin-top: 0.5rem; display: none; }

    footer { background: #111E33; padding: 1.5rem 2rem; text-align: center; margin-top: 2rem; }
    .footer-links { display: flex; justify-content: center; gap: 1.8rem; flex-wrap: wrap; margin-bottom: 0.6rem; }
    .footer-links a { font-size: 0.78rem; color: rgba(250,248,243,0.4); }
    .footer-copy { font-size: 0.72rem; color: rgba(250,248,243,0.2); }
  </style>
</head>
<body>

<nav>
  <a href="/" class="nav-logo">Sleep<span>Guide</span><span style="color:rgba(250,248,243,0.3);font-size:0.65rem;font-family:'DM Sans',sans-serif;font-weight:300;margin-left:3px">.com.au</span></a>
  <ul class="nav-links">
    <li><a href="/best-mattress-in-australia-2026">Mattresses</a></li>
    <li><a href="/blog/best-anti-snore-pillow-australia">Pillows</a></li>
    <li><a href="/sleep-score-optimizer">Sleep Quiz</a></li>
    <li><a href="/about-us">About</a></li>
    <li><a href="/contact">Contact</a></li>
  </ul>
</nav>

<div class="quiz-hero">
  <div class="hero-tag">Free · 2 minutes · Australian</div>
  <h1>What's Your <em>Sleep Score?</em></h1>
  <p>Answer 8 quick questions and get a personalised sleep assessment with expert recommendations tailored for Australians.</p>
  <div class="hero-stats">
    <div class="hero-stat"><strong>8</strong><span>Questions</span></div>
    <div class="hero-stat"><strong>2 min</strong><span>To complete</span></div>
    <div class="hero-stat"><strong>100%</strong><span>Free</span></div>
  </div>
</div>

<div class="quiz-outer">
  <!-- PROGRESS -->
  <div class="progress-wrap" id="progress-wrap">
    <div class="progress-header">
      <span class="progress-label" id="progress-label">Question 1 of 8</span>
      <span class="progress-count" id="progress-pct">0% complete</span>
    </div>
    <div class="progress-bar"><div class="progress-fill" id="progress-fill" style="width:0%"></div></div>
  </div>

  <!-- QUIZ -->
  <div id="quiz-container"></div>
</div>

<footer>
  <div class="footer-links">
    <a href="/">Home</a>
    <a href="/about-us">About</a>
    <a href="/privacy-policy">Privacy Policy</a>
    <a href="/contact">Contact</a>
  </div>
  <p class="footer-copy">© 2026 SleepGuide.com.au · For informational purposes only, not medical advice.</p>
</footer>

<script>
const questions = [
  {
    id: 'hours',
    text: 'How many hours of sleep do you usually get on a weeknight?',
    sub: 'Think about the last few weeks on average.',
    options: [
      { icon: '😴', label: 'Less than 5 hours', desc: 'Severely sleep deprived', score: 0 },
      { icon: '🥱', label: '5–6 hours', desc: 'Below recommended amount', score: 3 },
      { icon: '😊', label: '7–8 hours', desc: 'Within the ideal range', score: 10 },
      { icon: '🛌', label: 'More than 9 hours', desc: 'Above average — may signal an issue', score: 6 },
    ]
  },
  {
    id: 'quality',
    text: 'How would you rate the quality of your sleep overall?',
    sub: 'Not just the hours, but how rested you feel.',
    options: [
      { icon: '😩', label: 'Very poor', desc: 'I wake up exhausted most days', score: 0 },
      { icon: '😕', label: 'Poor', desc: 'Often unrefreshed in the morning', score: 3 },
      { icon: '😐', label: 'Fair', desc: 'Some good nights, some bad', score: 6 },
      { icon: '😌', label: 'Good or excellent', desc: 'Usually wake up refreshed', score: 10 },
    ]
  },
  {
    id: 'falling-asleep',
    text: 'How long does it typically take you to fall asleep?',
    sub: 'From the moment you turn the light off.',
    options: [
      { icon: '⚡', label: 'Under 5 minutes', desc: 'May indicate sleep deprivation', score: 6 },
      { icon: '✅', label: '10–20 minutes', desc: 'Ideal range for most adults', score: 10 },
      { icon: '⏳', label: '20–45 minutes', desc: 'Slightly elevated — worth monitoring', score: 5 },
      { icon: '😤', label: 'Over 45 minutes', desc: 'Could indicate insomnia symptoms', score: 0 },
    ]
  },
  {
    id: 'waking',
    text: 'Do you wake up during the night?',
    sub: 'Not counting toilet trips for those over 50.',
    options: [
      { icon: '💤', label: 'Rarely or never', desc: 'Sleep through most nights', score: 10 },
      { icon: '🌙', label: 'Once or twice a week', desc: 'Occasional disturbance', score: 7 },
      { icon: '😔', label: 'Most nights', desc: 'Regular sleep fragmentation', score: 3 },
      { icon: '😰', label: 'Multiple times every night', desc: 'Significant disruption', score: 0 },
    ]
  },
  {
    id: 'position',
    text: 'What is your primary sleeping position?',
    sub: 'The position you spend most of the night in.',
    options: [
      { icon: '🛏', label: 'Side sleeper', desc: 'Most common — good for spine', score: 9 },
      { icon: '⬆️', label: 'Back sleeper', desc: 'Good posture, may increase snoring', score: 8 },
      { icon: '⬇️', label: 'Stomach sleeper', desc: 'Can strain neck and lower back', score: 4 },
      { icon: '🔄', label: 'Combination sleeper', desc: 'Move between positions', score: 7 },
    ]
  },
  {
    id: 'mattress',
    text: 'How old is your current mattress?',
    sub: 'Most mattresses should be replaced every 7–10 years.',
    options: [
      { icon: '✨', label: 'Less than 3 years old', desc: 'Still in good condition', score: 10 },
      { icon: '👍', label: '3–7 years old', desc: 'Getting towards mid-life', score: 7 },
      { icon: '⚠️', label: '7–10 years old', desc: 'Due for assessment soon', score: 4 },
      { icon: '🚨', label: 'Over 10 years old', desc: 'Likely affecting your sleep quality', score: 0 },
    ]
  },
  {
    id: 'screen',
    text: 'Do you use screens (phone, TV, laptop) in the hour before bed?',
    sub: 'Blue light suppresses melatonin production.',
    options: [
      { icon: '📵', label: 'Never — I avoid screens', desc: 'Great sleep hygiene habit', score: 10 },
      { icon: '📱', label: 'Occasionally', desc: 'A few times per week', score: 7 },
      { icon: '💻', label: 'Most nights', desc: 'Regular blue light exposure', score: 3 },
      { icon: '😬', label: 'Every single night in bed', desc: 'Significantly impacting sleep', score: 0 },
    ]
  },
  {
    id: 'daytime',
    text: 'How do you feel during the day?',
    sub: 'Your daytime energy is a key indicator of sleep quality.',
    options: [
      { icon: '⚡', label: 'Energised and alert', desc: 'Sleep is doing its job', score: 10 },
      { icon: '☕', label: 'Need coffee to function', desc: 'Relying on caffeine to cope', score: 4 },
      { icon: '😴', label: 'Tired most of the day', desc: 'Chronic fatigue symptoms', score: 2 },
      { icon: '🥱', label: 'Fall asleep unintentionally', desc: 'May indicate a sleep disorder', score: 0 },
    ]
  }
];

const recommendations = {
  mattress: {
    tag: 'Mattresses',
    title: 'Best Mattresses in Australia 2026',
    desc: 'Find the right support for your sleep style and budget',
    url: '/best-mattress-in-australia-2026'
  },
  pillow: {
    tag: 'Pillows',
    title: 'Best Pillows for Your Sleep Position',
    desc: 'The right pillow makes a bigger difference than you think',
    url: '/blog/best-contour-pillow-australia-2026'
  },
  snore: {
    tag: 'Pillows',
    title: 'Best Anti-Snore Pillows Australia',
    desc: 'Specially designed to keep airways open all night',
    url: '/blog/best-anti-snore-pillow-australia'
  },
  backpain: {
    tag: 'Back Pain',
    title: 'Best Mattress for Back Pain Australia',
    desc: 'Physio-approved picks for spinal support',
    url: '/blog/best-mattress-for-back-pain-australia-2026'
  },
  koala: {
    tag: 'Review',
    title: 'Koala Mattress Review 2026',
    desc: 'Australia\'s most popular mattress — is it worth it?',
    url: '/blog/koala-mattress-review-2026'
  },
  weighted: {
    tag: 'Sleep Science',
    title: 'The Science of Weighted Blankets',
    desc: 'Evidence-based guide to better sleep quality',
    url: '/blog/the-science-of-weighted-blankets'
  },
  latex: {
    tag: 'Pillows',
    title: 'Best Latex Pillow Australia 2026',
    desc: 'Natural, cool and durable — expert picks',
    url: '/blog/best-latex-pillow-australia-2026'
  }
};

let current = 0;
let answers = {};

function getScoreColor(score) {
  if (score >= 75) return '#2D6A4F';
  if (score >= 50) return '#B7791F';
  return '#9B2C2C';
}

function getScoreLabel(score) {
  if (score >= 75) return { label: 'Great Sleeper', type: 'good' };
  if (score >= 55) return { label: 'Average Sleeper', type: 'warn' };
  if (score >= 35) return { label: 'Poor Sleeper', type: 'warn' };
  return { label: 'Sleep Deprived', type: 'alert' };
}

function updateProgress() {
  const pct = Math.round((current / questions.length) * 100);
  document.getElementById('progress-fill').style.width = pct + '%';
  document.getElementById('progress-label').textContent = current < questions.length
    ? `Question ${current + 1} of ${questions.length}`
    : 'Results ready';
  document.getElementById('progress-pct').textContent = pct + '% complete';
}

function renderQuestion() {
  const q = questions[current];
  const selected = answers[q.id];
  const container = document.getElementById('quiz-container');
  container.innerHTML = `
    <div class="question-card">
      <div class="q-number">Question ${current + 1} of ${questions.length}</div>
      <div class="q-text">${q.text}</div>
      <div class="q-sub">${q.sub}</div>
      <div class="options">
        ${q.options.map((opt, i) => `
          <button class="option-btn${selected === i ? ' selected' : ''}" data-index="${i}">
            <span class="option-icon">${opt.icon}</span>
            <span class="option-text">
              <span class="option-label">${opt.label}</span>
              <span class="option-desc">${opt.desc}</span>
            </span>
          </button>
        `).join('')}
      </div>
      <div class="q-nav">
        <button class="btn-back" id="btn-back" ${current === 0 ? 'style="visibility:hidden"' : ''}>← Back</button>
        <button class="btn-next" id="btn-next" ${selected === undefined ? 'disabled' : ''}>
          ${current === questions.length - 1 ? 'See My Results →' : 'Next →'}
        </button>
      </div>
    </div>
  `;

  container.querySelectorAll('.option-btn').forEach(btn => {
    btn.addEventListener('click', () => {
      const idx = parseInt(btn.dataset.index);
      answers[questions[current].id] = idx;
      container.querySelectorAll('.option-btn').forEach(b => b.classList.remove('selected'));
      btn.classList.add('selected');
      document.getElementById('btn-next').disabled = false;
    });
  });

  document.getElementById('btn-next').addEventListener('click', () => {
    if (current < questions.length - 1) {
      current++;
      updateProgress();
      renderQuestion();
    } else {
      updateProgress();
      showResults();
    }
  });

  const backBtn = document.getElementById('btn-back');
  if (backBtn) {
    backBtn.addEventListener('click', () => {
      if (current > 0) { current--; updateProgress(); renderQuestion(); }
    });
  }
}

function showResults() {
  // Calculate score
  let totalScore = 0;
  let maxScore = 0;
  questions.forEach(q => {
    maxScore += 10;
    const answerIdx = answers[q.id];
    if (answerIdx !== undefined) totalScore += q.options[answerIdx].score;
  });
  const pct = Math.round((totalScore / maxScore) * 100);
  const color = getScoreColor(pct);
  const { label, type } = getScoreLabel(pct);

  // Build personalised feedback
  const mattressAge = answers['mattress'];
  const position = answers['position'];
  const daytime = answers['daytime'];
  const waking = answers['waking'];
  const screen = answers['screen'];
  const hours = answers['hours'];

  let goods = [], warns = [], alerts = [];

  if (hours === 2) goods.push('You\'re hitting the 7–8 hour sweet spot — this is the single biggest factor in sleep health.');
  if (answers['quality'] === 3) goods.push('Waking up refreshed is a strong sign your sleep cycles are completing properly.');
  if (answers['falling-asleep'] === 1) goods.push('Taking 10–20 minutes to fall asleep is the ideal range — not too quick, not too slow.');
  if (waking === 0) goods.push('Sleeping through the night without waking means your sleep architecture is solid.');
  if (screen === 0) goods.push('Avoiding screens before bed is one of the most impactful sleep hygiene habits you can have.');

  if (mattressAge === 2) warns.push('Your mattress is 7–10 years old. Most mattresses lose 20–30% of their support by this age, which directly affects sleep quality and back health.');
  if (mattressAge === 3) alerts.push('A mattress over 10 years old is almost certainly contributing to your sleep problems. This is the highest-priority change you can make.');
  if (position === 2) warns.push('Stomach sleeping puts your neck in an unnatural rotation for hours. A specialised pillow can reduce strain significantly.');
  if (daytime === 2 || daytime === 3) alerts.push('Chronic daytime fatigue and unintentional sleep episodes can be symptoms of sleep apnoea — worth discussing with your GP.');
  if (screen === 3) warns.push('Using screens in bed every night suppresses melatonin for up to 3 hours, delaying your ability to fall into deep sleep.');
  if (waking === 3) warns.push('Waking multiple times per night fragments your sleep cycles, reducing the restorative deep sleep and REM sleep you get.');
  if (hours === 0 || hours === 1) alerts.push('Consistently getting under 6 hours sleep is associated with serious long-term health risks including cardiovascular disease and metabolic issues.');

  // Pick recs
  let recKeys = [];
  if (mattressAge >= 2) recKeys.push('mattress', 'backpain');
  else recKeys.push('koala', 'mattress');
  if (position === 2) recKeys.push('pillow');
  else if (waking >= 2) recKeys.push('snore');
  else recKeys.push('pillow');
  if (screen >= 2 || daytime >= 2) recKeys.push('weighted');
  else recKeys.push('latex');
  recKeys = [...new Set(recKeys)].slice(0, 4);

  const circumference = 2 * Math.PI * 54;
  const offset = circumference - (pct / 100) * circumference;

  document.getElementById('progress-wrap').style.display = 'none';
  document.getElementById('quiz-container').innerHTML = `
    <div class="results-card">
      <div class="results-header">
        <div class="score-ring-wrap">
          <svg width="130" height="130" viewBox="0 0 130 130">
            <circle cx="65" cy="65" r="54" fill="none" stroke="#F2EDE3" stroke-width="10"/>
            <circle cx="65" cy="65" r="54" fill="none" stroke="${color}" stroke-width="10"
              stroke-dasharray="${circumference}" stroke-dashoffset="${offset}"
              stroke-linecap="round" style="transition: stroke-dashoffset 1.2s ease"/>
          </svg>
          <div class="score-number">
            <span class="score-num" style="color:${color}">${pct}</span>
            <span class="score-max">/100</span>
          </div>
        </div>
        <h2>Your sleep score is ${pct}/100</h2>
        <p>${pct >= 75 ? 'Your sleep habits are strong — some fine-tuning could make good sleep even better.' : pct >= 50 ? 'There\'s meaningful room to improve your sleep. The recommendations below are your best starting points.' : 'Your sleep needs attention. The good news: the right changes can transform how you feel within weeks.'}</p>
      </div>

      ${goods.length > 0 ? `
      <div class="result-sections">
        ${goods.map(g => `<div class="result-section good"><div class="rs-header"><span class="rs-icon">✓</span><span class="rs-title">What you\'re doing well</span></div><p class="rs-text">${g}</p></div>`).join('')}
        ${warns.map(w => `<div class="result-section warn"><div class="rs-header"><span class="rs-icon">⚠</span><span class="rs-title">Worth improving</span></div><p class="rs-text">${w}</p></div>`).join('')}
        ${alerts.map(a => `<div class="result-section alert"><div class="rs-header"><span class="rs-icon">!</span><span class="rs-title">Priority attention needed</span></div><p class="rs-text">${a}</p></div>`).join('')}
      </div>` : `
      <div class="result-sections">
        ${warns.map(w => `<div class="result-section warn"><div class="rs-header"><span class="rs-icon">⚠</span><span class="rs-title">Worth improving</span></div><p class="rs-text">${w}</p></div>`).join('')}
        ${alerts.map(a => `<div class="result-section alert"><div class="rs-header"><span class="rs-icon">!</span><span class="rs-title">Priority attention needed</span></div><p class="rs-text">${a}</p></div>`).join('')}
      </div>`}

      <div class="recommendations">
        <div class="rec-title">Your personalised reading list</div>
        <div class="rec-cards">
          ${recKeys.map(k => `
            <div class="rec-card">
              <a href="${recommendations[k].url}">
                <div class="rec-tag">${recommendations[k].tag}</div>
                <h4>${recommendations[k].title}</h4>
                <p>${recommendations[k].desc}</p>
                <span class="rec-arrow">Read guide →</span>
              </a>
            </div>
          `).join('')}
        </div>
      </div>

      <div class="result-actions">
        <button class="btn-share" id="btn-share">📋 Copy result to share</button>
        <button class="btn-retry" id="btn-retry">Retake quiz</button>
      </div>
      <p class="share-confirm" id="share-confirm">✓ Copied to clipboard!</p>
    </div>
  `;

  document.getElementById('btn-retry').addEventListener('click', () => {
    current = 0;
    answers = {};
    document.getElementById('progress-wrap').style.display = 'block';
    updateProgress();
    renderQuestion();
  });

  document.getElementById('btn-share').addEventListener('click', () => {
    const text = `My SleepGuide sleep score: ${pct}/100 (${label})\nTake the free Australian sleep quiz: https://sleepguide.com.au/sleep-score-optimizer`;
    navigator.clipboard.writeText(text).then(() => {
      document.getElementById('share-confirm').style.display = 'block';
      setTimeout(() => { document.getElementById('share-confirm').style.display = 'none'; }, 3000);
    });
  });
}

// Init
updateProgress();
renderQuestion();
</script>

</body>
</html>
