---
title: Lab Scores
---

### Score Rundown:

- Lab - 2 points
- Lesson - 1 point
- Total - 3 points

<body>
    <div id="scores">
    </div>
</body>

<script>
    // put all scores and names in this array (order Z at top, A at bottom)
    let people = [
        ["name","homework", "comment"],
        ["","/2", ""],
        ["","/2", ""],
        ["","/2", ""],
        ["","/2", ""],
        ["","/2", ""],
        ["","/2", ""],
        ["","/2", ""],
        ["","/2", ""],
        ["","/2", ""],
        ["","/2", ""],
        ["","/2", ""],
        ["","/2", ""],
        ["","/2", ""],
        ["","/2", ""],
        ["","/2", ""],
        ["","/2", ""],
        ["","/2", ""],
    ]

    // // iterates through array and creates tr's and td's for each index
    // function makeTableHTML(people) {
    //     var result = "<table>";
    //     result += "<thead><tr><th>Name</th><th>Lab Score (Peer)</th><th>Lesson Score (Peer)</th><th>Lab Score (Live)</th><th>Lab Score (Live)</th><th>Total</th></thead><tbody>";
    //     // Create header row. Better way to do this?
    //     //for (var i = 0; i < array.length; i++) {
    //     for (var i = people.length-1; i > 0; i--) {
    //         result += "<tr>";
    //         for (var j = 0; j < people[i].length; j++) {
    //             result += "<td>"+people[i][j]+"</td>";   
    //         }   
    //         result += "</tr>";
    //     }   
    //     result += "</tbody></table>";
    //     document.getElementById("scores").innerHTML = result;
    // }
    // makeTableHTML(people);

    const url = "https://abopsc-backend.dontntntnt.de";

    function initializeTable() {
        var myHeaders = new Headers();
        myHeaders.append("Content-Type", "application/json");

        var requestOptions = {
          method: 'GET',
          headers: myHeaders,
          mode: 'cors',
          cache: 'default', 
          credentials: 'include',
          redirect: 'manual',
        };

        fetch(
          url + `/api/person/all`, requestOptions
        )
          .then(response => response.text())
        .then(result => {
          console.log(result);
        })
        .catch(error => console.log('error', error));
        
        var result = "<table";
        result+="<thead><tr><th>Name</th><th>Homework Score</th></thead><tbody>";

        result += "</tbody></table>";
        document.getElementById("scores").innerHTML = result;
    }
    initializeTable();
</script>
