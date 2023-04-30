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
        ["id","name", "homework", "comment"],
        ["","","/3", ""],
        ["","","/3", ""],
        ["","","/3", ""],
        ["","","/3", ""],
        ["","","/3", ""],
        ["","","/3", ""],
        ["","","/3", ""],
        ["","","/3", ""],
        ["","","/3", ""],
        ["","","/3", ""],
        ["","","/3", ""],
        ["","","/3", ""],
        ["","","/3", ""],
        ["","","/3", ""],
        ["","","/3", ""],
        ["","","/3", ""],
        ["","","/3", ""]
    ]

    var objects = [];

    // // iterates through array and creates tr's and td's for each index
    function makeTableHTML(people) {
        var result = "<table>";
        result += "<thead><tr><th>Name</th><th>Score</th><th>Comment</th></thead><tbody>";
        // Create header row. Better way to do this?
        //for (var i = 0; i < array.length; i++) {
        for (var i = people.length-1; i > 0; i--) {
            result += "<tr>";
            for (var j = 1; j < people[i].length; j++) {
                result += "<td>"+people[i][j]+"</td>";   
            }   
            result += "</tr>";
        }   
        result += "</tbody></table>";
        document.getElementById("scores").innerHTML = result;
    }
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
        .then((response) => response.json())
        .then((data) => {
          console.log(data);

          for (var i in data) {
            var person = data[i];
            if(person.roles[0].name == 'ROLE_USER'){
              console.log(person.name);

              let email = {email: person.email};

              var requestOptions2 = {
                  method: 'GET',
                  headers: myHeaders,
                  mode: 'cors',
                  cache: 'default', 
                  credentials: 'include',
                  redirect: 'manual',
                  body: JSON.stringify(email)
                };  

              fetch(
                url + '/api/grading/grades', requestOptions
              )
              .then((response) => response.json())
              .then((data2) => {
                for (var j in data2){
                  var grade = grade[j];
                  console.log(grade.id);
                }
              })                
            }
          }
        })
        .catch(error => console.log('error', error));

        var result = "<table";
        result+="<thead><tr><th>Name</th><th>Homework Score</th></thead><tbody>";

        result += "</tbody></table>";
        document.getElementById("scores").innerHTML = result;
    }
    initializeTable();
</script>
