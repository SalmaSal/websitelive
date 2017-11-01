Web Optimization project
===================
First of all I optimize all images and convert them into .png format (cheapest  ) : 
using this site http://optimizilla.com  to minimaz size of images and renamed to be : pizzeria-min.png , 2048-min.png, cam_be_like-min.png, mobilewebdev-min.png  and profilepic-min.png.


----------


#views/js/main.js
###optimize in scrolling:
```
in function  updatePositions() i take var scrollTop = document.documentElement.scrollTop || document.body.scrollTop;  remove it out of loop .
```


###Optimize 5 MS in resizing pizza: 
I got finaly 4.87 Ms :) by 

*  remove  costly redendince of calling determinDX by removing it from loop  that invok it in changePizzaSizes(size);by put document.getElementsByClassName("randomPizzaContainer");in variable called container 
```
function changePizzaSizes(size) {
    var container = document.getElementsByClassName("randomPizzaContainer");
    var dx = determineDx(container[0], size);
    var newwidth = (container[0].offsetWidth + dx) + 'px';
    for (var i = 0; i < container.length; i++) {
        container[i].style.width = newwidth;
    }
}
```
*  change all querySelectorAll to use getElementsByClassName .
*  Remove pizzasDiv declration out of for loop .
*  Remove var top declration out of for loop .
*  Remove var elem declration out of for loop .
*  use getElementById() as folowing 
```
var movingPizzas = document.getElementById('movingPizzas1');
for (var i = 0; i < (window.innerHeight/s)*cols; i++) {//change 200 Times iteration by caculate number of pizza that suitable for windows hights 
    var elem = document.createElement('img');
    elem.className = 'mover';
    elem.src = "images/pizza.png";
    elem.style.height = "100px";
    elem.style.width = "73.333px";
    elem.basicLeft = (i % cols) * s;
    elem.style.top = (Math.floor(i / cols) * s) + 'px';
    movingPizzas.appendChild(elem);
}
```
*  in  this function i change querySelector to getElementByID
        ``` 
            function changeSliderLabel(size) {
            switch(size) {
            case "1":
            document.getElementById("pizzaSize").innerHTML = "Small";
        ```
   
* When generates the sliding pizzas when the page load* **no need to repeat loop 200 times **
I use (window.innerHeight/s)*cols to calculate repetition depending on window height, where s is size of pizza cols is number of columns .


	  



#In pizza.html 
  ```
<div class="row">
<div class="col-md-12  text-center">   
```

 - Use  centered align  as bootstrap prosperity
 - so expensive to select all tags in  style.css  so I remove it to body tag 

*{
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  -box-sizing: border-box;
} 

- Remove spaces by jsbeautifier.



#Index.html	  
- Add media="print" attribute in print.css link to make sure browser apply this stylesheet only if the page is being printed.
- Add async to <script async src="js/perfmatters.js"></script>
- Add actual Images insted of url .
- Inline some css to avoid block rendering
- Remove  <link href="//fonts.googleapis.com/css?family=Open+Sans:400,700" rel="stylesheet">
and use javascript , Web Font Loader library .
