[sword_battle.html](https://github.com/user-attachments/files/26041814/sword_battle.html)
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>SWORD TOKEN — Battle Arena</title>
<link href="https://fonts.googleapis.com/css2?family=Cinzel+Decorative:wght@400;700;900&family=Cinzel:wght@400;600;700&family=IM+Fell+English:ital@0;1&display=swap" rel="stylesheet">
<style>
  :root {
    --gold: #c9a84c;
    --gold-light: #f0d080;
    --gold-dark: #7a5c1e;
    --blood: #8b1a1a;
    --blood-bright: #d42020;
    --dark0: #0a0a0f;
    --dark1: #10101a;
    --dark2: #16162a;
    --dark3: #1e1e35;
    --dark4: #252540;
    --text-muted: #7070a0;
    --text-body: #c8c8e0;
    --success: #3ecf6e;
    --parchment: #e8d9b0;
  }

  * { box-sizing: border-box; margin: 0; padding: 0; }

  body {
    background: var(--dark0);
    color: var(--text-body);
    font-family: 'IM Fell English', Georgia, serif;
    min-height: 100vh;
    overflow-x: hidden;
  }

  /* === STARFIELD === */
  #stars {
    position: fixed; top: 0; left: 0; width: 100%; height: 100%;
    pointer-events: none; z-index: 0; overflow: hidden;
  }
  .star {
    position: absolute; background: #fff; border-radius: 50%;
    animation: twinkle var(--d, 3s) infinite alternate;
  }
  @keyframes twinkle { from { opacity: 0.1; } to { opacity: 0.9; } }

  /* === LAYOUT === */
  .wrap { position: relative; z-index: 1; max-width: 900px; margin: 0 auto; padding: 2rem 1.5rem 4rem; }

  /* === HEADER === */
  .site-header { text-align: center; padding: 3rem 0 2rem; }
  .site-header .eyebrow {
    font-family: 'Cinzel', serif; font-size: 11px; letter-spacing: 0.3em;
    color: var(--gold); text-transform: uppercase; margin-bottom: 0.75rem;
  }
  .site-title {
    font-family: 'Cinzel Decorative', serif; font-size: clamp(2.2rem, 6vw, 4rem);
    font-weight: 900; color: var(--gold-light);
    text-shadow: 0 0 60px rgba(201,168,76,0.4), 0 2px 0 var(--gold-dark);
    line-height: 1.1; margin-bottom: 0.5rem;
  }
  .site-sub {
    font-family: 'Cinzel', serif; font-size: 0.85rem; letter-spacing: 0.15em;
    color: var(--text-muted); margin-bottom: 2rem;
  }
  .divider {
    display: flex; align-items: center; gap: 1rem; margin: 1.5rem 0;
  }
  .divider-line { flex: 1; height: 1px; background: linear-gradient(90deg, transparent, var(--gold-dark), transparent); }
  .divider-diamond {
    width: 10px; height: 10px; background: var(--gold);
    transform: rotate(45deg); flex-shrink: 0;
  }

  /* === TOKEN INFO CARDS === */
  .token-grid {
    display: grid; grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
    gap: 1rem; margin: 2rem 0;
  }
  .token-card {
    background: var(--dark2); border: 1px solid var(--gold-dark);
    border-radius: 4px; padding: 1.25rem 1rem; text-align: center;
  }
  .token-card .tc-label {
    font-family: 'Cinzel', serif; font-size: 10px; letter-spacing: 0.2em;
    color: var(--text-muted); text-transform: uppercase; margin-bottom: 0.5rem;
  }
  .token-card .tc-value {
    font-family: 'Cinzel Decorative', serif; font-size: 1.1rem;
    color: var(--gold-light); font-weight: 700; word-break: break-all;
  }
  .token-card .tc-value.small { font-size: 0.65rem; }

  /* === SECTION TITLES === */
  .section-title {
    font-family: 'Cinzel', serif; font-size: 1.1rem; font-weight: 600;
    color: var(--gold); letter-spacing: 0.1em; text-transform: uppercase;
    margin: 2.5rem 0 1rem;
  }

  /* === BATTLE ARENA === */
  .arena {
    background: var(--dark1); border: 1px solid var(--gold-dark);
    border-radius: 6px; padding: 2rem; margin: 1.5rem 0;
    position: relative; overflow: hidden;
  }
  .arena::before {
    content: ''; position: absolute; inset: 0;
    background: radial-gradient(ellipse at center bottom, rgba(139,26,26,0.12) 0%, transparent 70%);
    pointer-events: none;
  }

  /* Fighter row */
  .fighters {
    display: grid; grid-template-columns: 1fr 80px 1fr;
    align-items: center; gap: 1rem; margin-bottom: 2rem;
  }
  .fighter { text-align: center; }
  .fighter-sprite {
    font-size: 3.5rem; display: block; margin: 0 auto 0.5rem;
    transition: transform 0.3s, filter 0.3s;
    filter: drop-shadow(0 0 8px rgba(201,168,76,0.3));
  }
  .fighter-name {
    font-family: 'Cinzel', serif; font-size: 0.8rem; letter-spacing: 0.12em;
    color: var(--gold); text-transform: uppercase;
  }
  .fighter-hp {
    font-family: 'Cinzel', serif; font-size: 0.7rem; color: var(--text-muted);
    margin-top: 4px;
  }
  .hp-bar {
    height: 6px; background: var(--dark4); border-radius: 3px;
    margin-top: 6px; overflow: hidden;
  }
  .hp-fill {
    height: 100%; border-radius: 3px;
    background: var(--success); transition: width 0.6s ease, background 0.3s;
  }
  .hp-fill.low { background: var(--blood-bright); }
  .vs-text {
    font-family: 'Cinzel Decorative', serif; font-size: 1.4rem;
    font-weight: 900; color: var(--blood-bright); text-align: center;
    text-shadow: 0 0 20px var(--blood);
  }

  /* Controls */
  .battle-controls {
    display: flex; flex-direction: column; gap: 1rem; margin-bottom: 1.5rem;
  }
  .control-row { display: flex; align-items: center; gap: 1rem; flex-wrap: wrap; }
  .control-label {
    font-family: 'Cinzel', serif; font-size: 0.75rem; letter-spacing: 0.1em;
    color: var(--text-muted); text-transform: uppercase; min-width: 130px;
  }
  .sword-input {
    background: var(--dark3); border: 1px solid var(--gold-dark); border-radius: 3px;
    color: var(--gold-light); font-family: 'Cinzel Decorative', serif; font-size: 1rem;
    padding: 0.4rem 0.75rem; width: 120px; text-align: center;
    outline: none;
  }
  .sword-input:focus { border-color: var(--gold); }
  .chance-badge {
    font-family: 'Cinzel', serif; font-size: 0.75rem; letter-spacing: 0.05em;
    padding: 0.3rem 0.75rem; border-radius: 3px; font-weight: 600;
  }
  .chance-badge.bad { background: rgba(139,26,26,0.3); color: #ff7070; border: 1px solid var(--blood); }
  .chance-badge.good { background: rgba(62,207,110,0.15); color: var(--success); border: 1px solid #2a8a4a; }

  /* Wallet bar */
  .wallet-bar {
    display: flex; align-items: center; gap: 0.75rem; flex-wrap: wrap;
    margin-bottom: 1.5rem; padding: 0.85rem 1rem;
    background: var(--dark3); border: 1px solid var(--gold-dark); border-radius: 4px;
  }
  .wallet-dot {
    width: 8px; height: 8px; border-radius: 50%; background: var(--text-muted); flex-shrink: 0;
    transition: background 0.3s;
  }
  .wallet-dot.connected { background: var(--success); box-shadow: 0 0 6px var(--success); }
  .wallet-dot.error     { background: var(--blood-bright); }
  .wallet-status {
    font-family: 'Cinzel', serif; font-size: 0.72rem; letter-spacing: 0.08em;
    color: var(--text-muted); flex: 1; min-width: 0; overflow: hidden;
    text-overflow: ellipsis; white-space: nowrap;
  }
  .wallet-status.connected { color: var(--success); }
  .wallet-status.error     { color: #ff7070; }
  .connect-btn {
    font-family: 'Cinzel', serif; font-size: 0.72rem; letter-spacing: 0.08em;
    padding: 0.35rem 0.9rem; cursor: pointer;
    background: transparent; border: 1px solid var(--gold-dark); border-radius: 3px;
    color: var(--gold); transition: all 0.2s; white-space: nowrap;
  }
  .connect-btn:hover { background: rgba(201,168,76,0.1); border-color: var(--gold); }
  .connect-btn:disabled { opacity: 0.4; cursor: not-allowed; }
  .sword-balance {
    font-family: 'Cinzel Decorative', serif; font-size: 0.7rem;
    color: var(--gold-light); white-space: nowrap;
  }

  /* Tx link */
  .tx-link {
    display: inline-block; margin-top: 0.5rem;
    font-family: 'Cinzel', serif; font-size: 0.72rem; letter-spacing: 0.06em;
    color: var(--gold); text-decoration: underline; cursor: pointer;
  }

  /* Fight button */
  .fight-btn {
    display: block; width: 100%; padding: 1rem;
    font-family: 'Cinzel Decorative', serif; font-size: 1.1rem; font-weight: 700;
    letter-spacing: 0.12em; text-transform: uppercase; cursor: pointer;
    background: linear-gradient(180deg, #9a2020 0%, #5a0e0e 100%);
    color: var(--gold-light); border: 1px solid #c03030; border-radius: 4px;
    transition: all 0.2s; text-shadow: 0 1px 0 rgba(0,0,0,0.5);
  }
  .fight-btn:hover:not(:disabled) {
    background: linear-gradient(180deg, #c02828 0%, #780f0f 100%);
    transform: translateY(-1px); box-shadow: 0 4px 20px rgba(139,26,26,0.4);
  }
  .fight-btn:active:not(:disabled) { transform: translateY(0); }
  .fight-btn:disabled { opacity: 0.5; cursor: not-allowed; }

  /* Battle Log */
  .battle-log {
    background: var(--dark0); border: 1px solid var(--dark4); border-radius: 4px;
    padding: 1rem; min-height: 160px; max-height: 220px; overflow-y: auto;
    font-size: 0.88rem; line-height: 1.7;
  }
  .log-line { margin: 0; padding: 2px 0; }
  .log-line.sys { color: var(--text-muted); font-style: italic; font-size: 0.78rem; }
  .log-line.atk { color: #ff9a9a; }
  .log-line.def { color: #9ad4ff; }
  .log-line.win { color: var(--success); font-weight: 700; font-size: 1rem; font-family: 'Cinzel', serif; }
  .log-line.lose { color: var(--blood-bright); font-weight: 700; font-size: 1rem; font-family: 'Cinzel', serif; }
  .log-line.gold { color: var(--gold-light); font-family: 'Cinzel', serif; }

  /* Result banner */
  .result-banner {
    display: none; text-align: center; padding: 1.5rem;
    border-radius: 4px; margin-top: 1rem; animation: fadeIn 0.5s ease;
  }
  @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: none; } }
  .result-banner.victory {
    display: block; background: rgba(62,207,110,0.1);
    border: 1px solid #2a8a4a; color: var(--success);
  }
  .result-banner.defeat {
    display: block; background: rgba(139,26,26,0.15);
    border: 1px solid var(--blood); color: #ff8080;
  }
  .result-title {
    font-family: 'Cinzel Decorative', serif; font-size: 1.5rem;
    font-weight: 900; margin-bottom: 0.5rem;
  }
  .result-sub { font-size: 0.9rem; opacity: 0.85; font-style: italic; }

  .hoard-label {
    font-family: 'Cinzel', serif; font-size: 9px; letter-spacing: 0.15em;
    color: var(--text-muted); text-transform: uppercase; margin-top: 8px;
  }
  .hoard-count {
    font-family: 'Cinzel Decorative', serif; font-size: 0.95rem; font-weight: 700;
    color: var(--blood-bright); margin-top: 2px;
    transition: color 0.4s, transform 0.3s;
  }
  .hoard-count.pulse {
    animation: hoard-pulse 0.5s ease;
  }
  @keyframes hoard-pulse {
    0%   { transform: scale(1);    color: var(--blood-bright); }
    40%  { transform: scale(1.35); color: #ff4444; }
    100% { transform: scale(1);    color: var(--blood-bright); }
  }

  /* Shake animation */
  @keyframes shake { 0%,100%{transform:translateX(0)} 20%{transform:translateX(-8px)} 40%{transform:translateX(8px)} 60%{transform:translateX(-5px)} 80%{transform:translateX(5px)} }
  .shaking { animation: shake 0.4s ease; }
  @keyframes glow-gold { 0%,100%{filter:drop-shadow(0 0 8px rgba(201,168,76,0.3))} 50%{filter:drop-shadow(0 0 24px rgba(201,168,76,0.8))} }
  .glowing { animation: glow-gold 0.6s ease; }

  /* === INSTRUCTIONS === */
  .instructions-box {
    background: var(--dark2); border: 1px solid var(--gold-dark); border-radius: 6px;
    padding: 1.75rem; margin: 1.5rem 0;
  }
  .step {
    display: flex; gap: 1.25rem; align-items: flex-start; margin-bottom: 1.5rem;
  }
  .step:last-child { margin-bottom: 0; }
  .step-num {
    font-family: 'Cinzel Decorative', serif; font-size: 1.2rem; font-weight: 900;
    color: var(--gold); min-width: 32px; line-height: 1.4;
  }
  .step-body { flex: 1; }
  .step-title {
    font-family: 'Cinzel', serif; font-size: 0.9rem; font-weight: 600;
    color: var(--gold-light); letter-spacing: 0.06em; margin-bottom: 0.4rem;
  }
  .step-desc { font-size: 0.88rem; color: var(--text-body); line-height: 1.65; }
  .code-pill {
    display: inline-block; background: var(--dark0); border: 1px solid var(--dark4);
    border-radius: 3px; padding: 0.15rem 0.5rem; font-family: 'Courier New', monospace;
    font-size: 0.78rem; color: #a0d0ff; word-break: break-all;
  }
  .highlight-row {
    background: rgba(201,168,76,0.08); border-left: 3px solid var(--gold);
    border-radius: 0 4px 4px 0; padding: 0.75rem 1rem; margin: 0.75rem 0;
    font-size: 0.85rem;
  }

  /* === CONTRACT CODE === */
  .code-block {
    background: var(--dark0); border: 1px solid var(--dark4); border-radius: 6px;
    padding: 1.5rem; overflow-x: auto; margin: 1.5rem 0;
    font-family: 'Courier New', monospace; font-size: 0.78rem; line-height: 1.7;
    color: #b0c8e8;
  }
  .kw { color: #c792ea; }
  .ty { color: #82aaff; }
  .str { color: #c3e88d; }
  .cm { color: #546078; font-style: italic; }
  .num { color: #f78c6c; }
  .fn { color: #82aaff; }

  /* === FOOTER === */
  .footer {
    text-align: center; margin-top: 4rem; padding-top: 2rem;
    border-top: 1px solid var(--dark4);
    font-family: 'Cinzel', serif; font-size: 0.7rem; letter-spacing: 0.1em;
    color: var(--text-muted);
  }

  /* Scrollbar */
  .battle-log::-webkit-scrollbar { width: 4px; }
  .battle-log::-webkit-scrollbar-track { background: var(--dark0); }
  .battle-log::-webkit-scrollbar-thumb { background: var(--gold-dark); border-radius: 2px; }

  /* responsive */
  @media(max-width: 500px) {
    .fighters { grid-template-columns: 1fr 50px 1fr; }
    .fighter-sprite { font-size: 2.5rem; }
    .vs-text { font-size: 1rem; }
    .control-label { min-width: 100px; font-size: 0.68rem; }
  }
</style>
</head>
<body>

<!-- Stars -->
<div id="stars"></div>

<div class="wrap">

  <!-- HEADER -->
  <header class="site-header">
    <div class="eyebrow">Sepolia Testnet &bull; ERC-20 Battle Token</div>
    <h1 class="site-title">&#x2694; SWORD</h1>
    <div class="site-sub">Token of Champions &bull; Vanquish the Monster. Claim the Spoils.</div>
    <div class="divider"><div class="divider-line"></div><div class="divider-diamond"></div><div class="divider-line"></div></div>
  </header>

  <!-- TOKEN DETAILS -->
  <div class="section-title">Token Details</div>
  <div class="token-grid">
    <div class="token-card">
      <div class="tc-label">Token Name</div>
      <div class="tc-value">SWORD</div>
    </div>
    <div class="token-card">
      <div class="tc-label">Total Supply</div>
      <div class="tc-value">1,000,000</div>
    </div>
    <div class="token-card">
      <div class="tc-label">Network</div>
      <div class="tc-value">Sepolia</div>
    </div>
    <div class="token-card">
      <div class="tc-label">Swords to Defeat Monster</div>
      <div class="tc-value">100</div>
    </div>
    <div class="token-card">
      <div class="tc-label">Victory Reward</div>
      <div class="tc-value">0.001 ETH</div>
    </div>
    <div class="token-card">
      <div class="tc-label">Deployed to</div>
      <div class="tc-value small">0xe549E983358dbCEC0f85CB59F9b7dCd35f058Ea7</div>
    </div>
  </div>

  <div class="divider"><div class="divider-line"></div><div class="divider-diamond"></div><div class="divider-line"></div></div>

  <!-- LIVE BATTLE DEMO -->
  <div class="section-title">&#x2694; Live Battle Simulator</div>
  <p style="font-size:0.88rem; color:var(--text-muted); margin-bottom:1rem;">
    Choose your sword count below. 100 or more swords gives a strong chance of victory. Under 100 swords and the monster has a 98% chance to crush you. Press <em>Enter the Arena</em> to watch the battle unfold.
  </p>

  <div class="arena" id="arena">

    <!-- Wallet Bar -->
    <div class="wallet-bar">
      <div class="wallet-dot" id="wallet-dot"></div>
      <div class="wallet-status" id="wallet-status">Not connected — MetaMask required</div>
      <div class="sword-balance" id="sword-balance" style="display:none"></div>
      <button class="connect-btn" id="connect-btn" onclick="connectWallet()">Connect Wallet</button>
    </div>

    <!-- Fighters -->
    <div class="fighters">
      <div class="fighter" id="fighter-player">
        <span class="fighter-sprite" id="sprite-player">&#x1F9DD;</span>
        <div class="fighter-name">Champion</div>
        <div class="fighter-hp" id="hp-player-text">100 HP</div>
        <div class="hp-bar"><div class="hp-fill" id="hp-player-fill" style="width:100%"></div></div>
      </div>
      <div class="vs-text">VS</div>
      <div class="fighter" id="fighter-monster">
        <span class="fighter-sprite" id="sprite-monster">&#x1F409;</span>
        <div class="fighter-name">The Wyrm</div>
        <div class="fighter-hp" id="hp-monster-text">100 HP</div>
        <div class="hp-bar"><div class="hp-fill" id="hp-monster-fill" style="width:100%"></div></div>
        <div class="hoard-label">Swords Collected</div>
        <div class="hoard-count" id="hoard-count">0 &#x2694;</div>
      </div>
    </div>

    <!-- Controls -->
    <div class="battle-controls">
      <div class="control-row">
        <span class="control-label">Swords to Send</span>
        <input type="number" class="sword-input" id="sword-count" value="50" min="1" max="1000000" />
        <span class="chance-badge bad" id="chance-badge">Monster wins 98%</span>
      </div>
    </div>

    <button class="fight-btn" id="fight-btn" onclick="startBattle()">&#x2694; Enter the Arena</button>

    <!-- Log -->
    <div style="margin-top:1.5rem;">
      <div class="section-title" style="margin-top:0; font-size:0.8rem;">Battle Chronicle</div>
      <div class="battle-log" id="battle-log">
        <p class="log-line sys">— Awaiting challenger to enter the arena... —</p>
      </div>
    </div>

    <!-- Result banner -->
    <div class="result-banner" id="result-banner">
      <div class="result-title" id="result-title"></div>
      <div class="result-sub" id="result-sub"></div>
    </div>

  </div>

  <div class="divider"><div class="divider-line"></div><div class="divider-diamond"></div><div class="divider-line"></div></div>

  <!-- INSTRUCTIONS -->
  <div class="section-title">How to Play — For Token Holders</div>
  <p style="font-size:0.85rem; color:var(--text-muted); margin-bottom:1rem; font-style:italic;">
    Prerequisites: You already hold SWORD tokens and have Sepolia ETH for gas.
  </p>

  <div class="instructions-box">
    <div class="step">
      <div class="step-num">I</div>
      <div class="step-body">
        <div class="step-title">Add the SWORD Token to Your Wallet</div>
        <div class="step-desc">
          In MetaMask (or any Web3 wallet), navigate to <em>Import Token</em> and paste the contract address:<br><br>
          <span class="code-pill">0xe549E983358dbCEC0f85CB59F9b7dCd35f058Ea7</span><br><br>
          Enter <strong>SWORD</strong> as the symbol and <strong>18</strong> as decimals. Your balance will appear immediately.
        </div>
      </div>
    </div>

    <div class="step">
      <div class="step-num">II</div>
      <div class="step-body">
        <div class="step-title">Approve the Contract to Spend Your Swords</div>
        <div class="step-desc">
          Before battling, you must authorize the battle contract to move your SWORD tokens. Call the <span class="code-pill">approve()</span> function on the SWORD token contract, passing the battle contract address and the amount you wish to stake (minimum 100 SWORD for victory odds in your favor).
        </div>
        <div class="highlight-row">
          Tip: Approve a larger amount once (e.g. 10,000 SWORD) so you do not need to re-approve every match.
        </div>
      </div>
    </div>

    <div class="step">
      <div class="step-num">III</div>
      <div class="step-body">
        <div class="step-title">Call <span class="code-pill">battle(uint256 swordAmount)</span></div>
        <div class="step-desc">
          Invoke the battle function on the contract, passing how many SWORD tokens you want to stake into the fight. The contract will:
          <ul style="margin:0.6rem 0 0 1.2rem; line-height:2;">
            <li>Transfer your swords to the contract</li>
            <li>If amount &lt; 100 — monster wins with <strong>98% chance</strong></li>
            <li>If amount &ge; 100 — player wins with <strong>98% chance</strong></li>
            <li>On victory: sends <strong>0.001 Sepolia ETH</strong> to your address</li>
          </ul>
        </div>
      </div>
    </div>

    <div class="step">
      <div class="step-num">IV</div>
      <div class="step-body">
        <div class="step-title">Verify the Outcome on Sepolia Etherscan</div>
        <div class="step-desc">
          After the transaction confirms, check Sepolia Etherscan for your wallet address. A <span class="code-pill">BattleResult</span> event will show whether you won or lost, the amount of SWORD staked, and any ETH reward sent back to you.
        </div>
        <div class="highlight-row">
          Etherscan Sepolia: <span class="code-pill">https://sepolia.etherscan.io/address/0xe549E983358dbCEC0f85CB59F9b7dCd35f058Ea7</span>
        </div>
      </div>
    </div>

    <div class="step">
      <div class="step-num">V</div>
      <div class="step-body">
        <div class="step-title">Repeat &amp; Accumulate Rewards</div>
        <div class="step-desc">
          Each battle is independent. Stack 100+ SWORD per fight and maintain your 98% win rate. Rewards of 0.001 Sepolia ETH are sent automatically with each victory — no manual claiming required.
        </div>
      </div>
    </div>
  </div>

  <div class="divider"><div class="divider-line"></div><div class="divider-diamond"></div><div class="divider-line"></div></div>

  <!-- SOLIDITY CONTRACT -->
  <div class="section-title">Solidity Smart Contract</div>
  <p style="font-size:0.85rem; color:var(--text-muted); margin-bottom:1rem; font-style:italic;">
    Deploy this contract on Sepolia using Remix IDE or Hardhat. Fund it with Sepolia ETH to pay out victors.
  </p>

  <div class="code-block"><pre>
<span class="cm">// SPDX-License-Identifier: MIT</span>
<span class="kw">pragma solidity</span> ^<span class="num">0.8.20</span>;

<span class="kw">import</span> <span class="str">"@openzeppelin/contracts/token/ERC20/ERC20.sol"</span>;
<span class="kw">import</span> <span class="str">"@openzeppelin/contracts/access/Ownable.sol"</span>;

<span class="cm">// ─────────────────────────────────────────────────────
//  SWORD Token — ERC20
// ─────────────────────────────────────────────────────</span>
<span class="kw">contract</span> <span class="ty">SwordToken</span> <span class="kw">is</span> <span class="ty">ERC20</span>, <span class="ty">Ownable</span> {
    <span class="kw">constructor</span>(<span class="ty">address</span> recipient) <span class="ty">ERC20</span>(<span class="str">"Sword"</span>, <span class="str">"SWORD"</span>) <span class="ty">Ownable</span>(msg.sender) {
        <span class="cm">// Mint 1,000,000 SWORD to the specified address</span>
        _mint(recipient, <span class="num">1_000_000</span> * <span class="num">10</span> ** decimals());
    }
}

<span class="cm">// ─────────────────────────────────────────────────────
//  Battle Arena Contract
// ─────────────────────────────────────────────────────</span>
<span class="kw">contract</span> <span class="ty">BattleArena</span> <span class="kw">is</span> <span class="ty">Ownable</span> {

    <span class="ty">SwordToken</span> <span class="kw">public immutable</span> sword;
    <span class="ty">uint256</span> <span class="kw">public constant</span> VICTORY_THRESHOLD = <span class="num">100</span> * <span class="num">10</span>**<span class="num">18</span>;
    <span class="ty">uint256</span> <span class="kw">public constant</span> REWARD_AMOUNT    = <span class="num">0.001</span> ether;

    <span class="kw">event</span> <span class="fn">BattleResult</span>(
        <span class="ty">address indexed</span> player,
        <span class="ty">uint256</span> swordsStaked,
        <span class="ty">bool</span> playerWon,
        <span class="ty">uint256</span> ethRewarded
    );

    <span class="kw">constructor</span>(<span class="ty">address</span> swordToken) <span class="ty">Ownable</span>(msg.sender) {
        sword = <span class="ty">SwordToken</span>(swordToken);
    }

    <span class="cm">/// @notice Fund the arena with Sepolia ETH for rewards</span>
    <span class="kw">receive</span>() <span class="kw">external payable</span> {}

    <span class="cm">/// @notice Enter battle. Stake swordAmount SWORD tokens.
    ///  &gt;= 100 SWORD: 98% chance player wins + 0.001 ETH reward
    ///  &lt; 100  SWORD: 98% chance monster wins (no reward)</span>
    <span class="kw">function</span> <span class="fn">battle</span>(<span class="ty">uint256</span> swordAmount) <span class="kw">external</span> {
        <span class="kw">require</span>(swordAmount > <span class="num">0</span>, <span class="str">"Stake at least 1 SWORD"</span>);
        sword.transferFrom(msg.sender, <span class="ty">address</span>(<span class="kw">this</span>), swordAmount);

        <span class="ty">uint256</span> rand = _pseudoRandom() % <span class="num">100</span>;

        <span class="ty">bool</span> playerWins;
        <span class="kw">if</span> (swordAmount >= VICTORY_THRESHOLD) {
            <span class="cm">// 98% win chance (rand 0–97)</span>
            playerWins = (rand < <span class="num">98</span>);
        } <span class="kw">else</span> {
            <span class="cm">// 2% win chance (rand 0–1)</span>
            playerWins = (rand < <span class="num">2</span>);
        }

        <span class="ty">uint256</span> ethSent = <span class="num">0</span>;
        <span class="kw">if</span> (playerWins && <span class="ty">address</span>(<span class="kw">this</span>).balance >= REWARD_AMOUNT) {
            ethSent = REWARD_AMOUNT;
            (<span class="ty">bool</span> ok,) = msg.sender.call{<span class="kw">value</span>: REWARD_AMOUNT}(<span class="str">""</span>);
            <span class="kw">require</span>(ok, <span class="str">"ETH transfer failed"</span>);
        }

        <span class="kw">emit</span> <span class="fn">BattleResult</span>(msg.sender, swordAmount, playerWins, ethSent);
    }

    <span class="cm">/// @dev Simple on-chain pseudo-randomness (not production-safe;
    ///      use Chainlink VRF for a production deployment)</span>
    <span class="kw">function</span> <span class="fn">_pseudoRandom</span>() <span class="kw">private view returns</span> (<span class="ty">uint256</span>) {
        <span class="kw">return</span> <span class="ty">uint256</span>(<span class="ty">keccak256</span>(<span class="ty">abi.encodePacked</span>(
            block.timestamp, block.prevrandao, msg.sender
        )));
    }

    <span class="cm">/// @notice Withdraw SWORD tokens collected from battles</span>
    <span class="kw">function</span> <span class="fn">withdrawSword</span>(<span class="ty">uint256</span> amount) <span class="kw">external</span> onlyOwner {
        sword.transfer(owner(), amount);
    }

    <span class="cm">/// @notice Withdraw ETH from arena (owner only)</span>
    <span class="kw">function</span> <span class="fn">withdrawEth</span>() <span class="kw">external</span> onlyOwner {
        (<span class="ty">bool</span> ok,) = owner().call{<span class="kw">value</span>: <span class="ty">address</span>(<span class="kw">this</span>).balance}(<span class="str">""</span>);
        <span class="kw">require</span>(ok, <span class="str">"Withdraw failed"</span>);
    }
}
  </pre></div>

  <!-- FOOTER -->
  <div class="footer">
    <p>SWORD Token &bull; Sepolia Testnet &bull; For demonstration purposes</p>
    <p style="margin-top:0.4rem;">Contract address: 0xe549E983358dbCEC0f85CB59F9b7dCd35f058Ea7</p>
  </div>

</div><!-- /wrap -->

<script src="https://cdnjs.cloudflare.com/ajax/libs/ethers/6.7.0/ethers.umd.min.js"></script>
<script>
  /* ── Stars ── */
  const starEl = document.getElementById('stars');
  for(let i=0;i<120;i++){
    const s=document.createElement('div'); s.className='star';
    const sz=Math.random()*2+0.5;
    s.style.cssText=`left:${Math.random()*100}%;top:${Math.random()*100}%;width:${sz}px;height:${sz}px;--d:${(Math.random()*4+2).toFixed(1)}s;animation-delay:${(Math.random()*5).toFixed(1)}s`;
    starEl.appendChild(s);
  }

  /* ── Constants ── */
  const SWORD_ADDRESS   = '0xe549E983358dbCEC0f85CB59F9b7dCd35f058Ea7';
  const MONSTER_ADDRESS = '0xe549E983358dbCEC0f85CB59F9b7dCd35f058Ea7'; // tokens sent here on monster win
  const SEPOLIA_CHAIN_ID = '0xaa36a7';
  const ERC20_ABI = [
    'function transfer(address to, uint256 amount) returns (bool)',
    'function balanceOf(address owner) view returns (uint256)',
    'function decimals() view returns (uint8)'
  ];

  /* ── State ── */
  let provider, signer, swordContract, walletAddress;
  let battling = false;
  let monsterHoard = 0;

  /* ── Chance badge ── */
  const swordInput  = document.getElementById('sword-count');
  const chanceBadge = document.getElementById('chance-badge');
  swordInput.addEventListener('input', ()=>{
    const v = parseInt(swordInput.value)||0;
    if(v>=100){ chanceBadge.textContent='Player wins 98%'; chanceBadge.className='chance-badge good'; }
    else       { chanceBadge.textContent='Monster wins 98%'; chanceBadge.className='chance-badge bad'; }
  });

  /* ── Wallet helpers ── */
  function setWalletUI(state, msg, balance){
    const dot  = document.getElementById('wallet-dot');
    const stat = document.getElementById('wallet-status');
    const bal  = document.getElementById('sword-balance');
    const btn  = document.getElementById('connect-btn');
    dot.className  = 'wallet-dot '+(state==='connected'?'connected':state==='error'?'error':'');
    stat.className = 'wallet-status '+(state==='connected'?'connected':state==='error'?'error':'');
    stat.textContent = msg;
    if(balance !== undefined){
      bal.style.display = 'block';
      bal.textContent   = balance.toLocaleString()+' ⚔ SWORD';
    }
    if(state==='connected'){ btn.textContent='Connected'; btn.disabled=true; }
    else { btn.textContent='Connect Wallet'; btn.disabled=false; }
  }

  async function connectWallet(){
    if(!window.ethereum){ setWalletUI('error','MetaMask not found — install it first'); return; }
    try {
      setWalletUI('','Connecting...');
      await window.ethereum.request({ method: 'eth_requestAccounts' });

      /* Switch to Sepolia */
      try {
        await window.ethereum.request({ method: 'wallet_switchEthereumChain', params:[{chainId: SEPOLIA_CHAIN_ID}] });
      } catch(sw){
        if(sw.code===4902){
          await window.ethereum.request({ method: 'wallet_addEthereumChain', params:[{
            chainId: SEPOLIA_CHAIN_ID, chainName:'Sepolia',
            nativeCurrency:{name:'SepoliaETH',symbol:'ETH',decimals:18},
            rpcUrls:['https://rpc.sepolia.org'],
            blockExplorerUrls:['https://sepolia.etherscan.io']
          }]});
        }
      }

      provider     = new ethers.BrowserProvider(window.ethereum);
      signer       = await provider.getSigner();
      walletAddress= await signer.getAddress();
      swordContract= new ethers.Contract(SWORD_ADDRESS, ERC20_ABI, signer);

      const decimals = await swordContract.decimals();
      const raw      = await swordContract.balanceOf(walletAddress);
      const balance  = Number(ethers.formatUnits(raw, decimals));

      const short = walletAddress.slice(0,6)+'...'+walletAddress.slice(-4);
      setWalletUI('connected', short, Math.floor(balance));
    } catch(e){
      setWalletUI('error', e.message?.slice(0,60)||'Connection failed');
    }
  }

  /* ── Log helpers ── */
  function log(text, cls=''){
    const el=document.getElementById('battle-log');
    const p=document.createElement('p'); p.className='log-line '+(cls||'sys'); p.textContent=text;
    el.appendChild(p); el.scrollTop=el.scrollHeight;
  }
  function logLink(text, url){
    const el=document.getElementById('battle-log');
    const a=document.createElement('a'); a.className='tx-link'; a.textContent=text;
    a.href=url; a.target='_blank';
    el.appendChild(a); el.scrollTop=el.scrollHeight;
  }
  function clearLog(){ document.getElementById('battle-log').innerHTML=''; }

  function setHP(who,pct){
    const fill=document.getElementById('hp-'+who+'-fill');
    const txt =document.getElementById('hp-'+who+'-text');
    const hp  =Math.max(0,Math.round(pct));
    fill.style.width=hp+'%'; fill.className='hp-fill'+(hp<30?' low':'');
    txt.textContent=hp+' HP';
  }
  function shake(id){ const e=document.getElementById(id); e.classList.remove('shaking'); void e.offsetWidth; e.classList.add('shaking'); setTimeout(()=>e.classList.remove('shaking'),400); }
  function glow(id){  const e=document.getElementById(id); e.classList.remove('glowing');  void e.offsetWidth; e.classList.add('glowing');  setTimeout(()=>e.classList.remove('glowing'),600); }
  function sleep(ms){ return new Promise(r=>setTimeout(r,ms)); }

  function updateHoard(amount){
    monsterHoard+=amount;
    const el=document.getElementById('hoard-count');
    el.textContent=monsterHoard.toLocaleString()+' ⚔';
    el.classList.remove('pulse'); void el.offsetWidth; el.classList.add('pulse');
  }

  /* ── BATTLE ── */
  async function startBattle(){
    if(battling) return;

    /* Must be connected */
    if(!signer){
      alert('Connect your wallet first!'); return;
    }

    const swords = parseInt(swordInput.value)||0;
    if(swords < 1){ alert('Enter at least 1 SWORD to battle.'); return; }

    battling=true;
    const btn=document.getElementById('fight-btn');
    btn.disabled=true;
    const banner=document.getElementById('result-banner');
    banner.style.display='none'; banner.className='result-banner';

    clearLog();
    setHP('player',100); setHP('monster',100);
    document.getElementById('sprite-player').textContent='🧝';
    document.getElementById('sprite-monster').textContent='🐉';

    /* Determine outcome locally (mirrors contract logic) */
    const strongEnough = swords >= 100;
    const roll         = Math.random()*100;
    const playerWins   = strongEnough ? (roll<98) : (roll<2);

    log(`⚔ A challenger enters with ${swords.toLocaleString()} SWORD${swords===1?'':'s'}!`,'sys');
    await sleep(600);
    log(strongEnough ? 'The champion radiates power — the monster hesitates...'
                     : 'The champion enters with too few swords — the monster snarls in contempt...','sys');
    await sleep(700);

    /* ── REAL TOKEN TRANSFER ── */
    log('📜 Signing token transfer in MetaMask...','sys');
    let txHash = null;
    try {
      const decimals = await swordContract.decimals();
      const amount   = ethers.parseUnits(String(swords), decimals);
      const tx       = await swordContract.transfer(MONSTER_ADDRESS, amount);
      txHash = tx.hash;
      log(`✦ Transaction submitted — awaiting confirmation...`,'gold');
      logLink('View on Etherscan ↗', `https://sepolia.etherscan.io/tx/${txHash}`);
      await tx.wait();
      log(`✦ Transfer confirmed on-chain!`,'gold');

      /* Refresh balance */
      const raw = await swordContract.balanceOf(walletAddress);
      const bal = Math.floor(Number(ethers.formatUnits(raw, decimals)));
      document.getElementById('sword-balance').textContent = bal.toLocaleString()+' ⚔ SWORD';
    } catch(e){
      const msg = e?.reason || e?.message?.slice(0,80) || 'Transaction failed';
      log('✦ Transfer failed: '+msg,'lose');
      btn.disabled=false; btn.textContent='⚔ Fight Again'; battling=false;
      return;
    }
    await sleep(400);

    /* ── Battle animation ── */
    let playerHP=100, monsterHP=100;
    const rounds=4+Math.floor(Math.random()*3);
    for(let r=0;r<rounds;r++){
      await sleep(550);
      if(playerWins){
        const pdmg=15+Math.floor(Math.random()*20), mdmg=3+Math.floor(Math.random()*8);
        monsterHP=Math.max(5,monsterHP-pdmg); playerHP=Math.max(10,playerHP-mdmg);
        setHP('monster',monsterHP); setHP('player',playerHP);
        shake('sprite-monster'); await sleep(200); shake('sprite-player');
        log(`Round ${r+1}: Your blade strikes for ${pdmg} damage! The wyrm claws back for ${mdmg}.`,'atk');
      } else {
        const pdmg=15+Math.floor(Math.random()*22), mdmg=2+Math.floor(Math.random()*5);
        playerHP=Math.max(5,playerHP-pdmg); monsterHP=Math.max(10,monsterHP-mdmg);
        setHP('player',playerHP); setHP('monster',monsterHP);
        shake('sprite-player'); await sleep(200); shake('sprite-monster');
        log(`Round ${r+1}: The wyrm unleashes ${pdmg} fire damage! You scratch back for ${mdmg}.`,'def');
      }
      if(r===rounds-1){
        await sleep(700);
        if(playerWins){
          setHP('monster',0); glow('sprite-player');
          log(`FINAL STRIKE! The dragon falls, slain by ${swords.toLocaleString()} swords!`,'win');
        } else {
          setHP('player',0); glow('sprite-monster');
          log('The wyrm roars — your champion crumbles into ash...','lose');
        }
      }
    }

    await sleep(800);

    if(playerWins){
      log('✦ Victory! 0.001 Sepolia ETH reward awaits (requires BattleArena contract).','gold');
      document.getElementById('sprite-player').textContent='👑';
      document.getElementById('sprite-monster').textContent='💀';
      banner.className='result-banner victory';
      document.getElementById('result-title').textContent='⚔ Victory!';
      document.getElementById('result-sub').textContent='Your swords vanquished the wyrm. Glory is yours.';
    } else {
      log('✦ Defeat. The monster claimed your swords.','lose');
      updateHoard(swords);
      document.getElementById('sprite-player').textContent='💀';
      document.getElementById('sprite-monster').textContent='🐉';
      banner.className='result-banner defeat';
      document.getElementById('result-title').textContent='☠ Defeat';
      document.getElementById('result-sub').textContent='Arm yourself with 100+ SWORD tokens to fight with honor.';
    }
    if(txHash){
      const a=document.createElement('a'); a.className='tx-link';
      a.textContent='View confirmed transaction ↗';
      a.href=`https://sepolia.etherscan.io/tx/${txHash}`; a.target='_blank';
      banner.appendChild(document.createElement('br')); banner.appendChild(a);
    }
    banner.style.display='block';
    btn.disabled=false; btn.textContent='⚔ Fight Again'; battling=false;
  }

  /* ── Auto-reconnect if already approved ── */
  window.addEventListener('load', async ()=>{
    if(window.ethereum){
      const accounts = await window.ethereum.request({method:'eth_accounts'});
      if(accounts.length) connectWallet();
      window.ethereum.on('accountsChanged', ()=>connectWallet());
      window.ethereum.on('chainChanged',    ()=>connectWallet());
    }
  });
</script>
</body>
</html>
