---
title: Assignments 
layout: single
permalink: /assignments/
---

<section id="assignments" class="level2">
<h2 class="anchored" data-anchor-id="assignments">Assignments</h2>
<ol type="1">
<li><a href="{{site.baseurl}}/grading/">Assignment 1</a></li>
<li><a href="">Assignment 2</a></li>
</ol>

<h3>
  <div id="user"></div>
  <div id="loginMessage"></div>
</h3>
<script>
  if (sessionStorage.getItem("username") == null) {
      sessionStorage.setItem("username", "Guest");
  }
  if (sessionStorage.getItem("authorized") == null) {
      sessionStorage.setItem("authorized", false);
  }
  document.getElementById("user").innerHTML = "Hello " + sessionStorage.getItem("username") + "!";
  console.log(sessionStorage.getItem("authorized"));

  if (sessionStorage.getItem("authorized") === "false") {
      document.getElementById("loginMessage").innerHTML = "You are not logged in. Please log in to access the lesson.";
  }
</script>


