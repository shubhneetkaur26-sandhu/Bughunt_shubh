# Bughunt_shubh
There are 4 bugs in this website , 1 easy 2 moderate and 1 hard , try to find them
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>SweetSlice 🍰</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />

  <style>
    * { box-sizing: border-box; }
    body {
      margin: 0;
      font-family: 'Poppins', sans-serif;
      background: linear-gradient(135deg, #ffd1dc, #ff4f9a);
      color: #ffffff;
      min-height: 100vh;
    }

    header { text-align: center; padding: 70px 20px 40px; }
    header h1 {
      font-size: 3.2rem;
      letter-spacing: 2px;
      text-shadow: 0 6px 25px rgba(0,0,0,0.35);
    }
    header p { opacity: 0.9; font-weight: 600; }

    .products {
      max-width: 1100px;
      margin: auto;
      padding: 40px 20px 120px;
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
      gap: 28px;
    }

    .card {
      background: rgba(0,0,0,0.75);
      border-radius: 22px;
      padding: 20px;
      box-shadow: 0 30px 60px rgba(0,0,0,0.4);
      transition: transform 0.3s ease;
    }
    .card:hover { transform: translateY(-6px); }
    .card h3 { color: #ffffff; margin-bottom: 8px; }
    .price { color: #ffd36a; font-weight: 600; }

    button {
      width: 100%;
      margin-top: 12px;
      padding: 10px;
      border-radius: 999px;
      border: none;
      font-weight: 600;
      cursor: pointer;
      background: #ffffff;
      color: #ff4f9a;
    }

    #cart {
      max-width: 300px;
      margin: auto;
      padding: 20px;
      background: rgba(0,0,0,0.65);
      border-radius: 18px;
      text-align: center;
      margin-bottom: 80px;
    }

    .remove {
      margin-top: 8px;
      background: #ff4d6d;
      color: white;
      font-size: 0.85rem;
    }
  </style>
</head>
<body>

<header>
  <h1>SweetSlice</h1>
  <p>Find the bugs if you can</p>
</header>

<section class="products">
  <div class="card"><h3>Chocolate Truffle</h3><p class="price">₹450</p><button onclick="addToCart('Chocolate Truffle',450)">Add to Cart</button><button class="remove" onclick="removeOne('Chocolate Truffle')">Remove</button></div>
  <div class="card"><h3>Dark Chocolate</h3><p class="price">₹450</p><button onclick="addToCart('Dark Chocolate',450)">Add to Cart</button><button class="remove" onclick="removeOne('Dark Chocolate')">Remove</button></div>
  <div class="card"><h3>Butterscotch</h3><p class="price">₹500</p><button onclick="addToCart('Butterscotch',500)">Add to Cart</button><button class="remove" onclick="removeOne('Butterscotch')">Remove</button></div>
  <div class="card"><h3>Vanilla Cream</h3><p class="price">₹550</p><button onclick="addToCart('Vanilla Cream',550)">Add to Cart</button><button class="remove" onclick="removeOne('Vanilla Cream')">Remove</button></div>
  <div class="card"><h3>Strawberry Delight</h3><p class="price">₹550</p><button onclick="addToCart('Strawberry Delight',550)">Add to Cart</button><button class="remove" onclick="removeOne('Strawberry Delight')">Remove</button></div>
  <div class="card"><h3>Red Velvet</h3><p class="price">₹600</p><button onclick="addToCart('Red Velvet',600)">Add to Cart</button><button class="remove" onclick="removeOne('Red Velvet')">Remove</button></div>
  <div class="card"><h3>Blueberry Cheesecake</h3><p class="price">₹650</p><button onclick="addToCart('Blueberry Cheesecake',650)">Add to Cart</button><button class="remove" onclick="removeOne('Blueberry Cheesecake')">Remove</button></div>
  <div class="card"><h3>Caramel Crunch</h3><p class="price">₹700</p><button onclick="addToCart('Caramel Crunch',700)">Add to Cart</button><button class="remove" onclick="removeOne('Caramel Crunch')">Remove</button></div>
</section>

<div id="cart">
  <h3>Cart</h3>
  <p>Items: <span id="itemCount">0</span></p>
  <p>Total: ₹<span id="total">0</span></p>
</div>

<script>
  let cart = [];

  function addToCart(name, price) {
    cart.push({ name, price });
    updateCart();
  }

  function removeOne(name) {
    const index = cart.findIndex(item => item.name === name);
    if (index !== -1) cart.splice(index, 1);
    updateCart();
  }

  function updateCart() {
    let total = 0;

    cart.forEach(item => {
      let price = item.price;

      // MODERATE BUG: truffle adds extra 20
      if (item.name === 'Chocolate Truffle') price += 20;

      total += price;
    });

    // EASY BUG: extra 50 added after 2 items
    if (cart.length > 2) total += 50;

    // MODERATE BUG: shows limit 5 but keeps adding
    if (cart.length === 5) alert('Cart limit reached');

    // HARD BUG: discount auto applied above 4000
    if (total > 4000) total -= 500;

    document.getElementById('itemCount').innerText = cart.length;
    document.getElementById('total').innerText = total;
  }
</script>

</body>
</html>