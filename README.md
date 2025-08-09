<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Ma Boutique en Ligne</title>
  <style>
    * {
      box-sizing: border-box;
    }

    body {
      font-family: Arial, sans-serif;
      margin: 0;
      padding: 0;
      background: #f4f4f4;
    }

    header {
      background: #333;
      color: white;
      padding: 20px;
      text-align: center;
    }

    nav {
      background: #444;
      overflow: hidden;
    }

    nav a {
      float: left;
      display: block;
      color: white;
      text-align: center;
      padding: 14px 20px;
      text-decoration: none;
    }

    nav a:hover {
      background-color: #555;
    }

    .container {
      padding: 30px;
    }

    .section {
      display: none;
    }

    .active {
      display: block;
    }

    .products {
      display: flex;
      flex-wrap: wrap;
      gap: 20px;
    }

    .product {
      background: white;
      padding: 15px;
      border: 1px solid #ccc;
      width: calc(25% - 20px);
      box-shadow: 0 0 5px rgba(0,0,0,0.1);
      text-align: center;
      border-radius: 10px;
    }

    .product img {
      width: 100%;
      height: 150px;
      object-fit: cover;
    }

    .product h3 {
      margin: 10px 0 5px;
    }

    .product p {
      font-weight: bold;
      color: green;
    }

    .product button {
      padding: 8px 12px;
      background: #28a745;
      color: white;
      border: none;
      cursor: pointer;
      border-radius: 5px;
    }

    .product button:hover {
      background: #218838;
    }

    .cart, .order-form {
      background: white;
      padding: 20px;
      border: 1px solid #ccc;
      margin-top: 30px;
      border-radius: 10px;
    }

    input, textarea {
      width: 100%;
      padding: 10px;
      margin: 10px 0;
    }

    .advertisement {
      background: url('https://via.placeholder.com/1200x200?text=Espace+Publicitaire') no-repeat center;
      background-size: cover;
      height: 200px;
      margin: 20px 0;
      border-radius: 10px;
    }

    footer {
      text-align: center;
      padding: 20px;
      background: #333;
      color: white;
    }
  </style>
</head>
<body>

<header>
  <h1>🛍️ Ma Boutique en Ligne</h1>
  <p>Achat et commande rapide en ligne</p>
</header>

<nav>
  <a href="#" onclick="showSection('accueil')">Accueil</a>
  <a href="#" onclick="showSection('produits')">Produits</a>
  <a href="#" onclick="showSection('commande')">Commander</a>
  <a href="#" onclick="showSection('contact')">Contact</a>
</nav>

<div class="container">

  <!-- Section Accueil -->
  <div id="accueil" class="section active">
    <img src="c:\Users\RDC MON PAYS\Desktop\images (2).png">
     <img src="c:\Users\RDC MON PAYS\Desktop\images (2).png">
      <img src="c:\Users\RDC MON PAYS\Desktop\images (2).png">
       <img src="c:\Users\RDC MON PAYS\Desktop\images (2).png">
    <h2>Bienvenue sur notre boutique !</h2>
    <p>Choisissez parmi nos produits et passez votre commande facilement.</p>

    <!-- Espace publicité -->
    <div class="advertisement"></div>
  </div>

  <!-- Section Produits -->
  <div id="produits" class="section">
    <h2>Nos Produits</h2>
    <div class="products">
      <div class="product">
        <img src="c:\Users\RDC MON PAYS\Desktop\images.jfif" alt="Produit 1">
        <h3>Chaussures Sport</h3>
        <p>59.99 €</p>
        <button onclick="addToCart('Chaussures Sport', 59.99)">Ajouter</button>
      </div>

      <div class="product">
        <img src="c:\Users\RDC MON PAYS\Desktop\images (2).png" alt="Produit 2">
        <h3>Montre connectée</h3>
        <p>89.99 €</p>
        <button onclick="addToCart('Montre connectée', 89.99)">Ajouter</button>
      </div>

      <div class="product">
        <img src="c:\Users\RDC MON PAYS\Desktop\images (3).png" alt="Produit 3">
        <h3>Casque Bluetooth</h3>
        <p>39.90 €</p>
        <button onclick="addToCart('Casque Bluetooth', 39.90)">Ajouter</button>
      </div>
    </div>
  </div>

  <!-- Section Commander -->
  <div id="commande" class="section">
    <h2>Passer une commande</h2>

    <div class="cart">
      <h3>Votre Panier 🛒</h3>
      <ul id="cart-items"></ul>
      <p><strong>Total :</strong> <span id="total">0.00</span> €</p>
    </div>

    <div class="order-form">
      <h3>Formulaire de commande</h3>
      <form onsubmit="return submitOrder()">
        <input type="text" id="nom" placeholder="Votre nom" required>
        <input type="email" id="email" placeholder="Votre email" required>
        <textarea id="note" placeholder="Note ou adresse de livraison" rows="4"></textarea>
        <button type="submit">Envoyer la commande</button>
      </form>
    </div>
  </div>

  <!-- Section Contact -->
  <div id="contact" class="section">
    <h2>Contact</h2>
    <p>Email : contact@ma-boutique.com</p>
    <p>Téléphone : +33 6 00 00 00 00</p>
  </div>
</div>

<footer>
  &copy; 2025 Ma Boutique - Tous droits réservés
</footer>

<script>
  let cart = [];
  let total = 0;

  function showSection(id) {
    document.querySelectorAll('.section').forEach(section => {
      section.classList.remove('active');
    });
    document.getElementById(id).classList.add('active');
  }

  function addToCart(nom, prix) {
    cart.push({ nom: nom, prix: prix });
    total += prix;
    updateCart();
  }

  function updateCart() {
    const items = document.getElementById('cart-items');
    items.innerHTML = '';
    cart.forEach(item => {
      const li = document.createElement('li');
      li.textContent = `${item.nom} - ${item.prix.toFixed(2)} €`;
      items.appendChild(li);
    });
    document.getElementById('total').textContent = total.toFixed(2);
  }

  function submitOrder() {
    const nom = document.getElementById('nom').value;
    const email = document.getElementById('email').value;
    const note = document.getElementById('note').value;

    if (cart.length === 0) {
      alert("Votre panier est vide.");
      return false;
    }

    alert(`Merci ${nom} ! Votre commande de ${cart.length} article(s) pour un total de ${total.toFixed(2)} € a été envoyée.\n\nEmail : ${email}\nNote : ${note}`);
    
    // Réinitialiser
    cart = [];
    total = 0;
    updateCart();
    document.getElementById('nom').value = '';
    document.getElementById('email').value = '';
    document.getElementById('note').value = '';

    return false; // empêche le rechargement de la page
  }
</script>

</body>
</html>




