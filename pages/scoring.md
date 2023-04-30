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
        ["Rebecca","2.9/3", "excellent, beautiful, hetvi loves you"],
        ["Pranav","2.7/3", "comprehensive code and has an output shown"],
        ["Jay","2.7/3", "comprehensive code and has an output shown"],
        ["Rithvik","2.7/3", "comprehensive code and has an output shown"],
        ["Aryan","2.7/3", "comprehensive code and has an output shown"],
        ["Tiaben","2.9/3", "it's good and there's extra credit"],
        ["Saumya","2.7/3", "comprehensive code with expected output shown"],
        ["Sophie","2.7/3", "comprehensive code with expected output shown"],
        ["Saathvika","2.9/3", "comprehensive code with expected output shown + completed ec"],
        ["Karthik","2/3", "comprehensive code with expected output shown"],
        ["Evan","2.7/3", "comprehensive code with expected output shown"],
        ["Sanjay","2.7/3", "comprehensive code with expected output shown"],
        ["Adi","2.7/3", "comprehensive code with expected output shown"],
        ["Akhil","2.7/3", "comprehensive code with expected output shown"],
        ["Tristan","2.7/3", "comprehensive code with expected output shown"],
        ["Allie","2.7/3", "comprehensive code but no output shown"],
        ["Shraddha","2.7/3", "comprehensive code with expected output shown"],
        ["Meena","2.7/3", "comprehensive code with expected output shown"],
        ["Madhumita","2.7/3", "comprehensive code with expected output shown"],
        ["Aadya","2.7/3", "comprehensive code with expected output shown"],
        ["Rohan","2.7/3", "comprehensive code with expected output shown"],
        ["Shreya","2.7/3", "comprehensive code with expected output shown"],
        ["Linda","2.7/3", "comprehensive code with code output"]
    ]

    // iterates through array and creates tr's and td's for each index
    function makeTableHTML(people) {
        var result = "<table>";
        result += "<thead><tr><th>    Name           </th><th>    Homework Score       </th><th>    Comments       </th></thead><tbody>";
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
