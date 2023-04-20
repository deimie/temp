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
        ["name","peerLab","peerLesson","liveLab","liveLesson","total"],
        ["","/2","/1","/2","/1","/3"],
        ["","/2","/1","/2","/1","/3"],
        ["","/2","/1","/2","/1","/3"],
        ["","/2","/1","/2","/1","/3"],
        ["","/2","/1","/2","/1","/3"],
        ["","/2","/1","/2","/1","/3"],
        ["","/2","/1","/2","/1","/3"],
        ["","/2","/1","/2","/1","/3"],
        ["","/2","/1","/2","/1","/3"],
        ["","/2","/1","/2","/1","/3"],
        ["","/2","/1","/2","/1","/3"],
        ["","/2","/1","/2","/1","/3"],
        ["","/2","/1","/2","/1","/3"],
        ["","/2","/1","/2","/1","/3"],
        ["","/2","/1","/2","/1","/3"],
        ["","/2","/1","/2","/1","/3"],
        ["","/2","/1","/2","/1","/3"],
        ["","/2","/1","/2","/1","/3"],
        ["","/2","/1","/2","/1","/3"],
        ["","/2","/1","/2","/1","/3"],
        ["","/2","/1","/2","/1","/3"]

    ]

    // iterates through array and creates tr's and td's for each index
    function makeTableHTML(people) {
        var result = "<table>";
        result += "<thead><tr><th>Name</th><th>Lab Score (Peer)</th><th>Lesson Score (Peer)</th><th>Lab Score (Live)</th><th>Lab Score (Live)</th><th>Total</th></thead><tbody>";
        // Create header row. Better way to do this?
        //for (var i = 0; i < array.length; i++) {
        for (var i = people.length-1; i > 0; i--) {
            result += "<tr>";
            for (var j = 0; j < people[i].length; j++) {
                result += "<td>"+people[i][j]+"</td>";   
            }   
            result += "</tr>";
        }   
        result += "</tbody></table>";
        document.getElementById("scores").innerHTML = result;
    }
    makeTableHTML(people);


    function makeTable() {
        
    }

</script>
