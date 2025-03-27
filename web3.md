```html
<!DOCTYPE html>
<html lang="en">
<head>
    <title>Document</title>
    <style>
        main {
            width: 100%;
            height: 100vh;
            position: relative;
        }
        .amar, .vishal, .sachin {
            width: 500px;
            height: 500px;
            position: absolute;
            transition: z-index 0.3s ease;
        }
        .amar {
            background-color: red;
            top: 0;
            left: 100px;
        }
        .vishal {
            background-color: blue;
            top: 100px;
            left: 200px;
        }
        .sachin {
            background-color: yellow;
            top: 200px;
            left: 300px;
        }
    </style>
</head>
<body>
    <main>
        <div class="amar">Amar</div>
        <div class="vishal">Vishal</div>
        <div class="sachin">Sachin</div>
    </main>

    <script>
        // Initial setup for z-index
        document.querySelector(".amar");
        document.querySelector(".vishal");
        document.querySelector(".sachin");

        function zIndex(el, n){
            el.style.zIndex = n;
        }

        // Adding event listeners for mouseenter and mouseleave
        document.querySelectorAll('.amar, .vishal, .sachin').forEach(function (el) {
            el.addEventListener("mouseenter", function() {
                zIndex(el, 10);
            });
            el.addEventListener("mouseleave", function() {
                zIndex(el, 1);
            });
        });
    </script>
</body>
</html>
```