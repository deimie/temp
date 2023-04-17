---
title: Grading 
layout: single
permalink: /grading/
---
{% include lab_nav.html %}

## Grading Checklist Period 2 APCSA

<body>
    <table>
        <tr>
            <th>Name</th>
            <th>Score</th>
        </tr>
        <tr>
            <td>Name</td>
            <td>Score</td>
        </tr>
    </table>
    <form>
           Name:<br>
            <input type="text" id="name" name="name">
            Grade:<br>
            <input type="text" id="grade" name="grade">
            <button type="button" onclick="addRow();">Submit</button>
    </form>
</body>

<script>
    function addRow(){
        var name = document.getElementById("name").value;
        var grade = document.getElementById("grade").value;

        var table = document.getElementsByTagName("table")[0];
        var newRow = table.insertRow(1);

        var nameCell = newRow.insertCell(0);
        var gradeCell = newRow.insertCell(1);

        nameCell.innerHTML = name;
        gradeCell.innerHTML = grade; 
    }
</script>