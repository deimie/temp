---
title: Quiz
---

<!--Honestly I have no idea what build_revision is, you might just have to delete it if it's causing problems-->
<link href="{{ '/quiz/?v=' | append: site.github.build_revision | relative_url }}">

<h2>Quiz</h2>
<ul class="quiz" id="quiz">

</ul>
<button class="score-questions" onclick="returnScore()" id="check">Check</button>
<span id="results" class="results">Your score is -/-</span>

<script>


    // If not logged in, redirect to login
    if (!sessionStorage.getItem("authorized")) window.location.href = "https://deimie.github.io/temp/pages/userControl.html";

    const question_answer_map = new Map();
    var question_count = 0;

    var currentUrl = window.location.href;
    let url = new URL(currentUrl);
    let urlParams = new URLSearchParams(url.search);
    var problem_set_name = parseString(urlParams.get("name"));

    create_questions(problem_set_name);

    function create_questions(name) {
        

        url = "https://abopsc-backend.dontntntnt.de/api/problem/getProblemSetMC";

        const body = {
            method : "POST",
            headers : {
                "Content-Type" : "application/json"
            },
            credentials : "include",
            body: JSON.stringify({name : name})
        }

        fetch(url, body).then(data => data.json()).then(data => {
            problem_set_data = data;
            var questionNumber = 0;
            Object.keys(data).forEach(q => {
                const container = Document.createElement("li");
                const questionElem = Document.createElement("h4");
                questionElem.innerHTML = q;
                questionElem.id = "q" + questionNumber;
                container.appendChild(questionElem);

                const choices = document.createElement("ul");
                choices.classList = "choices";

                // Add answer choices to each question
                Object.keys(data.get(q)).forEach(r => {
                    const li = document.createElement("li");
                    const label = document.createElement("label");
                    const input = document.createElement("input");
                    input.type = "radio";
                    input.name = "question" + questionNumber;
                    const span = document.createElement("span");
                    span.innerHTML = r;
                    label.appendChild(input);
                    label.appendChild()
                    li.appendChild(label);
                    choices.appendChild(li);

                    // Store answers
                    if (data.get(q).get(r)) {
                        question_answer_map.set(q, r);
                    }
                })

                container.appendChild(choices);

                document.getElementById("quiz").appendChild(container);

                questionNumber++;
                question_count++;
            })
        });

        // Passes in name of radio set and question, returns boolean
        function checkQuestion(question, radioName) {
            var radios = document.getElementsByName(radioName);
            var correctness = undefined;
            for (var y = 0; y < radios.length; y++) {
                radios[y].disabled = true;
                if (radios[y].checked) correctness = question_answer_map.get(question) == radios[y].innerHTML;
            }
            return correctness;
        }

        function getScore() {
            document.getElementById("check").disabled = true;
            var score = 0;
            for (var i = 0; i < question_count; i++) {
                if (checkQuestion(Document.getElementById("q" + i).innerHTML, "question" + i)) {
                    score++;
                } else {
                    document.getElementById("q" + i).style.color = "red";
                }
            }
            return score;
        }

        // REMEMBER TO GET USER EMAIL AND PASSWORD
        function returnScore() {
            var number_score = getScore();
            var json_body = {sessionStorage.getItem("email"), }
            document.getElementById("results").innerHTML = "Your score is " + number_score + "/" + question_count

            // TODO: Create backend POST CORS for receiving scores and change url
            fetch("https://abopsc-backend.dontntntnt.de/api/problem/score",
                {
                    method : "POST",
                    headers : {
                        "Content-Type" : "application/json"
                    },
                    credentials : "include",
                    body : JSON.stringify({email : sessionStorage.getItem("email"), name : problem_set_name, score : number_score});
                }
            );
        }
    }
</script>