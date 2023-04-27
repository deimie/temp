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
        ["name", "homeworkGrade", "comments"],
        ["Rebecca","3.3/3", "excellent, beautiful, hetvi loves you"],
        ["Pranav","2.8/3", "comprehensive code but hack 4 doesn't have an output shown"],
        ["Jay","2.8/3", "comprehensive code but hack 4 doesn't have an output shown"],
        ["Rithvik","2./8/3", "comprehensive code but hack 4 doesn't have an output shown"],
        ["Aryan","2.8/3", "comprehensive code but hack 4 doesn't have an output shown"],
        ["Tiaben","3.0/3", "it's good, but try fixing hack 4 output for scanner input"],
        ["Saumya","3.0/3", "comprehensive code with expected output shown"],
        ["Sophie","3.0/3", "comprehensive code with expected output shown"],
        ["Saathvika","3.3./3", "comprehensive code with expected output shown + completed ec"],
        ["Karthik","3.0/3", "comprehensive code with expected output shown"],
        ["Evan","3.0/3", "comprehensive code with expected output shown"],
        ["Sanjay","3.0/3", "comprehensive code with expected output shown"],
        ["Adi","3.0/3", "comprehensive code with expected output shown"],
        ["Akhil","3.0/3", "comprehensive code with expected output shown"],
        ["Tristan","3.0/3", "comprehensive code with expected output shown"],
        ["Allie","2.7/3", "comprehensive code but no output shown"],
        ["Shraddha","3.0/3", "comprehensive code with expected output shown"],
        ["Meena","3.0/3", "comprehensive code with expected output shown"],
        ["Madhumita","3.0/3", "comprehensive code with expected output shown"],
        ["Aadya","3.0/3", "comprehensive code with expected output shown"],
        ["Rohan","3.0/3", ""],
        ["Shreya","3.0/3", ""],
        ["Linda","./3", ""],
        ["Grey","./3", ""]
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


    // function makeTable() {
    //     console.log("smth");
    // }

</script>
