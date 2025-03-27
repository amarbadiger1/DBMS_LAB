```html
<!DOCTYPE html>
<html lang="en">
<head>
    <title>Fibonacci</title>
    <style>
        button {
            padding: 10px;
            border: 1px solid black;
            border-radius: 5px;
            cursor: pointer;
            background-color: white;
        }
        div {
            padding: 10px;
            border: 1px solid black;
            border-radius: 5px;
            margin: 10px;
            text-align: center;
        }
    </style>
</head>
<body>
    <div>
        <h1>Enter First N Fibonacci Numbers</h1>
        <button class="fibo">Generate</button>
    </div>
    <div>
        <h1>Generate Number and Its Square</h1>
        <button class="square">Generate</button>
    </div>

    <script>
        function fibo() {
            let n = prompt("Enter the number");
            let f1 = 0, f2 = 1, output = "Number\n" + f1 + "\n" + f2 + "\n";
            for (let i = 1; i < n - 1; i++) {
                let nextTerm = f1 + f2;
                f1 = f2;
                f2 = nextTerm;
                output += nextTerm + "\n";
            }
            alert(output);
        }

        function sq() {
            let n = prompt("Enter the value for n");
            let output = "Number\n";
            for (let i = 1; i <= n; i++) {
                output += i + " | " + (i * i) + "\n";
            }
            alert(output);
        }

        document.querySelector(".fibo").addEventListener("click", fibo);
        document.querySelector(".square").addEventListener("click", sq);
    </script>
</body>
</html>
```