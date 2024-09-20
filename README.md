<!doctype html>
<html lang="en"> 
 <head> 
  <meta charset="UTF-8"> 
  <meta name="viewport" content="width=device-width, initial-scale=1.0"> 
  <title>Shop Bill Management System</title> 
  <link rel="stylesheet" href="style.css"> 
 </head> 
 <body> 
  <div class="container"> 
   <h1>Shop Bill Management System</h1> <!-- Shop Information --> 
   <div class="shop-section"> 
    <h2>Shop Details</h2> <label for="shopName">Shop NO.:</label> 
    <input type="text" id="shopName" placeholder="Enter shop name"> 
   </div> <!-- Recipient Information --> 
   <div class="recipient-section"> 
    <h2>Recipient Details</h2> <label for="recipientName">Name:</label> 
    <input type="text" id="recipientName" placeholder="Enter recipient name"> <label for="recipientAddress">Address:</label> 
    <input type="text" id="recipientAddress" placeholder="Enter recipient address"> <label for="recipientContact">Contact:</label> 
    <input type="text" id="recipientContact" placeholder="Enter recipient contact"> 
   </div> <!-- Bill Items --> 
   <div class="bill-section"> 
    <h2>Bill Items</h2> <label for="itemName">Item Name:</label> 
    <input type="text" id="itemName" placeholder="Enter item name"> <label for="itemPrice">Item Price:</label> 
    <input type="number" id="itemPrice" placeholder="Enter item price"> <button onclick="addItem()">Add Item</button> 
   </div> <!-- Bill Display --> 
   <div class="bill-display"> 
    <h2>Bill</h2> 
    <table id="billTable"> 
     <thead> 
      <tr> 
       <th>Item Name</th> 
       <th>Item Price</th> 
      </tr> 
     </thead> 
     <tbody> 
     </tbody> 
    </table> 
    <div class="total"> <strong>Total: ₹<span id="totalPrice">0.00</span></strong> 
    </div> 
   </div> <button onclick="generateBill()">Generate Bill</button> 
   <div class="bill-result"> 
    <h2>MAHABALE PRODUCTS.LTD</h2> 
    <p id="billShop"></p> 
    <p id="billRecipient"></p> 
    <p id="billItems"></p> 
    <p>Total: ₹<span id="finalTotal">0.00</span></p> 
   </div> 
  </div> 
  <script src="script.js"></script> 
  <style>
      
      body {
    font-family: Arial, sans-serif;
    background-color: #f4f4f9;
    margin: 0;
    padding: 20px;
}

.container {
    max-width: 600px;
    margin: 0 auto;
    background: #fff;
    padding: 20px;
    border-radius: 10px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

h1, h2 {
    text-align: center;
    color: #333;
}

label {
    display: block;
    margin-bottom: 5px;
    font-weight: bold;
}

input {
    width: 100%;
    padding: 8px;
    margin-bottom: 10px;
    border: 1px solid #ccc;
    border-radius: 5px;
}

button {
    background-color: blue;
    color: white;
    border: none;
    padding: 10px 15px;
    font-size: 16px;
    border-radius: 5px;
    cursor: pointer;
}

button:hover {
    background-color: #218838;
}

table {
    width: 100%;
    border-collapse: collapse;
    margin-top: 20px;
}

table, th, td {
    border: 1px solid #ddd;
}

th, td {
    padding: 10px;
    text-align: left;
}

.total {
    margin-top: 10px;
    text-align: right;
    font-size: 18px;
}

.bill-result {
    background-color: #e9ecef;
    padding: 10px;
    margin-top: 20px;
    border-radius: 5px;
}

.bill-result p {
    margin: 0;
    padding: 5px 0;
}  
    </style> 
  <script>
      
      let items = [];
let totalPrice = 0;

function addItem() {
    const itemName = document.getElementById("itemName").value;
    const itemPrice = parseFloat(document.getElementById("itemPrice").value);

    if (itemName && itemPrice) {
        // Add item to the list
        items.push({ name: itemName, price: itemPrice });

        // Update the bill table
        const tableBody = document.querySelector("#billTable tbody");
        const newRow = tableBody.insertRow();
        newRow.insertCell(0).innerText = itemName;
        newRow.insertCell(1).innerText = `$${itemPrice.toFixed(2)}`;

        // Update total price
        totalPrice += itemPrice;
        document.getElementById("totalPrice").innerText = totalPrice.toFixed(2);

        // Clear input fields
        document.getElementById("itemName").value = '';
        document.getElementById("itemPrice").value = '';
    } else {
        alert("Please enter valid item details.");
    }
}

function generateBill() {
    const shopName = document.getElementById("shopName").value;
    const recipientName = document.getElementById("recipientName").value;
    const recipientAddress = document.getElementById("recipientAddress").value;
    const recipientContact = document.getElementById("recipientContact").value;

    if (!shopName || !recipientName || !recipientAddress || !recipientContact) {
        alert("Please enter all details (shop and recipient).");
        return;
    }

    // Display shop and recipient details
    document.getElementById("billShop").innerHTML = `<strong>Shop Name:</strong> ${shopName}`;
    document.getElementById("billRecipient").innerHTML = `
        <strong>Recipient Name:</strong> ${recipientName}<br>
        <strong>Address:</strong> ${recipientAddress}<br>
        <strong>Contact:</strong> ${recipientContact}
    `;

    // Display bill items
    let itemList = '<strong>Items:</strong><ul>';
    items.forEach(item => {
        itemList += `<li>${item.name} - $${item.price.toFixed(2)}</li>`;
    });
    itemList += '</ul>';
    document.getElementById("billItems").innerHTML = itemList;

    // Display total
    document.getElementById("finalTotal").innerText = totalPrice.toFixed(2);
}  
    </script> 
 </body>
</html>
