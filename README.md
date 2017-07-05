# Website Performance Optimization portfolio project
### link to site - https://hsdeveloper147.github.io/frontend-moble-portfolio/
## Changes made to the project
### Changes in index.html
1. Placed minified version of style.css as an inline css.
2. Optimised images.
3. add async keyword in the <script> tag
    ```
    <script async src="https://www.google-analytics.com/analytics.js">
    </script> <script async src="js/perfmatters.js"></script>
    ```
4. Used webfont for loading the font
    ```<script>
        WebFont.load({google:{families: ['Open+Sans:400,700']}});
        </script>
5. Minified css and js used.
6. Added style="width: 100px; height: 50px;" for each image
7. used media property to not consider print.css when not printing
    ```<link href="css/style.css" rel="stylesheet" media="print"> ```

### Changes in main.js (frontend-mobile-portfolio/views/js/main.js)
1.Deleted determineDx function which was a cause of Forced Reflow and Modified changePizzaSizes function as below
  ```
  Iterates through pizza elements on the page and changes their widths
  function changePizzaSizes(size) {

    switch(size) {
        case "1":
          newwidth= 25;
          break;
        case "2":
          newwidth = 33.3;
          break;
        case "3":
          newwidth = 50;
          break;
        default:
          console.log("bug in sizeSwitcher");
      }

    var randomPizzas =  document.querySelectorAll(".randomPizzaContainer");

    for (var i = 0; i<randomPizzas.length; i++) {
        randomPizzas[i].style.width=newwidth+"%";
     }
  }
  ```
2. updatePositions function is chaged as below
  ```
  function updatePositions() {
  frame++;
  window.performance.mark("mark_start_frame");

  var items = document.querySelectorAll('.mover');
  // taking expression that uses layout properties outside the forloop.
  //-- Intialize a variable len to item.length
  var len = items.length;
  //-- Doing Layout read at once and the style write in a batch (loop)
  var scrollTop = (document.body.scrollTop / 1250);
  for (var i = 0; i < len; i++) {
    var phase = Math.sin( scrollTop + (i % 5));
    items[i].style.left = items[i].basicLeft + 100 * phase + 'px';
  }
  ```
3. Made a varibale movingPizza outside the forloop
  `var movingPizza = document.getElementById("movingPizzas1");`
4. Changed the number of loop iterations from 200 to 24 (multiple of 8 i.e no. of columns)
  `for (var i = 0; i < 24; i++) { ... } `
5. Whenever to access an element by Id used getElementById instead of querySelector.
6. Moved initialisation of pizzaDiv outside the for loop
    ```var pizzasDiv = document.getElementById("randomPizzas");```




