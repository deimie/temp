---
title: Lab Scores
---

### Score Rundown:

- Lab - 2 points
- Lesson - 1 point
- Total - 3 points


<html>
  <div id="scores">
  </div>
  <div id="scoringInput">
  <table id="gradesInput">
  <tr>
  <th>
  <span>email:</span>
  <input
  autocomplete="off"
  type="email"
  id="email"
  name="email"
  placeholder="enter email..."
  />
  </th>
  </tr>
  <tr>
  <th>
  <span>score</span>
  <input
  autocomplete="off"
  type="text"
  id="score"
  name="score"
  placeholder="enter score..."
  />
  </th>
  </tr>
  <tr>
  <th>
  <span>comment</span>
  <input
  autocomplete="off"
  type="text"
  id="comment"
  name="comment"
  placeholder="enter comment..."
  />
  </th>
  </tr>
  <tr>
  <th>
  <button
  class="btn"
  type="submit"
  value="Submit"
  onclick="submitScore();"
  >
  Submit
  </button>
  </th>
  </tr>
  </table>
  </div> 
</html>

<script>
    document.getElementById("gradesInput").style.display = "hide";
    if(sessionStorage.getItem("role") == "ROLE_ADMIN"){
      document.getElementById("gradesInput").style.display = "show";
    } else if (sessionStorage.getItem("role") == null || sessionStorage.getItem("role") == "ROLE_USER"){
      document.getElementById("gradesInput").style.display = "hide";
    } else {
      document.getElementById("gradesInput").style.display = "hide";
    }

    // submit scores of user (TODO: can put inputs into table)
    function submitScore(){
      var emailValue = document.getElementById("email").value;
      var scoreValue = document.getElementById("score").value;
      var commentValue = document.getElementById("comment").value;
      var assignmentName = "homework";

      console.log(emailValue);
      console.log(scoreValue);
      console.log(commentValue);

      var myHeaders = new Headers();
        myHeaders.append("Content-Type", "application/json");

      var data = { email: emailValue, assignment: assignmentName, score: scoreValue, comment: commentValue };

      var requestOptions = {
        method: 'POST',
        headers: myHeaders,
        mode: 'cors',
        cache: 'default', 
        credentials: 'include',
        redirect: 'manual',
        body: JSON.stringify(data)
      };

      fetch(
        "https://abopsc-backend.dontntntnt.de/api/grading/updateGrade",
        requestOptions
      )
        .then((response) => response.text())
        .then((text) => {
          console.log(text);
          window.location.href = "https://deimie.github.io/temp/pages/scoringtemp.html";
        })
        .catch((error) => console.log("error", error));

    }

    // iterates through array and creates tr's and td's for each index
    function makeTableHTML(people) {
        var result = "<table>";
        result += "<thead><tr><th>Name</th><th>Email</th><th>Score</th><th>Comment</th></thead><tbody>";
        // Create header row. Better way to do this?
        //for (var i = 0; i < array.length; i++) {
        for (var i = people.length-1; i > 0; i--) {
            result += "<tr>";
            for (var j = 1; j < people[i].length; j++) {
                if(people[i][j] == null){
                  result += "<td></td>";
                }else{
                  result += "<td>"+ people[i][j]+"</td>";   
                }  
            }   
            result += "</tr>";
        }   
        result += "</tbody></table>";
        document.getElementById("scores").innerHTML = result;
    }

    const url = "https://abopsc-backend.dontntntnt.de";

    async function initializeTable() {
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

        var objects = [["id","name", "email", "homeworkScore", "comment"]];

        try{
          const response = await fetch(
            url + `/api/person/all`, requestOptions
          );
          
          const data = await response.json();
          console.log(data);

          for (var i in data) {
            var person = data[i];
            if(person.roles[0].name == 'ROLE_USER'){
              console.log(person.name);
              console.log(person.email);

              var requestOptions2 = {
                  method: 'POST',
                  headers: myHeaders,
                  mode: 'cors',
                  cache: 'default', 
                  credentials: 'include',
                  redirect: 'manual',
                  body: JSON.stringify({ email: person.email })
                };  
            
                const response2 = await fetch(url + '/api/grading/grades', requestOptions2);
                const data2 = await response2.json();
                  for (var j in data2){
                    var grade = data2[j];
                    var personGradeArray = [];
                    personGradeArray.push(grade.id);
                    personGradeArray.push(grade.person.name);
                    personGradeArray.push(grade.person.email);
                    personGradeArray.push(grade.points.toString());
                    personGradeArray.push(grade.comment)
                    console.log(personGradeArray);
                    objects.push(personGradeArray);
                  }              
              }
            }    
      } catch {
        console.log("failed"); // probably can pass through response
      }

        console.log(objects);
        return objects;
    }

    async function userTable(){
      var myHeaders = new Headers();
      myHeaders.append("Content-Type", "application/json");

      var requestOptions2 = {
        method: 'POST',
        headers: myHeaders,
        mode: 'cors',
        cache: 'default', 
        credentials: 'include',
        redirect: 'manual',
        body: JSON.stringify({ email: sessionStorage.getItem("email") })
      };  

      var objects = [["id","name", "homeworkScore", "comment"]];
  
      const response2 = await fetch(url + '/api/grading/grades', requestOptions2);
      const data2 = await response2.json();

      for (var j in data2){
        var grade = data2[j];
        var personGradeArray = [];
        personGradeArray.push(grade.id);
        personGradeArray.push(grade.person.name);
        personGradeArray.push(grade.points.toString());
        personGradeArray.push(grade.comment)
        console.log(personGradeArray);
        objects.push(personGradeArray);
      }   

      return objects;
    }

    if(sessionStorage.getItem("role") == "ROLE_ADMIN"){
      initializeTable().then(result => {
        makeTableHTML(result);
      })
    }

    if(sessionStorage.getItem("role") == "ROLE_USER"){
      userTable().then(result => {
        makeTableHTML(result);
      })
    }
</script>
