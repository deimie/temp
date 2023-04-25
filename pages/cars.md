---
title: Cars Lab
---
Part 1: Complete Lesson Hacks on a Jupyter Notebook.
 
Part 2: PBL 

You are a teenager who has their license and wants to find a car to buy. When you go to the car dealership, you realize that there are many different things you have to keep track of. You have to keep track of the car brands you look at, the prices of the cars, phone numbers of different sales representatives, etc.

To make it easy on yourself, you want to develop a computerized code that is able to sort through different prices, car brands, etc.

In this lab, you will be creating a car registry that will allow you to keep track of different cars and their prices. You will also be able to compare prices, calculate the acceleration of the car, and find the cheapest car in the registry.

To get started, we've provided the following code in the Github repo here: https://github.com/dontran15/backend-abopsc/tree/master/src/main/java/com/nighthawk/spring_portfolio/database/lab as well as the frontend shown on this page. You will be working with the `CarLab` class and the `CarLabApiController` files

TODO:
- [ ] Clone code and run locally
- [ ] Add car make, model, mpg as attributes to CarLab class, using knowledge of different primitive types
- [ ] Add a constructor to the CarLab class that takes in the car make, model, and mpg as parameters
- [ ] Create another method based on operations on the CarLab class that uses a different data type
- [ ] Given a list of requirements for budget, mpg, and acceleration, find the cheapest car that meets all of the requirements (use boolean operators and iteration

### Car Registry

<!-- Create table to display cars -->
<table id="carsTable">
    <tr>
        <th>Name</th>
        <th>Price</th>
    </tr>
</table>

### Prices

Cheapest car is: <div id="result"></div>

<script>
    // fetch from database
    const resultTable = document.getElementById("carsTable");
    const cars_url = "https://abopsc-backend.dontntntnt.de/api/carLab";
    fetch(cars_url + "/")
        .then(response => response.json())
        .then(data => {
            console.log(data)
            // create table rows
            for (let i = 0; i < data.length; i++) {
                let row = resultTable.insertRow(-1);
                let name = row.insertCell(0);
                let price = row.insertCell(1);
                name.innerHTML = data[i].name;
                price.innerHTML = data[i].price;
            }
        });
    .catch(err => console.log(err));
    
    // find cheapest car
    const cheapestCar = document.getElementById("result");
    const cheapest_url = cars_url + "/compareprice";

    fetch(cheapest_url)
        .then(response => response.json())
        .then(data => {
            console.log(data)
            cheapestCar.innerHTML = data;
        });
    .catch(err => console.log(err));

</script>
