---
title: Cars Lab
---

### Car Registry

<!-- Create table to display cars -->

<table id="carsTable">
    <tr>
        <th>Name</th>
        <th>Price</th>
    </tr>
</table>

<script>
    // fetch from database
    const resultTable = document.getElementById("carsTable");
    const cars_url = "https://abopsc-backend.dontntntnt.de/api/carLab";
    fetch(cars_url)
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
    

</script>
