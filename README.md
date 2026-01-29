<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<title>География 9 класс — тест</title>
<style>
body {
    font-family: Arial;
    background: #f0f2f5;
    padding: 20px;
}
.container {
    background: white;
    padding: 20px;
    border-radius: 10px;
    max-width: 600px;
    margin: auto;
}
button {
    padding: 10px;
    margin: 5px 0;
    width: 100%;
    font-size: 16px;
}
.timer {
    font-weight: bold;
    color: red;
}
</style>
</head>
<body>

<div class="container">
<h2>Тест по географии (9 класс)</h2>
<p id="question"></p>
<div id="answers"></div>
<p class="timer">Время: <span id="time">25</span> сек</p>
<button onclick="nextQuestion()">Далее</button>
<p id="result"></p>
</div>

<script>
const questions = [
{q:"Самая большая страна мира?",a:["Россия","Канада","Китай","США"],c:0},
{q:"Самый населённый материк?",a:["Африка","Азия","Европа","Австралия"],c:1},
{q:"Столица Казахстана?",a:["Алматы","Астана","Шымкент","Караганда"],c:1},
{q:"Самый большой океан?",a:["Атлантический","Индийский","Тихий","Северный"],c:2},
{q:"Самая высокая гора мира?",a:["Эльбрус","Монблан","Килиманджаро","Эверест"],c:3},
{q:"Самый маленький материк?",a:["Европа","Антарктида","Австралия","Африка"],c:2},
{q:"Самая длинная река?",a:["Амазонка","Нил","Янцзы","Миссисипи"],c:1},
{q:"Столица Франции?",a:["Лион","Марсель","Париж","Ницца"],c:2},
{q:"Самый холодный материк?",a:["Европа","Азия","Антарктида","Африка"],c:2},
{q:"Какая страна в Южной Америке?",a:["Испания","Чили","Италия","Египет"],c:1}
];

// случайные 15 (если вопросов меньше — возьмёт сколько есть)
questions.sort(() => Math.random() - 0.5);
let test = questions.slice(0, 15);

let index = 0;
let score = 0;
let time = 25;
let timer;

function showQuestion() {
    if (index >= test.length) {
        document.body.innerHTML =
        `<h2>Результат: ${score} из ${test.length}<br>Оценка: ${getGrade()}</h2>`;
        return;
    }

    document.getElementById("question").innerText =
        (index+1)+". "+test[index].q;

    const answersDiv = document.getElementById("answers");
    answersDiv.innerHTML = "";

    test[index].a.forEach((text, i) => {
        let btn = document.createElement("button");
        btn.innerText = text;
        btn.onclick = () => answer(i);
        answersDiv.appendChild(btn);
    });

    resetTimer();
}

function answer(i) {
    if (i === test[index].c) score++;
    nextQuestion();
}

function nextQuestion() {
    index++;
    showQuestion();
}

function resetTimer() {
    clearInterval(timer);
    time = 25;
    document.getElementById("time").innerText = time;

    timer = setInterval(() => {
        time--;
        document.getElementById("time").innerText = time;
        if (time === 0) {
            clearInterval(timer);
            nextQuestion();
        }
    }, 1000);
}

function getGrade() {
    if (score >= 13) return 5;
    if (score >= 10) return 4;
    if (score >= 7) return 3;
    return 2;
}

showQuestion();
</script>

</body>
</html>
