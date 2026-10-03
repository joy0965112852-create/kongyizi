<!DOCTYPE html>
<html lang="zh-Hant">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>孔ＯＯ</title>
    <style>
        body {
            font-family: '標楷體', 'Times New Roman', serif;
            background-color: #e8dcc4; 
            background-image: radial-gradient(#d5c3a1 1px, transparent 1px);
            background-size: 20px 20px;
            color: #2c1e16;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            line-height: 1.8;
            letter-spacing: 1px;
            transition: background-color 0.5s, color 0.5s;
        }
        #game-container {
            background-color: #f7f1e3;
            padding: 40px;
            border-radius: 4px;
            box-shadow: 0 10px 25px rgba(0,0,0,0.2);
            max-width: 750px; 
            width: 90%;
            text-align: justify; /* 確保整體內容左右對齊 */
            text-justify: inter-ideograph;
            border: 1px solid #a38c6d;
            border-left: 15px solid #5c4033; 
            transition: background-color 0.5s, border 0.5s, box-shadow 0.5s;
            max-height: 85vh;
            overflow-y: auto;
        }
        body.white-theme {
            background: #ffffff;
        }
        body.white-theme #game-container {
            background-color: #ffffff;
            border: none;
            box-shadow: none;
            color: #aaaaaa;
            text-align: center;
        }
        body.black-theme {
            background: #000000;
        }
        body.black-theme #game-container {
            background-color: #000000;
            border: none;
            box-shadow: none;
            color: #ff0000;
            text-align: center;
        }
        h1, h2 {
            text-align: center;
            color: inherit;
            border-bottom: 2px dashed #a38c6d;
            padding-bottom: 10px;
        }
        body.white-theme h1, body.white-theme h2,
        body.black-theme h1, body.black-theme h2 {
            border: none;
        }
        input[type="text"] {
            width: 200px; 
            padding: 8px 12px;
            margin: 0 10px;
            font-size: 18px;
            font-family: inherit;
            border: 1px solid #8b7355;
            border-radius: 4px;
            background-color: #fffaf0;
        }
        button {
            display: block;
            width: 100%;
            padding: 15px;
            margin: 15px 0;
            font-size: 18px;
            cursor: pointer;
            background-color: #7b5e43;
            color: #f7f1e3;
            border: none;
            border-radius: 4px;
            transition: all 0.3s ease;
            font-family: inherit;
            box-shadow: 0 4px 6px rgba(0,0,0,0.1);
        }
        button:hover {
            background-color: #4a3320;
            transform: translateY(-2px);
        }
        body.white-theme button {
            background-color: #cccccc;
            color: #ffffff;
        }
        body.white-theme button:hover { background-color: #999999; }
        body.black-theme button {
            background-color: #333333;
            color: #ff0000;
        }
        body.black-theme button:hover { background-color: #555555; }
        .story-text {
            font-size: 20px;
            margin-bottom: 25px;
            text-align: justify;
            text-justify: inter-ideograph;
            word-break: normal; 
            overflow-wrap: break-word;
        }
        .fade-in {
            animation: fadeIn 0.8s ease-in-out;
        }
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }
        .dialogue-line {
            display: none; 
            margin: 15px 0;
            padding: 10px 18px;
            border-radius: 8px;
            width: fit-content;
            max-width: 85%;
            animation: fadeIn 0.5s ease-in-out;
            text-align: justify;
        }
        .dialogue-left {
            background-color: #e4d5b7;
            align-self: flex-start;
            margin-right: auto;
            border-bottom-left-radius: 0;
        }
        .dialogue-right {
            background-color: #7b5e43;
            color: #f7f1e3;
            align-self: flex-end;
            margin-left: auto;
            border-bottom-right-radius: 0;
        }
        .dialogue-plain {
            background-color: transparent;
            align-self: flex-start;
            padding: 5px 0;
            margin-right: auto;
            border-radius: 0;
        }
        .dialogue-container {
            display: flex;
            flex-direction: column;
        }
    </style>
</head>
<body>

<div id="game-container" class="fade-in">
</div>

<script>
    let playerName = "";
    let familyBackground = "";
    let dialogueIndex = 0;
    const container = document.getElementById('game-container');

    function resetTheme() {
        document.body.className = '';
    }

    function renderScreen(content) {
        container.innerHTML = `<div class="fade-in">${content}</div>`;
    }

    function initGame() {
        resetTheme();
        renderScreen(`
            <h1>孔ＯＯ</h1>
            <div class="story-text" style="text-align: center;">
                請輸入你的名字：孔 <input type="text" id="nameInput" placeholder="請輸入單名或雙名">
                <br><br>
                「歡迎來到清末民初的魯鎮。在這個時代，『萬般皆下品，惟有讀書高』。<br>你的一生，將由你的選擇決定……」
            </div>
            <button onclick="startGame()">進入遊戲</button>
        `);
    }

    function startGame() {
        const nameInput = document.getElementById('nameInput').value.trim();
        playerName = nameInput ? nameInput : "某";
        stage1();
    }

    function stage1() {
        renderScreen(`
            <h2>出身與啟蒙</h2>
            <div class="story-text">
                孔${playerName}，請選擇你的最初開局：
            </div>
            <button onclick="stage1_result('poor')">貧困家庭</button>
            <button onclick="stage1_result('normal')">普通家庭</button>
            <button onclick="stage1_result('rich')">富貴家庭</button>
        `);
    }

    function stage1_result(type) {
        familyBackground = type;
        let descText = "";
        
        if (type === 'poor') {
            descText = "你家徒四壁，連買燈油的錢都沒有。你選擇鑿壁偷光、囊螢映雪，靠著鄰居微弱的燈光苦讀四書五經。因為長期營養不良，你的身材高大卻面黃肌瘦。";
        } else if (type === 'normal') {
            descText = "家裡開個小作坊，把你送進鎮上的平民私塾。你每天跟著老先生搖頭晃腦地背誦「君子固窮」。";
        } else if (type === 'rich') {
            descText = "你是當地望族之子，家裡請了名師到宅邸授課，你從小用上好的宣紙練字，寫得一筆好字。";
        }

        renderScreen(`
            <div class="story-text">${descText}</div>
            <button onclick="stage2_result()">歲月流逝，前往科舉考場</button>
        `);
    }

    function stage2_result() {
        let descText = "";
        if (familyBackground === 'poor') {
            descText = "你滿懷希望地去參加鄉試，榜單公布那天，你在人群中尋找自己的名字……<br><br>已經飢腸轆轆的你，使勁所有力氣看穿榜單，但卻找不到自己的名字，名落孫山。";
        } else if (familyBackground === 'normal') {
            descText = "你滿懷希望地去參加鄉試，榜單公布那天，你在人群中尋找自己的名字……<br><br>你的八股文不合考官胃口，即使使勁力氣看穿榜單，但都找不到自己的名字，名落孫山。";
        } else if (familyBackground === 'rich') {
            descText = "你滿懷希望地去參加鄉試，榜單公布那天，你在人群中尋找自己的名字……<br><br>你的八股文不合考官胃口，即使使勁力氣看穿榜單，但都找不到自己的名字，名落孫山。";
        }

        let choicesHTML = `
            <button onclick="stage3()">不甘心，繼續苦讀趕考</button>
            <button onclick="showJobs()">認清現實，另尋他路</button>
        `;
        if (familyBackground === 'rich') {
            choicesHTML += `<button onclick="bribe_result()">給考官溫卷</button>`;
        }

        renderScreen(`
            <h2>命運的試煉「科舉考試」</h2>
            <div class="story-text">
                ${descText}
            </div>
            <h3>【選擇你的下一步】</h3>
            ${choicesHTML}
        `);
    }

    function bribe_result() {
        renderScreen(`
            <div class="story-text">
                偏偏遇到百年難得一見的清官，還好他仍有不忍之心，只判你終身不得參加科舉。
            </div>
            <button onclick="showJobs()">認清現實，另尋他路</button>
        `);
    }

    function stage3() {
        let descText = "";
        if (familyBackground === 'poor') {
            descText = "你為了準備科舉，卻買不起昂貴的書籍與紙筆，於是鋌而走險去偷書。被抓到後，你堅稱「竊書不能算偷」，卻還是遭到眾人毒打。你雖保住性命，卻落得滿身是傷，最終只能流落街頭。";
        } else if (familyBackground === 'normal') {
            descText = "考到三十歲依然是個童生，家裡的小作坊被你拖垮破產，父母將你趕出家門。";
        } else if (familyBackground === 'rich') {
            descText = "你靠著家底深厚，一路考到了五十多歲，卻依然只是個童生。因為你平時好喝懶做，除了背誦八股文之外毫無謀生技能，隨著家族長輩凋零，萬貫家財終究被你吃喝揮霍殆盡。曾經奉承你的親友紛紛將你掃地出門，你從闊少爺變成了一無所有的落魄老童生。";
        }

        renderScreen(`
            <h2>命運的岔路</h2>
            <div class="story-text">${descText}</div>
            <button onclick="showJobs()">另尋他路</button>
        `);
    }

    function showJobs() {
        renderScreen(`
            <h2>另尋他路</h2>
            <div class="story-text">你必須找份工作養活自己，你會選擇：</div>
            <button onclick="jobResult('teacher')">勉強當上蒙塾老師</button>
            <button onclick="jobResult('copy')">發揮專長，替人抄書</button>
            <button onclick="jobResult('labor')">脫下長衫，去碼頭做苦力</button>
        `);
    }

    function jobResult(jobType) {
        let resultText = "";
        if (jobType === 'teacher') {
            resultText = "你堅持教小孩「回字有四種寫法」，家長認為你教的東西對生活毫無幫助。加上你名聲實在壞得一敗塗地，最終被辭退。";
        } else if (jobType === 'copy') {
            resultText = "你寫得一筆好字，一開始生意不錯。但你自認是「讀書人」，不屑抄寫通俗小說或白話文，只肯抄古籍。加上你好喝懶做，常常把東家的筆墨紙硯變賣換酒喝，名聲臭了，再也沒人找你。";
        } else if (jobType === 'labor') {
            resultText = "你決定放下讀書人的身段，穿著長衣去和短衣幫一起扛麻袋。但你四體不勤，根本扛不動；更慘的是，短衣幫的工人嘲笑你：「喲！這不是孔乙己嗎？讀書人怎麼來跟我們搶飯吃？」你發現自己融入不了底層，卻也被上層拋棄。你受不了屈辱，選擇離開。";
        }

        renderScreen(`
            <div class="story-text">${resultText}</div>
            <button onclick="stage4_intro()">繼續</button>
        `);
    }

    function stage4_intro() {
        renderScreen(`
            <h2>最後的掙扎</h2>
            <div class="story-text">
                孔${playerName}，沒有謀生能力，只能乞討或趁機偷竊。<br><br>
                穿著長衫、滿臉花白，且夾帶傷痕的你，步履蹣跚，已經好幾天沒吃飯了，肚子餓得發疼，經過咸亨酒店時，聞到陣陣酒香與茴香豆的味道，總讓你垂涎三尺。
            </div>
            <button onclick="stage4_dialogue_1()">【下一頁】</button>
        `);
    }

    function stage4_dialogue_1() {
        dialogueIndex = 0;
        renderScreen(`
            <div class="dialogue-container" id="dialogueBox1">
                <div class="dialogue-line dialogue-left">「哎呀！這不是那個誰？」</div>
                <div class="dialogue-line dialogue-left">「孔……孔什麼來著？」</div>
                <div class="dialogue-line dialogue-left">某人看著旁邊的描紅紙，笑了一聲說：「上大人孔乙己……就叫孔乙己吧。」</div>
                <div class="dialogue-line dialogue-plain">眾人一齊大笑。</div>
            </div>
            <button id="nextBtn1" onclick="showNextDialogue1()">【浮現對話】</button>
        `);
        showNextDialogue1();
    }

    function showNextDialogue1() {
        const lines = document.querySelectorAll('#dialogueBox1 .dialogue-line');
        if (dialogueIndex < lines.length) {
            lines[dialogueIndex].style.display = 'block';
            dialogueIndex++;
            if (dialogueIndex === lines.length) {
                const btn = document.getElementById('nextBtn1');
                btn.innerText = "【下一頁】";
                btn.onclick = stage4_dialogue_2;
            }
        }
    }

    function stage4_dialogue_2() {
        dialogueIndex = 0;
        renderScreen(`
            <div class="dialogue-container" id="dialogueBox2">
                <div class="dialogue-line dialogue-right">「我是孔${playerName}！」</div>
                <div class="dialogue-line dialogue-left">「孔乙己，你臉上又添上新傷疤了！」</div>
                <div class="dialogue-line dialogue-right">「我是……我是孔${playerName}！不是孔乙己！」</div>
                <div class="dialogue-line dialogue-left">「孔乙己，你當眞認識字麽？你怎的連半個秀才也撈不到呢？」</div>
                <div class="dialogue-line dialogue-right">「我、我……不是孔乙己！」</div>
                <div class="dialogue-line dialogue-left">「孔乙己！還欠十九個錢呢！」</div>
                <div class="dialogue-line dialogue-right">「……」</div>
            </div>
            <button id="nextBtn2" onclick="showNextDialogue2()">【浮現對話】</button>
        `);
        showNextDialogue2();
    }

    function showNextDialogue2() {
        const lines = document.querySelectorAll('#dialogueBox2 .dialogue-line');
        if (dialogueIndex < lines.length) {
            lines[dialogueIndex].style.display = 'block';
            dialogueIndex++;
            if (dialogueIndex === lines.length) {
                const btn = document.getElementById('nextBtn2');
                btn.innerText = "【下一頁】";
                btn.onclick = stage4_identity;
            }
        }
    }

    function stage4_identity() {
        document.body.className = 'white-theme';
        renderScreen(`
            <div class="story-text" style="font-size: 32px; font-weight: bold; margin-top: 20vh; text-align: center;">
                「我……我是誰？」
            </div>
            <button onclick="stage4_choices()" style="margin-top: 30vh;">【下一頁】</button>
        `);
    }

    function stage4_choices() {
        resetTheme();
        renderScreen(`
            <div class="story-text">
                孔乙己，你現在已經沒有現錢，但酒店裡的十九個錢還欠著，你又快要走向絕路，你會怎麼做？
            </div>
            <button onclick="ending_ding_1()">去丁舉人家裡偷點值錢的東西</button>
            <button onclick="ending_baozi()">去市場偷平民小販的包子</button>
            <button onclick="ending_beg_1()">堅持讀書人的氣節，絕不偷竊，上街乞討</button>
        `);
    }

    function ending_ding_1() {
        renderScreen(`
            <div class="story-text">
                你潛入丁舉人家。被發現後，丁舉人動用私刑，寫了服辯，還打了大半夜，你的腿被打折了。
            </div>
            <button onclick="ending_ding_2()">【下一頁】</button>
        `);
    }

    function ending_ding_2() {
        dialogueIndex = 0;
        renderScreen(`
            <div class="story-text">
                你在一個寒冷的冬夜，用手爬著去買了最後一碗溫酒。
            </div>
            <div class="dialogue-container" id="dialogueBox3">
                <div class="dialogue-line dialogue-left">「孔乙己麽？你還欠十九個錢呢！」</div>
                <div class="dialogue-line dialogue-left">「孔乙己，你又偸了東西了！」</div>
                <div class="dialogue-line dialogue-left">「取笑？要是不偸，怎麽會打斷腿？」</div>
            </div>
            <button id="nextBtn3" onclick="showNextDialogue3()">【浮現對話】</button>
        `);
        showNextDialogue3();
    }

    function showNextDialogue3() {
        const lines = document.querySelectorAll('#dialogueBox3 .dialogue-line');
        if (dialogueIndex < lines.length) {
            lines[dialogueIndex].style.display = 'block';
            dialogueIndex++;
            if (dialogueIndex === lines.length) {
                const btn = document.getElementById('nextBtn3');
                btn.innerText = "【下一頁】";
                btn.onclick = ending_ding_3;
            }
        }
    }

    function ending_ding_3() {
        renderScreen(`
            <div class="story-text">
                你用充滿泥濘的手，顫抖地掏出四文大錢，用盡力氣放在夥計手裡，隨後慢慢的、慢慢的消失在充滿歡笑聲的世界。
            </div>
            <button onclick="initGame()">重新開始</button>
        `);
    }

    function ending_baozi() {
        renderScreen(`
            <div class="story-text">
                你被小販抓住。周圍的群眾不但沒有同情你，反而圍成一圈嘲笑你、毆打你。你在眾人的哄笑聲中，被打得奄奄一息，隔天被發現凍死在街頭。
            </div>
            <button onclick="initGame()">重新開始</button>
        `);
    }

    function ending_beg_1() {
        renderScreen(`
            <div class="story-text">
                你穿著破長衫在街頭乞討，但因為你總是滿口「之乎者也」，路人覺得你是個瘋子，沒人願意施捨給你。
            </div>
            <button onclick="ending_beg_2()">【下一頁】</button>
        `);
    }

    function ending_beg_2() {
        dialogueIndex = 0;
        renderScreen(`
            <div class="dialogue-container" id="dialogueBox4">
                <div class="dialogue-line dialogue-left">「孔乙己麽？你還欠十九個錢呢！」</div>
                <div class="dialogue-line dialogue-left">「孔乙己，你臉上又添上新傷疤了！」</div>
                <div class="dialogue-line dialogue-left">「孔乙己，你當眞認識字麽？你怎的連半個秀才也撈不到呢？」</div>
            </div>
            <button id="nextBtn4" onclick="showNextDialogue4()">【浮現對話】</button>
        `);
        showNextDialogue4();
    }

    function showNextDialogue4() {
        const lines = document.querySelectorAll('#dialogueBox4 .dialogue-line');
        if (dialogueIndex < lines.length) {
            lines[dialogueIndex].style.display = 'block';
            dialogueIndex++;
            if (dialogueIndex === lines.length) {
                const btn = document.getElementById('nextBtn4');
                btn.innerText = "【下一頁】";
                btn.onclick = ending_beg_3;
            }
        }
    }

    function ending_beg_3() {
        renderScreen(`
            <div class="story-text">
                下著雪的夜晚，你餓死在眾人的視線外、潔白的雪堆裡。
            </div>
            <button onclick="ending_beg_4()">【下一頁】</button>
        `);
    }

    function ending_beg_4() {
        document.body.className = 'black-theme';
        renderScreen(`
            <div class="story-text" style="font-size: 32px; font-weight: bold; margin-top: 20vh; text-align: center;">
                「還欠十九個錢呢！」
            </div>
            <button onclick="initGame()" style="margin-top: 20vh;">重新開始</button>
        `);
    }

    initGame();
</script>
</body>
</html>