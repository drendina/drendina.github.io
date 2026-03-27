<!DOCTYPE html>
<html lang="it">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Menù Festa</title>

<style>
body {
  font-family: Arial;
  background: #f5f5f5;
  margin: 0;
  padding: 10px;
}

h2 {
  background: #333;
  color: white;
  padding: 10px;
  border-radius: 8px;
}

.item {
  display: flex;
  justify-content: space-between;
  background: white;
  margin: 5px 0;
  padding: 10px;
  border-radius: 8px;
}

.controls button {
  padding: 5px 10px;
  font-size: 16px;
}

.cart {
  position: fixed;
  bottom: 0;
  left: 0;
  right: 0;
  background: #222;
  color: white;
  padding: 15px;
}

</style>
</head>

<body>

<h2>🍕 Pizze</h2>
<div id="menu"></div>

<h2>🛒 Il tuo ordine</h2>
<div id="cart"></div>

<div class="cart">
  Totale: € <span id="total">0</span>
</div>

<script>

const menuItems = [
  {name:"Margherita", price:5},
  {name:"Pizza farcita", price:5.5},

  {name:"Panino con salume", price:2},
  {name:"Piadina con salume", price:2.5},
  {name:"Tramezzino con salume", price:2},
  {name:"Panino vuoto", price:0.5},
  {name:"Polenta", price:1},
  {name:"Fetta di torta", price:1.5},

  {name:"Panino con salamella", price:3},
  {name:"Polenta con salamella", price:3},

  {name:"Patatine fritte", price:2},
  {name:"Torta fritta con salume", price:5.5},
  {name:"Torta fritta con zola", price:5.5},

  {name:"Crespelle", price:4.5},
  {name:"Tagliatelle al pomodoro", price:3},
  {name:"Tagliatelle al ragù", price:4},
  {name:"Tagliatelle al sugo di lepre", price:4.5},
  {name:"Roastbeef all’inglese", price:5},
  {name:"Spiedini di carne", price:5},

  {name:"Acqua 0.5L", price:0.6},
  {name:"Bibita lattina", price:1.2},
  {name:"Bottiglia vino", price:4.5},
  {name:"Birra 0.33", price:2},
  {name:"Birra piccola", price:2.5},
  {name:"Birra media", price:3.5},
  {name:"Caffè", price:1}
];

let cart = {};

const menuDiv = document.getElementById("menu");
const cartDiv = document.getElementById("cart");

menuItems.forEach(item => {
  const div = document.createElement("div");
  div.className = "item";

  div.innerHTML = `
    <span>${item.name} (€${item.price})</span>
    <div class="controls">
      <button onclick="removeItem('${item.name}')">-</button>
      <span id="qty-${item.name}">0</span>
      <button onclick="addItem('${item.name}', ${item.price})">+</button>
    </div>
  `;

  menuDiv.appendChild(div);
});

function addItem(name, price){
  if(!cart[name]) cart[name] = {qty:0, price};
  cart[name].qty++;
  update();
}

function removeItem(name){
  if(cart[name]){
    cart[name].qty--;
    if(cart[name].qty <= 0) delete cart[name];
  }
  update();
}

function update(){
  cartDiv.innerHTML = "";
  let total = 0;

  for(let name in cart){
    let item = cart[name];
    total += item.qty * item.price;

    cartDiv.innerHTML += `<div>${name} x${item.qty}</div>`;
    document.getElementById("qty-"+name).innerText = item.qty;
  }

  document.getElementById("total").innerText = total.toFixed(2);
}

</script>

</body>
</html>
