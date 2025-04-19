<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Kripss Shop</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <!-- Tailwind CSS -->
  <link href="https://cdn.jsdelivr.net/npm/tailwindcss@2.2.19/dist/tailwind.min.css" rel="stylesheet">
  <!-- Font Awesome Icons -->
  <script src="https://kit.fontawesome.com/a076d05399.js" crossorigin="anonymous"></script>
  <!-- Favicon -->
  <link rel="icon" type="image/png" href="https://cdn-icons-png.flaticon.com/512/3144/3144456.png" />
</head>

<body class="bg-blue-500 text-white">

  <!-- Welcome Page -->
  <div id="welcome-page" class="flex flex-col items-center justify-center min-h-screen text-center px-4 sm:px-6 lg:px-8">
    <h1 class="text-4xl sm:text-5xl font-bold mb-6">Welcome to Kripss 🛍️</h1>
    <button onclick="showLoginForm()" class="py-2 px-6 bg-white text-blue-600 rounded-full flex items-center gap-2">
      <i class="fas fa-user"></i> Login
    </button>
  </div>

  <!-- Login Form Modal -->
  <div id="login-form" class="hidden fixed inset-0 flex justify-center items-center bg-black bg-opacity-70 z-20">
    <div class="bg-white p-8 rounded-xl text-black w-80 sm:w-96">
      <h2 class="text-2xl mb-4">Login</h2>
      <input id="username" type="text" placeholder="Username" class="border p-2 w-full mb-4" />
      <input id="password" type="password" placeholder="Password" class="border p-2 w-full mb-4" />
      <button onclick="loginUser()" class="w-full py-2 bg-blue-600 text-white rounded hover:bg-blue-500">Login</button>
      <button onclick="closeLoginForm()" class="mt-3 text-gray-600">Cancel</button>
    </div>
  </div>

  <!-- Shop Page -->
  <div id="shop-page" class="hidden p-6">
    <h1 class="text-3xl sm:text-4xl font-bold mb-6">Kripss Shop 🛒</h1>
    <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6 mb-10" id="products-container"></div>

    <div class="p-4 bg-white text-black rounded-xl">
      <h2 class="text-2xl font-bold mb-4">Cart Summary</h2>
      <ul id="cart-summary" class="mb-4"></ul>
      <p class="text-xl font-semibold mb-4">Total: $<span id="total-price">0.00</span></p>
      <button class="w-full py-2 bg-blue-600 text-white rounded flex items-center justify-center gap-2">
        <i class="fas fa-credit-card"></i> Checkout
      </button>
    </div>
  </div>

  <script>
    const products = [
      { id: 1, name: 'Instagram Chart Poster', price: 29.99, image: 'https://via.placeholder.com/300x300?text=Poster', video: 'https://www.w3schools.com/html/mov_bbb.mp4' },
      { id: 2, name: 'Ronaldo Signed Jersey', price: 149.99, image: 'https://via.placeholder.com/300x300?text=Jersey', video: 'https://www.w3schools.com/html/mov_bbb.mp4' },
      { id: 3, name: 'Growth Guide Ebook', price: 19.99, image: 'https://via.placeholder.com/300x300?text=Ebook', video: 'https://www.w3schools.com/html/mov_bbb.mp4' },
      { id: 4, name: 'Influencer Sunglasses', price: 79.99, image: 'https://via.placeholder.com/300x300?text=Sunglasses', video: 'https://www.w3schools.com/html/mov_bbb.mp4' },
      { id: 5, name: 'Viral Content Planner', price: 24.99, image: 'https://via.placeholder.com/300x300?text=Planner', video: 'https://www.w3schools.com/html/mov_bbb.mp4' },
      { id: 6, name: 'Limited Edition Hoodie', price: 59.99, image: 'https://via.placeholder.com/300x300?text=Hoodie', video: 'https://www.w3schools.com/html/mov_bbb.mp4' }
    ];

    const cart = [];

    function showLoginForm() {
      document.getElementById('login-form').classList.remove('hidden');
    }

    function closeLoginForm() {
      document.getElementById('login-form').classList.add('hidden');
    }

    function loginUser() {
      const username = document.getElementById('username').value;
      const password = document.getElementById('password').value;

      if (username && password) {
        document.getElementById('welcome-page').classList.add('hidden');
        document.getElementById('login-form').classList.add('hidden');
        document.getElementById('shop-page').classList.remove('hidden');
        loadProducts();
      } else {
        alert('Please enter a username and password!');
      }
    }

    function loadProducts() {
      const container = document.getElementById('products-container');
      container.innerHTML = '';
      products.forEach(p => {
        const div = document.createElement('div');
        div.className = 'bg-white text-black rounded-2xl p-4';
        div.innerHTML = `
          <img src="${p.image}" alt="${p.name}" class="w-full h-60 object-cover rounded-t-2xl mb-4">
          <h2 class="text-xl font-semibold mb-2">${p.name}</h2>
          <p class="text-lg mb-4">$${p.price}</p>
          <video controls class="w-full mb-4">
            <source src="${p.video}" type="video/mp4">
            Your browser does not support the video tag.
          </video>
          <button onclick="addToCart(${p.id})" class="w-full py-2 bg-blue-600 text-white rounded flex items-center justify-center gap-2">
            <i class="fas fa-shopping-cart"></i> Add to Cart
          </button>
        `;
        container.appendChild(div);
      });
    }

    function addToCart(id) {
      const product = products.find(p => p.id === id);
      cart.push(product);
      updateCart();
    }

    function updateCart() {
      const summary = document.getElementById('cart-summary');
      summary.innerHTML = '';
      cart.forEach(item => {
        const li = document.createElement('li');
        li.textContent = `${item.name} — $${item.price}`;
        summary.appendChild(li);
      });
      const total = cart.reduce((sum, p) => sum + p.price, 0).toFixed(2);
      document.getElementById('total-price').textContent = total;
    }
  </script>

</body>
</html>
