<!doctype html>
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width,initial-scale=1">

<title>Hayden's Storm Counter Math</title>

<style>
body {
  font-family: system-ui, -apple-system, sans-serif;
  margin: 0;
  background: #eaf6fb;
  color: #123;
  padding: 20px;
  text-align: center;
}

main {
  max-width: 760px;
  margin: auto;
  background: white;
  border-radius: 24px;
  padding: 24px;
  box-shadow: 0 8px 28px #0002;
}

h1 {
  font-size: clamp(30px,7vw,52px);
}

.mission {
  font-size: 20px;
}

.problem {
  font-size: clamp(34px,9vw,64px);
  font-weight: 800;
  margin: 20px;
}

.groups {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 14px;
  flex-wrap: wrap;
}

.group {
  min-width: 120px;
  padding: 14px;
  border: 3px dashed #4b7282;
  border-radius: 18px;
}

.counter {
  font-size: 44px;
  display: inline-block;
  margin: 3px;
}

.plus {
  font-size: 42px;
  font-weight: 900;
}

.answers {
  display: flex;
  justify-content: center;
  gap: 12px;
  flex-wrap: wrap;
  margin: 24px;
}

button {
  font: inherit;
  font-size: 28px;
  font-weight: 800;
  padding: 14px 24px;
  border-radius: 16px;
  border: 2px solid #345;
  background: white;
  cursor: pointer;
  min-width: 85px;
}

button:active {
  transform: scale(.97);
}

#feedback {
  font-size: 25px;
  font-weight: 750;
  min-height: 40px;
}
</style>
</head>

<body>

<main>

<h1>🌪️ Hayden's Storm Counter Math</h1>

<p class="mission">
Storm mission: count the weather tools, add the groups,
then choose the answer.
</p>

<div id="problem" class="problem"></div>

<div id="groups" class="groups"></div>

<div id="answers" class="answers"></div>

<div id="feedback"></div>

<button id="next" style="display:none">
Next Storm ➜
</button>

<p>Touch each counter while you count it.</p>

</main>

<script>

const problems = [
  [2,3],
  [4,2],
  [1,5],
  [3,4],
  [5,3],
  [6,2],
  [4,5],
  [7,2],
  [6,4],
  [8,3]
];

const icons = [
  "🌧️",
  "⚡",
  "🌪️",
  "☁️",
  "📡",
  "🌡️",
  "💨",
  "⛈️",
  "🛰️",
  "🥽"
];

let i = 0;

function render() {

  const [a,b] = problems[i % problems.length];
  const total = a + b;
  const icon = icons[i % icons.length];

  document.getElementById("problem").textContent =
    a + " + " + b + " = ?";

  document.getElementById("groups").innerHTML =
    '<div class="group">' +
    Array(a).fill(
      '<span class="counter">' + icon + '</span>'
    ).join('') +
    '</div>' +

    '<span class="plus">+</span>' +

    '<div class="group">' +
    Array(b).fill(
      '<span class="counter">' + icon + '</span>'
    ).join('') +
    '</div>';

  let options = [
    total,
    Math.max(1,total-1),
    total+1
  ].sort(() => Math.random() - .5);

  document.getElementById("answers").innerHTML =
    options.map(n =>
      '<button onclick="check(' +
      n + ',' + total + ')">' +
      n +
      '</button>'
    ).join('');

  document.getElementById("feedback").textContent = "";

  document.getElementById("next").style.display = "none";
}

function check(answer,total) {

  if (answer === total) {

    document.getElementById("feedback").textContent =
      "✅ Correct! Great storm counting, Hayden!";

    document.getElementById("next").style.display =
      "inline-block";

  } else {

    document.getElementById("feedback").textContent =
      "Try again — count both groups carefully.";
  }
}

document.getElementById("next").onclick = function() {
  i++;
  render();
};

render();

</script>

</body>
</html>