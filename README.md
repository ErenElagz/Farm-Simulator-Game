# Farming Simulator Game Using JavaScript
The Farm Game starts on a small farm where you have a barn and a field. You start the game with a few animals, a few fields, and $5000. Your goal is to produce goods every week, sell them in the marketplace, and invest the money you earn. But beware! Prices change every week. Sometimes they crash, and sometimes they soar. 

It's your turn: will you sell what you have now, or wait for better prices? 

---

## Installation
To get started:
```bash
Download the project and open the `index.html` file in your browser. That's it!
```

---

## Features
- Manage 3 types of animals and 3 types of plants.
- Produce and sell 3 animal products and 3 plant products.
- Weekly consumption of feed and fertilizer for your farm.
- Dynamic weekly production and price fluctuations.
- View price history (last two weeks).
- Detailed UI design for ease of use.
- Buy and sell resources in the marketplace.
- Track your farm statistics.

---

## Documentation

### How to Play
It's a turn-based farm management game. Your ultimate goal is to build the largest and most profitable farm. Here are some key gameplay tips:

1. **Resource Management**: Make sure you have enough animal feed and plant fertilizer. These are consumed every week based on the number of animals and plants you own.
2. **Production**: Animals and plants produce goods weekly, depending on their type and production coefficients.
3. **Marketplace**: Decide when to sell your products. Prices change weekly, so timing your sales is crucial.
4. **Invest Wisely**: Use your earnings to buy more animals, plants, or resources to expand your farm.
5. **Survival**: Avoid running out of essential resources. If you don't have enough feed or fertilizer, your animals and plants may perish.

Good luck managing your farm! 🌾🐄

---

## Used Technologies and Standards
1. **HTML**: For structuring the web application.
2. **CSS**: For styling and layout.
3. **Bootstrap v5.3**: For responsive and modern UI components.
4. **JavaScript**: Core game logic and interactivity.
5. **JS DOM**: Dynamic updates to the game interface.

---

## Functions Overview

### Pricing Function
The `Pricing()` function updates the price of all items (animals, plants, and products) based on random coefficients. Prices fluctuate weekly, mimicking a dynamic market system.
```javascript
function Pricing() {
    function getRandomCoefficient(min, max) {
        return Math.random() * (max - min) + min;
    }
    for (let i of animalList) {
        i.lastLastPrice = i.lastPrice;
        i.lastPrice = i.price;
        i.price = Math.round(i.price * getRandomCoefficient(0.97, 1.03) * 100) / 100;
    }
    for (let i of plantList) {
        i.lastLastPrice = i.lastPrice;
        i.lastPrice = i.price;
        i.price = Math.round(i.price * getRandomCoefficient(0.94, 1.07) * 100) / 100;
    }
    for (let i of productionList) {
        i.lastLastPrice = i.lastPrice;
        i.lastPrice = i.price;
        i.price = Math.round(i.price * getRandomCoefficient(0.9, 1.1) * 100) / 100;
    }
}
```

### Production Function
The `Production()` function calculates the weekly production of goods based on the number of animals and plants, as well as their respective production coefficients.
```javascript
function Production() {
    milk.number = milk.number + cow.number * cow.productionCoefficient;
    wool.number = wool.number + sheep.number * sheep.productionCoefficient;
    egg.number = egg.number + chicken.number * chicken.productionCoefficient;
    fabric.number = fabric.number + cotton.number * cotton.productionCoefficient;
    fame.number = fame.number + wheat.number * wheat.productionCoefficient;
    oil.number = oil.number + sunflower.number * sunflower.productionCoefficient;
}
```

### Weekly Consumption
The `WeeklyConsumption()` function manages the weekly consumption of feed and fertilizer. If resources run out, animals or plants are lost.
```javascript
function WeeklyConsumption() {
    for (let i of animalList) {
        feed.number -= i.consumptionCoefficient * i.number;
    }
    if (feed.number < 0) {
        alert("Animal Feed is Low. Buy feed or animals will die.");
        cow.number -= 1;
        sheep.number -= 2;
        chicken.number -= 5;
        feed.number = 0;
    }
    for (let i of plantList) {
        fertilizer.number -= i.consumptionCoefficient * i.number;
    }
    if (fertilizer.number < 0) {
        alert("Plant Fertilizer is Low. Buy fertilizer or plants will fade.");
        cotton.number -= 1;
        wheat.number -= 2;
        sunflower.number -= 2;
        fertilizer.number = 0;
    }
}
```

### Marketplace Functions
#### Buy Function
Allows players to buy products from the marketplace if they have enough money.
```javascript
function MarketplaceBuy() {
    if (MarketplaceBuyForm.value < 1) {
        alert("Must be bigger than zero");
    } else {
        let selectedProduct = productList[Number(MarketplaceBuySelect.value)];
        if (myFarm.money < selectedProduct.price * Number(MarketplaceBuyForm.value)) {
            alert("Money not enough.");
        } else {
            myFarm.money -= selectedProduct.price * Number(MarketplaceBuyForm.value);
            selectedProduct.number += Number(MarketplaceBuyForm.value);
        }
    }
}
```
#### Sell Function
Allows players to sell products to the marketplace and earn money.
```javascript
function MarketplaceSell() {
    if (MarketplaceSellForm.value < 1) {
        alert("Must be bigger than zero");
    } else {
        let selectedProduct = productList[Number(MarketplaceSellSelect.value)];
        if (selectedProduct.number < Number(MarketplaceSellForm.value)) {
            alert("Not enough products.");
        } else {
            myFarm.money += selectedProduct.price * Number(MarketplaceSellForm.value);
            selectedProduct.number -= Number(MarketplaceSellForm.value);
        }
    }
}
```

### Display Functions
The `DisplayAllItems()` function dynamically updates the UI with current stats, weekly production, prices, and inventory.
```javascript
function DisplayAllItems() {
    // Update stats and inventory
    TotalFarmValue.innerHTML = myFarm.TotalFarmValue();
    Money.innerHTML = myFarm.money;
    WeekCounter.innerText = `${week} week`;
    week++;
}
```

---

## Screenshots

### Weekly Production
![Weekly Production](https://user-images.githubusercontent.com/125195062/229364226-a226d9d3-f93a-4aa5-9e25-8ea8706a7b38.png)

### Marketplace Buy/Sell
![Marketplace](https://user-images.githubusercontent.com/125195062/229364234-5255de10-3659-4ca7-9774-dd31ae622db4.png)

### Other Images
![Screenshot 2023-04-02 184618](https://user-images.githubusercontent.com/125195062/229364235-e63b04a5-523e-4608-8464-7b219e8b61db.png)
![Screenshot 2023-04-02 184605](https://user-images.githubusercontent.com/125195062/229364238-e63ed4d5-679e-47ff-bbde-ee352804c0f2.png)
![Screenshot 2023-06-24 111744](https://github.com/ErenElagz/Farm-Simulator-Game/assets/125195062/ef4be995-0aed-4e00-a0c7-55262ccf8e50)

---

## License
This project is licensed under the [MIT License](https://choosealicense.com/licenses/mit/).

---

## 🔗 Links
[![GitHub](https://img.shields.io/badge/my_portfolio-000?style=for-the-badge&logo=ko-fi&logoColor=white)](https://github.com/ErenElagz)
[![Twitter](https://img.shields.io/badge/twitter-1DA1F2?style=for-the-badge&logo=twitter&logoColor=white)](https://twitter.com/erenelagz)

---

## Support, Contact, and Feedback
If you have any questions or feedback, feel free to reach out to me at **elagzeren@gmail.com**.

> **Happy farming! 🌱**

