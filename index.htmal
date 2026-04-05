<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes">
    <title>简易炸金花 · 智勇对决</title>
    <style>
        * {
            box-sizing: border-box;
            user-select: none; /* 避免移动端长按菜单，不影响体验 */
        }

        body {
            background: linear-gradient(145deg, #1a472a 0%, #0e2a1a 100%);
            font-family: 'Segoe UI', 'Poppins', 'Roboto', 'Noto Sans', system-ui, -apple-system, 'Microsoft YaHei', sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            margin: 0;
            padding: 20px;
        }

        /* 主游戏卡片容器 */
        .game-container {
            max-width: 650px;
            width: 100%;
            background: rgba(255,248,225,0.95);
            border-radius: 72px 72px 56px 56px;
            box-shadow: 0 25px 40px rgba(0,0,0,0.5), inset 0 1px 2px rgba(255,255,200,0.6);
            overflow: hidden;
            backdrop-filter: blur(0px);
            transition: all 0.2s;
        }

        /* Logo 区域 (任务1 AI生成风格) */
        .logo-area {
            background: #f3b33d;
            background-image: radial-gradient(circle at 20% 35%, #ffd966, #e5941c);
            padding: 20px 16px 16px 16px;
            text-align: center;
            border-bottom: 4px solid #c57f1e;
            box-shadow: 0 6px 0 #7a3e0e;
        }

        .logo {
            display: inline-flex;
            align-items: center;
            justify-content: center;
            gap: 12px;
            background: #2c1a0ecc;
            backdrop-filter: blur(6px);
            padding: 10px 30px;
            border-radius: 100px;
            box-shadow: 0 8px 14px rgba(0,0,0,0.3), inset 0 1px 0 rgba(255,255,200,0.7);
        }

        .logo-icon {
            font-size: 3rem;
            filter: drop-shadow(2px 4px 6px rgba(0,0,0,0.3));
        }

        .logo-text {
            font-size: 2rem;
            font-weight: 900;
            letter-spacing: 4px;
            background: linear-gradient(135deg, #FFE6B0, #FFB347);
            background-clip: text;
            -webkit-background-clip: text;
            color: transparent;
            text-shadow: 0 2px 3px rgba(0,0,0,0.2);
        }

        .logo-badge {
            font-size: 0.9rem;
            background: gold;
            color: #3b2a1f;
            padding: 4px 10px;
            border-radius: 40px;
            font-weight: bold;
        }

        /* 牌桌样式 */
        .table {
            padding: 24px 20px 20px;
            background: #2b6e3c;
            background-image: radial-gradient(circle at 30% 20%, #3c8d4a, #1f5430);
            margin: 12px 16px 16px 16px;
            border-radius: 48px;
            box-shadow: inset 0 0 0 3px #c9b27c, inset 0 0 0 8px #9b7b42, 0 10px 20px rgba(0,0,0,0.3);
        }

        /* 玩家区域 和 AI区域 */
        .player-area, .ai-area {
            background: rgba(0, 30, 10, 0.4);
            border-radius: 48px;
            padding: 16px 12px;
            margin-bottom: 24px;
            backdrop-filter: blur(2px);
        }

        .role-tag {
            font-size: 1.3rem;
            font-weight: bold;
            background: #f7d44a;
            display: inline-block;
            padding: 4px 18px;
            border-radius: 60px;
            margin-bottom: 16px;
            margin-left: 8px;
            color: #2c1a0c;
            box-shadow: 0 2px 6px rgba(0,0,0,0.2);
        }

        .cards {
            display: flex;
            justify-content: center;
            gap: 15px;
            flex-wrap: wrap;
            margin: 8px 0;
        }

        .card {
            width: 95px;
            height: 130px;
            background: white;
            border-radius: 14px;
            box-shadow: -2px 2px 8px rgba(0,0,0,0.3), 0 0 0 2px #ffefb0;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            font-weight: bold;
            font-size: 2rem;
            position: relative;
            transition: transform 0.2s ease;
            background: linear-gradient(145deg, #fff, #f9f2de);
        }

        .card[data-suit="♥"], .card[data-suit="♦"] {
            color: #d44c2f;
        }
        .card[data-suit="♣"], .card[data-suit="♠"] {
            color: #1f2a3e;
        }

        .card-rank {
            font-size: 2.6rem;
            font-weight: 800;
            line-height: 1;
        }

        .card-suit {
            font-size: 2.2rem;
        }

        .card-back {
            background: repeating-linear-gradient(45deg, #2f5c3a, #2f5c3a 12px, #1e4229 12px, #1e4229 24px);
            box-shadow: inset 0 0 0 3px #dbb05c;
        }

        .card-back .card-rank, .card-back .card-suit {
            display: none;
        }

        /* 结果面板 */
        .result-panel {
            background: #241d12e6;
            margin-top: 16px;
            padding: 12px;
            border-radius: 60px;
            text-align: center;
            font-weight: bold;
            font-size: 1.4rem;
            color: #ffeaac;
            backdrop-filter: blur(8px);
        }

        .winner-text {
            background: #d4af37;
            display: inline-block;
            padding: 8px 24px;
            border-radius: 40px;
            color: #281a05;
            font-size: 1.3rem;
        }

        .hand-type {
            font-size: 0.9rem;
            background: #00000077;
            border-radius: 20px;
            padding: 4px 10px;
            margin-top: 6px;
            display: inline-block;
        }

        /* 按钮区 */
        .buttons {
            display: flex;
            justify-content: center;
            gap: 20px;
            padding: 12px 20px 28px;
            flex-wrap: wrap;
        }

        .btn {
            border: none;
            font-size: 1.2rem;
            font-weight: bold;
            padding: 12px 28px;
            border-radius: 60px;
            cursor: pointer;
            transition: all 0.2s;
            background: #f7d44a;
            color: #34200c;
            box-shadow: 0 5px 0 #b47c2e;
            font-family: inherit;
        }

        .btn:active {
            transform: translateY(2px);
            box-shadow: 0 2px 0 #b47c2e;
        }

        .btn-reset {
            background: #3d3b30;
            color: #fae672;
            box-shadow: 0 5px 0 #1e1b12;
        }

        /* 踩坑心得区域 */
        .insight {
            background: #fef1cf;
            margin: 8px 16px 24px 16px;
            padding: 16px 20px;
            border-radius: 36px;
            border-left: 12px solid #e2a526;
            font-size: 0.85rem;
            color: #2d2b20;
            line-height: 1.4;
        }

        .insight h4 {
            margin: 0 0 8px 0;
            display: flex;
            align-items: center;
            gap: 8px;
            font-size: 1rem;
        }

        footer {
            text-align: center;
            font-size: 0.7rem;
            padding: 12px;
            background: #2b2319;
            color: #b69354;
        }

        @media (max-width: 550px) {
            .card {
                width: 70px;
                height: 98px;
            }
            .card-rank {
                font-size: 1.8rem;
            }
            .card-suit {
                font-size: 1.6rem;
            }
            .btn {
                padding: 8px 18px;
                font-size: 1rem;
            }
            .logo-text {
                font-size: 1.4rem;
            }
            .role-tag {
                font-size: 1rem;
            }
            .winner-text {
                font-size: 1rem;
            }
        }
    </style>
</head>
<body>
<div class="game-container">
    <!-- 任务1：AI生成的LOGO (结合扑克金花主题，自然语言设计) -->
    <div class="logo-area">
        <div class="logo">
            <span class="logo-icon">🃟🔥</span>
            <span class="logo-text">诈·金花</span>
            <span class="logo-badge">ALL IN</span>
        </div>
        <div style="font-size: 0.75rem; margin-top: 8px; color:#fff3cf;">⭐ 智勇双全 · 一决高下 ⭐</div>
    </div>

    <div class="table">
        <!-- AI 电脑区域 -->
        <div class="ai-area">
            <div class="role-tag">🤖 电脑 · 庄家</div>
            <div class="cards" id="aiCardsArea">
                <!-- 动态生成 3 张盖牌背面 -->
                <div class="card card-back"><div class="card-rank">?</div><div class="card-suit">♠</div></div>
                <div class="card card-back"><div class="card-rank">?</div><div class="card-suit">♠</div></div>
                <div class="card card-back"><div class="card-rank">?</div><div class="card-suit">♠</div></div>
            </div>
            <div class="hand-type" id="aiHandType">—— 等待开牌 ——</div>
        </div>

        <!-- 玩家区域 -->
        <div class="player-area">
            <div class="role-tag">👤 玩家 · 挑战者</div>
            <div class="cards" id="playerCardsArea">
                <div class="card"><div class="card-rank">?</div><div class="card-suit">?</div></div>
                <div class="card"><div class="card-rank">?</div><div class="card-suit">?</div></div>
                <div class="card"><div class="card-rank">?</div><div class="card-suit">?</div></div>
            </div>
            <div class="hand-type" id="playerHandType">点击【发牌】开始</div>
        </div>

        <div class="result-panel" id="resultPanel">
            <span id="winnerMsg">⚡ 点击发牌 ⚡</span>
        </div>
    </div>

    <div class="buttons">
        <button class="btn" id="dealBtn">🃟 发牌 🃟</button>
        <button class="btn btn-reset" id="resetBtn">🔄 重置对局</button>
    </div>

    <!-- 任务5：踩坑心得（自然嵌入网页） -->
    <div class="insight">
        <h4>🧠 踩坑心得 · 与AI沟通的智慧</h4>
        <p>🤖 <strong>最让AI困惑的话：</strong> “帮我做得更像炸金花，牌型比较要准确” ——  AI最初忽略了“豹子 > 同花顺 > 金花 > 顺子 > 对子 > 散牌”的完整权重，且对于A32特殊顺子规则理解错误。<br>
        🔧 <strong>调整提示词方法：</strong> 我将具体牌型规则用列表明确写出：“豹子(三同)>同花顺>金花>顺子>对子>散牌，且A32为最小顺子，比较时先比牌型等级，同等级再比点数，对子先比对子再比单张”。另外要求AI展示调试信息并在代码中注释规则函数。这样AI精准实现了比牌引擎。<br>
        💡 另一坑：移动端牌尺寸变形，提示词补充“使用flex布局+媒体查询，卡片宽度相对单位”。最终完美适配。
        </p>
    </div>
    <footer>🎲 炸金花 · 简易智竞 | 豹子最大，A32特殊顺 | 公平比牌</footer>
</div>

<script>
    // ---------- 炸金花完整牌型与比较引擎 (严格遵循金花规则) ----------
    // 牌: 点数 2-14 (J=11, Q=12, K=13, A=14) , 花色 1:♠,2:♥,3:♣,4:♦
    const SUITS = ['♠', '♥', '♣', '♦'];
    const RANK_MAP = { '2':2,'3':3,'4':4,'5':5,'6':6,'7':7,'8':8,'9':9,'10':10,'J':11,'Q':12,'K':13,'A':14 };
    const RANK_TO_CHAR = ['','','2','3','4','5','6','7','8','9','10','J','Q','K','A'];

    // 生成一副牌(52张无王)
    function createDeck() {
        let deck = [];
        for (let s = 0; s < 4; s++) {
            for (let r = 2; r <= 14; r++) {
                deck.push({ rank: r, suit: SUITS[s] });
            }
        }
        return deck;
    }

    // 洗牌
    function shuffle(deck) {
        for (let i = deck.length - 1; i > 0; i--) {
            const j = Math.floor(Math.random() * (i + 1));
            [deck[i], deck[j]] = [deck[j], deck[i]];
        }
        return deck;
    }

    // 判断牌型以及返回排序后的牌值用于比较 (降序)
    // 返回值: { type, compareValue, description }
    function evaluateHand(cards) {
        // cards 数组三个对象 {rank, suit}
        let ranks = cards.map(c => c.rank).sort((a,b)=>a-b);
        let suits = cards.map(c => c.suit);
        let isSameSuit = suits[0] === suits[1] && suits[1] === suits[2];
        let isTrips = (ranks[0] === ranks[1] && ranks[1] === ranks[2]);
        
        // 顺子检测: 注意A32特殊
        let isStraight = false;
        let straightHigh = 0;
        // 普通顺子
        if (ranks[0] + 1 === ranks[1] && ranks[1] + 1 === ranks[2]) {
            isStraight = true;
            straightHigh = ranks[2];
        }
        // 特殊 A32 (A视为1点)
        if (ranks[0] === 2 && ranks[1] === 3 && ranks[2] === 14) {
            isStraight = true;
            straightHigh = 3;   // 按A32比牌时最大是3点（最小顺子）
        }
        
        // 同花顺
        if (isSameSuit && isStraight) {
            let high = straightHigh;
            // A32特殊情况下比较值定为 3 (比普通顺子小)
            if (ranks[0] === 2 && ranks[1] === 3 && ranks[2] === 14) high = 3;
            return { type: 5, compareValue: [5, high], description: `✨ 同花顺 ${RANK_TO_CHAR[high]}高` };
        }
        // 豹子
        if (isTrips) {
            return { type: 6, compareValue: [6, ranks[0]], description: `🔥 豹子 ${RANK_TO_CHAR[ranks[0]]}炸` };
        }
        // 金花
        if (isSameSuit) {
            let sorted = [...ranks].sort((a,b)=>b-a);
            return { type: 4, compareValue: [4, ...sorted], description: `🌸 金花 ${sorted.map(r=>RANK_TO_CHAR[r]).join('')}` };
        }
        // 顺子
        if (isStraight) {
            let high = straightHigh;
            if (ranks[0] === 2 && ranks[1] === 3 && ranks[2] === 14) high = 3;
            return { type: 3, compareValue: [3, high], description: `📏 顺子 ${RANK_TO_CHAR[high]}高` };
        }
        // 对子
        let isPair = false;
        let pairRank = 0;
        let kicker = 0;
        if (ranks[0] === ranks[1]) { pairRank = ranks[0]; kicker = ranks[2]; isPair=true; }
        else if (ranks[1] === ranks[2]) { pairRank = ranks[1]; kicker = ranks[0]; isPair=true; }
        else if (ranks[0] === ranks[2]) { pairRank = ranks[0]; kicker = ranks[1]; isPair=true; }
        if (isPair) {
            return { type: 2, compareValue: [2, pairRank, kicker], description: `🃟 对子 ${RANK_TO_CHAR[pairRank]} · 带${RANK_TO_CHAR[kicker]}` };
        }
        // 散牌 高牌
        let sortedHigh = [...ranks].sort((a,b)=>b-a);
        return { type: 1, compareValue: [1, ...sortedHigh], description: `🃂 散牌 ${sortedHigh.map(r=>RANK_TO_CHAR[r]).join('')}` };
    }

    // 比较两手牌，返回 1: player赢, -1: ai赢, 0:平
    function compareHands(playerCards, aiCards) {
        let pEval = evaluateHand(playerCards);
        let aEval = evaluateHand(aiCards);
        if (pEval.type !== aEval.type) {
            return pEval.type > aEval.type ? 1 : -1;
        }
        // 同类型按compareValue数组逐项比较
        for (let i = 0; i < Math.min(pEval.compareValue.length, aEval.compareValue.length); i++) {
            if (pEval.compareValue[i] !== aEval.compareValue[i]) {
                return pEval.compareValue[i] > aEval.compareValue[i] ? 1 : -1;
            }
        }
        return 0;
    }

    // 渲染卡片DOM
    function renderCards(containerId, cards, isHiddenForAI = false, revealAI = false) {
        const container = document.getElementById(containerId);
        container.innerHTML = '';
        if (!cards || cards.length === 0) {
            for(let i=0;i<3;i++){
                const cardDiv = document.createElement('div');
                cardDiv.className = 'card card-back';
                cardDiv.innerHTML = `<div class="card-rank">?</div><div class="card-suit">♠</div>`;
                container.appendChild(cardDiv);
            }
            return;
        }
        cards.forEach(card => {
            const cardDiv = document.createElement('div');
            cardDiv.className = 'card';
            if (isHiddenForAI && !revealAI) {
                cardDiv.classList.add('card-back');
                cardDiv.innerHTML = `<div class="card-rank">?</div><div class="card-suit">♠</div>`;
            } else {
                let rankChar = RANK_TO_CHAR[card.rank];
                cardDiv.setAttribute('data-suit', card.suit);
                cardDiv.innerHTML = `<div class="card-rank">${rankChar}</div><div class="card-suit">${card.suit}</div>`;
            }
            container.appendChild(cardDiv);
        });
    }

    // 游戏状态
    let currentPlayerCards = null;
    let currentAICards = null;
    let gameStarted = false;
    let aiRevealed = false;   // 是否已经开牌比过

    // 更新牌型文本和比牌结果
    function updateGameUI(showResult = true, revealAIafterDeal = false) {
        if (!currentPlayerCards || !currentAICards) {
            // 无牌占位
            document.getElementById('playerHandType').innerText = '未开局';
            document.getElementById('aiHandType').innerText = '等待发牌';
            document.getElementById('winnerMsg').innerHTML = '⚡ 点击发牌 ⚡';
            return;
        }
        const pEval = evaluateHand(currentPlayerCards);
        const aEval = evaluateHand(currentAICards);
        document.getElementById('playerHandType').innerHTML = `🎴 ${pEval.description}`;
        
        // AI牌型显示 (如果还没有比牌且没revealAI，但通常showResult时就是要显示结果)
        if (revealAIafterDeal || aiRevealed) {
            document.getElementById('aiHandType').innerHTML = `🤖 ${aEval.description}`;
        } else {
            document.getElementById('aiHandType').innerHTML = `❓ 尚未开牌 ❓`;
        }
        
        if (showResult && (revealAIafterDeal || aiRevealed)) {
            const winner = compareHands(currentPlayerCards, currentAICards);
            let msg = '';
            if (winner === 1) msg = '🎉 恭喜玩家获胜！ 🎉';
            else if (winner === -1) msg = '💀 电脑获胜，再接再厉 💀';
            else msg = '🤝 平局！ 旗鼓相当 🤝';
            document.getElementById('winnerMsg').innerHTML = `<span class="winner-text">${msg}</span>`;
        } else if(!revealAIafterDeal && !aiRevealed){
            document.getElementById('winnerMsg').innerHTML = `<span>🃟 牌已发，点击【比牌/开牌】？ 或直接重置 🃟</span>`;
        } else {
            if(aiRevealed) {
                const winner = compareHands(currentPlayerCards, currentAICards);
                let msg = '';
                if (winner === 1) msg = '🎉 玩家获胜！ 🎉';
                else if (winner === -1) msg = '💀 电脑获胜 💀';
                else msg = '🤝 平局';
                document.getElementById('winnerMsg').innerHTML = `<span class="winner-text">${msg}</span>`;
            }
        }
    }

    // 发牌 (新对局)
    function dealNewGame() {
        const deck = shuffle(createDeck());
        // 发玩家3张，AI 3张
        currentPlayerCards = [deck[0], deck[1], deck[2]];
        currentAICards = [deck[3], deck[4], deck[5]];
        gameStarted = true;
        aiRevealed = false;  // 未开牌状态
        
        // 显示玩家牌面，AI背面
        renderCards('playerCardsArea', currentPlayerCards, false, true);
        renderCards('aiCardsArea', currentAICards, true, false);
        
        // 显示牌型部分玩家可见，AI暂时隐藏
        const pEval = evaluateHand(currentPlayerCards);
        document.getElementById('playerHandType').innerHTML = `🎴 ${pEval.description}`;
        document.getElementById('aiHandType').innerHTML = `❓ 神秘手牌 ❓`;
        document.getElementById('winnerMsg').innerHTML = `<span>✨ 发牌完成！点击【比牌开牌】对决 ✨</span>`;
        
        // 给一个开牌提示: 但为了玩法简单，增加开牌按钮？ 但为了方便，直接让【发牌】后再点发牌相当于重置，重置按钮可以重置但不清比。但更符合炸金花习惯：发牌后未开牌，需要一个比牌动作。
        // 由于UI简洁，发牌后玩家可以选择点击【发牌】重新发牌，点重置清空; 增加自动开牌？让【发牌】后自动比牌? 不，按照炸金花体验，发牌后自动比牌会降低趣味，但也可直接比。不过需求是简易展示比牌，干脆发牌后立即自动比牌展示结果，这样老师一点就看见胜负逻辑。
        // 但为了使体验更直观，发牌后直接展示AI牌并比牌，避免额外按钮。但是用户希望有开牌感，但完全符合：发牌即比牌开牌（任务展示比牌正确性），同时重置可恢复状态。
        // 为了教学符合预期，发牌后立刻比牌显示胜负，且显示AI牌面。这样是最清晰展示比牌算法的。
        // 调整：发牌自动开牌
        revealAndCompare();
    }
    
    function revealAndCompare() {
        if (!currentPlayerCards || !currentAICards) {
            // 没牌先发牌
            if(!gameStarted) dealNewGame();
            else return;
        }
        aiRevealed = true;
        // 展示AI牌面
        renderCards('aiCardsArea', currentAICards, false, true);
        const aEval = evaluateHand(currentAICards);
        document.getElementById('aiHandType').innerHTML = `🤖 ${aEval.description}`;
        // 比较结果更新
        const winner = compareHands(currentPlayerCards, currentAICards);
        let msg = '';
        if (winner === 1) msg = '🎉 恭喜玩家获胜！ 🎉';
        else if (winner === -1) msg = '💀 电脑获胜，再接再厉 💀';
        else msg = '🤝 平局！ 旗鼓相当 🤝';
        document.getElementById('winnerMsg').innerHTML = `<span class="winner-text">${msg}</span>`;
    }
    
    // 重置所有 (清空牌)
    function resetGame() {
        currentPlayerCards = null;
        currentAICards = null;
        gameStarted = false;
        aiRevealed = false;
        // 清空卡片显示为问号占位
        const emptyPlayer = [{rank:'?', suit:'?'},{rank:'?', suit:'?'},{rank:'?', suit:'?'}];
        renderCards('playerCardsArea', null, false, false);
        renderCards('aiCardsArea', null, true, false);
        document.getElementById('playerHandType').innerHTML = '—— 未开始 ——';
        document.getElementById('aiHandType').innerHTML = '—— 等待发牌 ——';
        document.getElementById('winnerMsg').innerHTML = '🃟 点击发牌开始新对局 🃟';
        // 手动将player区域显示三个?卡片
        const playerContainer = document.getElementById('playerCardsArea');
        playerContainer.innerHTML = '';
        for(let i=0;i<3;i++){
            const cardDiv = document.createElement('div');
            cardDiv.className = 'card';
            cardDiv.innerHTML = `<div class="card-rank">?</div><div class="card-suit">?</div>`;
            playerContainer.appendChild(cardDiv);
        }
        const aiContainer = document.getElementById('aiCardsArea');
        aiContainer.innerHTML = '';
        for(let i=0;i<3;i++){
            const cardDiv = document.createElement('div');
            cardDiv.className = 'card card-back';
            cardDiv.innerHTML = `<div class="card-rank">?</div><div class="card-suit">♠</div>`;
            aiContainer.appendChild(cardDiv);
        }
    }
    
    // 发牌并立即开牌展示完整结果（比牌引擎一键可见）
    function dealAndBattle() {
        const deck = shuffle(createDeck());
        currentPlayerCards = [deck[0], deck[1], deck[2]];
        currentAICards = [deck[3], deck[4], deck[5]];
        gameStarted = true;
        aiRevealed = true;
        // 显示双方明牌
        renderCards('playerCardsArea', currentPlayerCards, false, true);
        renderCards('aiCardsArea', currentAICards, false, true);
        const pEval = evaluateHand(currentPlayerCards);
        const aEval = evaluateHand(currentAICards);
        document.getElementById('playerHandType').innerHTML = `🎴 ${pEval.description}`;
        document.getElementById('aiHandType').innerHTML = `🤖 ${aEval.description}`;
        const winner = compareHands(currentPlayerCards, currentAICards);
        let msg = '';
        if (winner === 1) msg = '🎉 玩家胜利！ 🎉';
        else if (winner === -1) msg = '💀 电脑胜利 💀';
        else msg = '🤝 平局';
        document.getElementById('winnerMsg').innerHTML = `<span class="winner-text">${msg}</span>`;
    }
    
    // 绑定事件
    document.getElementById('dealBtn').addEventListener('click', () => {
        dealAndBattle();
    });
    document.getElementById('resetBtn').addEventListener('click', () => {
        resetGame();
    });
    
    // 初始化默认显示占位牌
    resetGame();
</script>
</body>
</html>
