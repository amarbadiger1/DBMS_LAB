```html
<!DOCTYPE html>
<html >
<head>
    <title>Fruit Store</title>
    <script type="text/javascript">
        function calculateTotal() {
            var applePrice = 0.59, orangePrice = 0.49, bananaPrice = 0.39;
            var total = 0;

            // Get quantity and calculate cost for each fruit
            if (document.getElementById("apple").checked) {
                var appleQty = parseInt(document.getElementById("apple_qty").value) || 0;
                total += appleQty * applePrice;
            }
            if (document.getElementById("orange").checked) {
                var orangeQty = parseInt(document.getElementById("orange_qty").value) || 0;
                total += orangeQty * orangePrice;
            }
            if (document.getElementById("banana").checked) {
                var bananaQty = parseInt(document.getElementById("banana_qty").value) || 0;
                total += bananaQty * bananaPrice;
            }

            // Calculate tax and final amount
            var tax = total * 0.05;
            var finalTotal = total + tax;

            alert("Your total cost is $" + finalTotal.toFixed(2));

            return false; // Prevent form submission
        }
    </script>
</head>
<body>
    <h2>Fruit Store</h2>
    <form onsubmit="return calculateTotal();">
        <label>
            <input type="checkbox" id="apple" /> Apple (59 cents each)
        </label>
        Quantity: <input type="text" id="apple_qty" value="1" size="3" /><br/><br/>

        <label>
            <input type="checkbox" id="orange" /> Orange (49 cents each)
        </label>
        Quantity: <input type="text" id="orange_qty" value="1" size="3" /><br/><br/>

        <label>
            <input type="checkbox" id="banana" /> Banana (39 cents each)
        </label>
        Quantity: <input type="text" id="banana_qty" value="1" size="3" /><br/><br/>

        <input type="submit" value="Calculate Total" />
    </form>
</body>
</html>


```