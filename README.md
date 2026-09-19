# My Grades
<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<title>Мой средний балл</title>

<style>
body {
    font-family: Arial;
    background: #f2f4f7;
    padding: 50px;
}

.container {
    max-width: 600px;
    margin: auto;
    padding: 30px;
    background: white;
    border-radius: 20px;
    box-shadow: 0 10px 30px #ddd;
}

h1 {
    text-align: center;
}

input, button {
    width: 100%;
    padding: 14px;
    margin-top: 10px;
    box-sizing: border-box;
    font-size: 16px;
    border-radius: 10px;
}

input {
    border: 1px solid #ccc;
}

button {
    background: #333;
    color: white;
    border: none;
    cursor: pointer;
}

#result {
    margin-top: 25px;
    padding: 20px;
    background: #f5f5f5;
    border-radius: 15px;
    text-align: center;
}

.average {
    font-size: 40px;
    font-weight: bold;
}
</style>
</head>

<body>

<div class="container">

<h1>📚 Мой средний балл</h1>

<p>Введи свои оценки</p>

<input id="subject" placeholder="Предмет">

<input id="grades" placeholder="5, 4, 5, 3">

<button onclick="calculate()">Рассчитать</button>

<div id="result" style="display:none">

<h2 id="name"></h2>

<div class="average" id="average"></div>

<p id="message"></p>

</div>

</div>

<script>

let gradesInput = document.getElementById("grades");

gradesInput.addEventListener("input", function() {

    let value = this.value.replace(/[^2-5]/g, "");

    let result = "";

    for (let i = 0; i < value.length; i++) {

        if (i > 0) result += ", ";

        result += value[i];

    }

    this.value = result;
});


function calculate() {

    let text = gradesInput.value;

    let grades = text.split(",").map(Number);

    let sum = 0;

    for (let grade of grades) {
        sum += grade;
    }

    let average = sum / grades.length;

    document.getElementById("result").style.display = "block";

    document.getElementById("name").textContent =
        document.getElementById("subject").value || "Мой предмет";

    document.getElementById("average").textContent =
        average.toFixed(2);

    if (average >= 4.6) {

        document.getElementById("message").textContent =
            "🎉 Средний балл уже 4.6 или выше!";

    } else {

        let fives = 0;

        while ((sum + fives * 5) /
               (grades.length + fives) < 4.6) {

            fives++;
        }

        document.getElementById("message").textContent =
            "🎯 Нужно ещё " + fives + " пятёрок до 4.6.";

    }
}

</script>

</body>
</html>
