<html>
<head>
<title>my blog</title>
</head>
<body>
<p align="center"><ins><b>Arefin Ani</b></ins></p>
<div style="background-color:yellow; color:red; padding-20%;"<p> i will write later.</p><hr width="50%"/>
<input id="mysearch" name="search" type="search" placeholder="search"/>
<input id="car" type="text" list="search"/>
<datalist id="search">
<option value="tapu">
<option value="ani">
<option value="jihad">
<option value="kawser">
<option value="rifat">
<option value="rasel">
<option value="ronik">
</datalist>
<p> exam is running</p>
<p>i am now on  the madical and <br/> hanging out with my friends.</p>
<p>i am with: </p>
<p>jihad</p>
<p>rasel</p>
<p>ronik</p>
<p>kawser</p>
</div>
<p>this is like a tone</p>
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <meta http-equiv="X-UA-Compatible" content="ie=edge">
        <script src="https://cdnjs.cloudflare.com/ajax/libs/p5.js/0.9.0/p5.min.js" integrity="sha256-WVsM3xrcqyuFNF3W1qtIKbHFsD0977nDQA8DCMp1zCw=" crossorigin="anonymous"></script>
        <title>Sorting Algorithms</title>
        <style>
        
        #p5Section{

            position: relative;
            margin: auto;
            width: 100%;

        }

        #p5Div{

            position: relative;
            margin: auto;
            border: 1px solid black;
            height: 200px;
            width: 300px;

        }

        </style>
    </head>
    <body>
        <section id="mySection">
            <div id="p5Section">
                <div id="p5Div" class="flags"></div>
            </div>
        </section>
        <script>

            var p5Canvas;
            var myArr = buildArr((Math.ceil(Math.random()*60))+10);
            var resultsArray = [];
            var sortingNames = ["Insertion Sort","Selection Sort","Merge Sort","Quick Sort","Bubble Sort","Shell Sort"];
            var maxNum = Math.max(...myArr);
            var m = 0;
            var frames = 10;
            var randType;
            var sortingType = [];
            var newArr = [];
            var restArr = [];
            var midArr = [];

            function setup(){

                p5Canvas = createCanvas(300,200);
                p5Canvas.parent("p5Div");
                frameRate(frames);

            }

            function draw(){

                //console.log(m);

                clear();
                noStroke();

                x = p5Canvas.width;
                y = p5Canvas.height;

                myText = ""+sortingNames[randType];

                fill(0);
                textSize(36);
                textAlign(LEFT,TOP);
                text(""+myText,5,5);

                noStroke();

                for(k=0; k<myArr.length; k++){

                    var col = "rgb("+Math.floor((resultsArray[m][k]/(myArr.length-1))*(255/2))+","+Math.floor((resultsArray[m][k]/(myArr.length-1))*(255/2))+",255)";
                    fill(""+col);
                    rect(((k+0.05)/myArr.length)*x,((maxNum-resultsArray[m][k])/maxNum)*y,(x/(myArr.length))-1.5,(resultsArray[m][k]/maxNum)*y);

                }

                if(m < (resultsArray.length-1)){

                    m++;

                } else {

                    noLoop();
                    setTimeout(loadNewDraw,1500);

                }

            }

            function loadNewDraw(){

                m = 0;
                frameRate(frames);
                myArr = buildArr((Math.ceil(Math.random()*50))+10);
                maxNum = Math.max(...myArr);
                resultsArray = [];
                newArr = [];
                restArr = [];
                midArr = [];
                randType = Math.floor(Math.random()*sortingType.length);
                //console.log(randType);
                //console.log(""+(sortingNames[randType]));
                sortingType[randType](myArr);
                loop();

            }

            /* -- */

            function buildArr(len){

                var arr = new Array(len);

                for(let i=0; i<len; i++){

                    var num = Math.floor(Math.random()*len)+1;

                    if(arr.indexOf(num) == -1){

                        arr[i] = num;

                    } else {

                        i--;

                    }

                }

                //console.log(arr);
                return arr;

            }

            /* -- */

            let insertionSort = (inputArr) => {
                let length = inputArr.length;
                for (let i = 1; i < length; i++) {
                    let key = inputArr[i];
                    let j = i - 1;
                    while (j >= 0 && inputArr[j] > key) {
                        inputArr[j + 1] = inputArr[j];
                        j = j - 1;
                    }
                    inputArr[j + 1] = key;
                    resultsArray.push(inputArr.slice(0));
                    //console.log(inputArr);
                }
                return inputArr;
            };

            /* -- */

            let selectionSort = (inputArr) => {
                let len = inputArr.length;
                for (let i = 0; i < len; i++) {
                    let min = i;
                    for (let j = i + 1; j < len; j++) {
                        if (inputArr[min] > inputArr[j]) {
                            min = j;
                        }
                    }
                    if (min !== i) {
                        let tmp = inputArr[i];
                        inputArr[i] = inputArr[min];
                        inputArr[min] = tmp;
                    }
                    resultsArray.push(inputArr.slice(0));
                    //console.log(inputArr);
                }
                return inputArr;
            }

            /* -- */

            // Merge Sort Implentation (Recursion)
            function mergeSort (unsortedArray) {

                // No need to sort the array if the array only has one element or empty
                if (unsortedArray.length <= 1) {
                    midArr.push(unsortedArray);
                    //console.log(midArr[midArr.length-1]);
                    for(let i=0; i<restArr.length; i++){

                        if(restArr.indexOf(restArr[i],(i+1)) != -1 || midArr[midArr.length-1].indexOf(restArr[i],i) != -1){

                            restArr.shift();
                            i--;

                        }

                    }
                    //console.log("left: "+newArr);
                    //console.log("right: "+restArr);
                    resultsArray.push(newArr.slice(0).concat(midArr[midArr.length-1]).concat(restArr.slice(0)));
                    //console.log("--");
                    newArr.push(unsortedArray[0]);
                    return unsortedArray;
                }
                // In order to divide the array in half, we need to figure out the middle
                const middle = Math.floor(unsortedArray.length / 2);

                //console.log(unsortedArray[middle]);

                // This is where we will be dividing the array into left and right
                const left = unsortedArray.slice(0, middle);
                const right = unsortedArray.slice(middle);

                //console.log("left: " +newArr);

                restArr = right.concat(restArr);

                if(left.length > 1){

                    midArr.push(left);
                    //console.log(midArr[midArr.length-1]);
                    //console.log("left: "+newArr);

                    for(let i=0; i<restArr.length; i++){

                        if(restArr.indexOf(restArr[i],(i+1)) != -1 || midArr[midArr.length-1].indexOf(restArr[i],i) != -1){

                            restArr.shift();
                            i--;

                        }

                    }
                    
                    //console.log("right: "+restArr);
                    resultsArray.push(newArr.slice(0).concat(midArr[midArr.length-1]).concat(restArr.slice(0)));
                    //console.log("--");     

                }

                // Using recursion to combine the left and right
                return merge(
                    mergeSort(left), mergeSort(right)
                );
                
            }

            // Merge the two arrays: left and right
            function merge (left, right) {

                var resultArray = [], leftIndex = 0, rightIndex = 0;

                // We will concatenate values into the resultArray in order
                while (leftIndex < left.length && rightIndex < right.length) {
                    if (left[leftIndex] < right[rightIndex]) {
                        resultArray.push(left[leftIndex]);
                        leftIndex++; // move left array cursor
                    } else {
                        resultArray.push(right[rightIndex]);
                        rightIndex++; // move right array cursor
                    }

                }

                midArr.push(resultArray.concat(left.slice(leftIndex)).concat(right.slice(rightIndex)).slice(0));
                //console.log(midArr[midArr.length-1]);

                for(let i=newArr.length-1; i>=0; i--){

                    if(midArr[midArr.length-1].indexOf(newArr[i]) != -1){

                        newArr.pop();

                    }

                }

                //console.log("left: "+newArr);

                restArr = right.concat(restArr);

                for(let i=0; i<restArr.length; i++){

                    if(restArr.indexOf(restArr[i],(i+1)) != -1 || midArr[midArr.length-1].indexOf(restArr[i],i) != -1){

                        restArr.shift();
                        i--;

                    }

                }

                //console.log("right: "+restArr);

                resultsArray.push(newArr.slice(0).concat(midArr[midArr.length-1]).concat(restArr.slice(0)));

                //console.log("--");

                if(midArr[midArr.length-1].length > 1){

                    newArr = newArr.concat(midArr[midArr.length-1]);

                }

                // We need to concat here because there will be one element remaining
                // from either left OR the right
                return resultArray
                        .concat(left.slice(leftIndex))
                        .concat(right.slice(rightIndex));

                
            }

            /* -- */

            const defaultComparator = (a, b) => {
                if (a < b) {
                    return -1;
                }
                if (a > b) {
                    return 1;
                }
                return 0;
            };

            const quickSort = (
                unsortedArray,
                comparator = defaultComparator
            ) => {

                // Create a sortable array to return.
                const sortedArray = [ ...unsortedArray ];

                //console.log(sortedArray);

                // Recursively sort sub-arrays.
                const recursiveSort = (start, end) => {

                    // If this sub-array is empty, it's sorted.
                    if (end - start < 1) {
                        return;
                    }

                    const pivotValue = sortedArray[end];
                    let splitIndex = start;
                    for (let i = start; i < end; i++) {

                        const sort = comparator(sortedArray[i], pivotValue);

                        // This value is less than the pivot value.
                        if (sort === -1) {

                            // If the element just to the right of the split index,
                            //   isn't this element, swap them.
                            if (splitIndex !== i) {
                                const temp = sortedArray[splitIndex];
                                sortedArray[splitIndex] = sortedArray[i];
                                sortedArray[i] = temp;
                            }
                            
                            resultsArray.push(sortedArray.slice(0));
                            

                            // Move the split index to the right by one,
                            //   denoting an increase in the less-than sub-array size.
                            splitIndex++;
                        }

                        // Leave values that are greater than or equal to
                        //   the pivot value where they are.
                    }

                    // Move the pivot value to between the split.
                    sortedArray[end] = sortedArray[splitIndex];
                    sortedArray[splitIndex] = pivotValue;

                    //console.log(sortedArray);

                    // Recursively sort the less-than and greater-than arrays.
                    recursiveSort(start, splitIndex - 1);
                    recursiveSort(splitIndex + 1, end);
                };

                // Sort the entire array.
                recursiveSort(0, unsortedArray.length - 1);
                resultsArray.push(sortedArray.slice(0));
                return sortedArray;
            };

            /* -- */

            let bubbleSort = (inputArr) => {
                resultsArray.push(inputArr.slice(0));
                let len = inputArr.length;
                let swapped;
                do {
                    swapped = false;
                    for (let i = 0; i < len; i++) {
                        if (inputArr[i] > inputArr[i + 1]) {
                            let tmp = inputArr[i];
                            inputArr[i] = inputArr[i + 1];
                            inputArr[i + 1] = tmp;
                            swapped = true;
                            resultsArray.push(inputArr.slice(0));
                        }
                        
                    }
                } while (swapped);
                resultsArray.push(inputArr.slice(0));
                return inputArr;
            };

            /* -- */

            function shellSort(arr) {
                resultsArray.push(arr.slice(0));
                var increment = arr.length / 2;
                while (increment > 0) {
                    for (i = increment; i < arr.length; i++) {
                        var j = i;
                        var temp = arr[i];
                
                        while (j >= increment && arr[j-increment] > temp) {
                            arr[j] = arr[j-increment];
                            j = j - increment;
                        }
                
                        arr[j] = temp;
                        resultsArray.push(arr.slice(0));
                    }
                
                    if (increment == 2) {
                        increment = 1;
                    } else {
                        increment = parseInt(increment*5 / 11);
                    }
                }
                resultsArray.push(arr.slice(0));
                return arr;
            }

            /* -- */
           
            sortingType = [insertionSort,selectionSort,mergeSort,quickSort,bubbleSort,shellSort];
            
            randType = Math.floor(Math.random()*sortingType.length);
            //console.log(randType);
            //console.log(""+(sortingNames[randType]));
            sortingType[randType](myArr);
            //console.log(resultsArray);

            //console.log(insertionSort(myArr));
        
            /*

                Visually show Insertion sort and selection sort

                Sources:

                Insertion Sort base code - https://medium.com/javascript-algorithms/javascript-algorithms-insertion-sort-59b6b655373c


            */
        
        </script>
    </body>
</html>
<form>
    <label>Your name:</label>
    <input id="user" name="username" type="text" placeholder="your name here" />
</form>
<!--your comment-->
<p>this is funny</p>
<img src="https://encrypted-tbn0.gstatic.com/images?q=tbn%3AANd9GcTdQkWK-B2Kj8erUDezVfQxhfqB5tTiRGe01sDwrij1bxpJ8lyF" height="50%" width="50%" alt="">
<p>i love apex legends the video game.</p>
<p>which main character is crypto.</p>
<img src="https://encrypted-tbn0.gstatic.com/images?q=tbn%3AANd9GcRJ7keFqO84KMqN7Wx0-brCBF_LKGbrf3vlJV9HYz6-v0phpRNH" height="80%" width="90%" border="10%" alt="">
<p>i have a instagram account</p>
<p>you can find me from this link bellow</p>
<a href="https://www.instagram.com/arentohere" terget="_blank"> instagram</a>
<p>you can find me on facebook also by <a href="https://www.facebook.com/arefin.ani.5" terget="_blank">click here</a></p>
<p>you can call me a </p>
<ol>
<li>gamer</li>
<li>youtuber</li>
<li>live streamer</li>
<li>extraordinary</li>
</ol>
<p>lets do it again</p>
<p>i am a</p>
<ul>
<li>gamer</li>
<li>streamer</li>
<li>youtuber</li>
<li>extraordinary</li>
</ul>
<p>do you find any marks change.</p>
<p>i changed the number pattern in full stop like point</p>
<p>😛😜</p>
<p>lets do it in another pattern</p>
<table border="1" >
<tr>
<td bgcolor="green">programer</td>
<td bgcolor="red">gamer</td>
</tr>
<tr>
<td>haha</td>
<td>haha</td>
</tr>
</table>
<h1><span>this is just a test of my coding</span></h1>
<table>
<tr>
<th>la</th>
<th>la</th>
<th>la</th>
</tr>
</table>

<!DOCTYPE html>
<html>
<head>
<meta keywords="html,learn,teach" />
<link rel="stylesheet" type="text/css" href="style.css">
<title>HTML</title>
</head>
<body background="tech1.jpg" color=blue>
<!--headings-->
<div>
<font color=" # ffffff "><h1 align="center" >welcome to Html</h1>
</div>
<!--paragraph-->
<p align="center">the page web is free for all country</p>
<h2 align="center">sign in</h2></font>
<!--forms-->
<form align="center" >
<div>
<label></label>
<input type="text" name="frist-name" placeholder="Frist Name" size="13%">
<label></label>
<input type="text" name="last-name" placeholder="Last Name" size="13%">
</div>
<br>
<div>
<label></label>
<input type="email" name="email" placeholder="Email Address :" size="31%">
</div>
<br>
<div>
<label></label>
<input type="password" name="password" placeholder="password" size="13%">
<label></label>
<input type="password" name="password" placeholder="cofirm password" size="13%">
</div>
<br>
<div>
<label></label>
<input type="number" name="Age" value="30" size="13%">
</div>
<br>
<div>
<label></label>
<input type="date" name="birthay" value="30">
</div>
<br>
<div align="center">
<label></label>
<select name="Gender">
<option value="male">male</option>
<option value="female">female</option>
<option value="other">other</option>
</select>
</div>
<br>
<div>
<label></label>
<textarea name="Message" placeholder="Me
ssage"></textarea>
</div>
<br>
<div>
<input type="submit" name="submit" value="Submit">
</div>
</form>
</body>
</html>
<p>lets play this music</p>
<audio controls><source src="audio.mp3" type="audio/mpeg"><source src="audio.ogg" type="audio.ogg">
    Audio element not supported by your browser
</audio>
<p> now the test of play a video</p>
<p>video is</p>
loading: <progress min="0" max="100" value="45"> 
</progress>
<video controls>
   <source src="ame.mp4" type="video/mp4">
   <source src="ame.mp4" type="video/ogg">
   Video is not supported by your browser
</video>
<p>this is a sideshow</p>
<svg width="1000" height="250">
    <rect width="150" height="150" fill="blue">
        <animate attributeName="x" from="0" to="300"
      dur="5s" fill="freeze" repeatCount="2"/> 
    </rect>
<form>
    <label>Your name:</label>
    <input id="user" name="username" type="text" />
</form>
</body>
</html>
<!DOCTYPE html>
<html>
    <head>
        <title>Shaheed Minar Of Bangladesh</title>
    </head>
    <body>
   
       <center><svg>
 
            <!-- Ground-->
        
            <path d = "M 5 300 345 300"  stroke = "green" fill="none"><animate attributeName="stroke" from="blue" to="darkred" dur="10s" fill="none" repeatCount="indefinite" /></path>
            <path d = "M 5 290 345 290" stroke = "green"  fill="none"><animate attributeName="stroke" from="blue" to="darkred" dur="10s" fill="none" repeatCount="indefinite" /></path>
          <path d= "M 5 300 5 290" stroke="green" fill ="none">
          <animate attributeName="stroke" from="blue" to="darkred" dur="10s" fill="none" repeatCount="indefinite" /></path>
          <path d= "M 345 300 345 290" stroke="green" fill ="none"><animate attributeName="stroke" from="blue" to="darkred" dur="10s" fill="none" repeatCount="indefinite" /></path>
            <!-- First Piller-->
          <path d= "M 10 290 10 220 L 50 220 L 50 290" stroke="green" fill ="none"><animate attributeName="stroke" from="green" to="red" dur="10s" fill="none" repeatCount="indefinite" /></path> 
         <path d= "M 20 290 20 230 L 40 230 L 40 290" stroke="green" fill ="none"><animate attributeName="stroke" from="green" to="red" dur="10s" fill="none" repeatCount="indefinite" /></path>
         <!-- Second Piller-->
         <path d= "M 70 290 70 200 L 120 200 L 120 290" stroke="green" fill ="none"><animate attributeName="stroke" from="green" to="red" dur="10s" fill="none" repeatCount="indefinite" /></path> 
         <path d= "M 80 290 80 210 L 110 210 L 110 290" stroke="green" fill ="none"><animate attributeName="stroke" from="green" to="red" dur="10s" fill="none" repeatCount="indefinite" /></path>
         <!-- Fourth Piller-->
         <path d= "M 340 290 340 220 L 300 220 L 300 290" stroke="green" fill ="none"><animate attributeName="stroke" from="green" to="red" dur="10s" fill="none" repeatCount="indefinite" /></path> 
         <path d= "M 330 290 330 230 L 310 230 L 310 290" stroke="green" fill ="none"><animate attributeName="stroke" from="green" to="red" dur="10s" fill="none" repeatCount="indefinite" /></path>
         <!-- Third Piller-->
         <path d= "M 280 290 280 200 L 230 200 L 230 290" stroke="green" fill ="none"><animate attributeName="stroke" from="green" to="red" dur="10s" fill="none" repeatCount="indefinite" /></path> 
         <path d= "M 270 290 270 210 L 240 210 L 240 290" stroke="green" fill ="none"><animate attributeName="stroke" from="green" to="red" dur="10s" fill="none" repeatCount="indefinite" /></path>
         <!-- Middle Piller-->
         <path d= "M 140 170 130 110 L 200 110 L 210 170" stroke="green" fill ="none"><animate attributeName="stroke" from="green" to="red" dur="10s" fill="none" repeatCount="indefinite" /></path> 
         <path d= "M 150 170 142 120 L 190 120 L 200 170" stroke="green" fill ="none"><animate attributeName="stroke" from="green" to="red" dur="10s" fill="none" repeatCount="indefinite" /></path>
         <!-- 1st -->
         <path d= "M 140 290 140 170" stroke="green" fill ="none"><animate attributeName="stroke" from="green" to="red" dur="10s" fill="none" repeatCount="indefinite" /></path>
          <path d= "M 150 290 150 170" stroke="green" fill ="none"><animate attributeName="stroke" from="green" to="red" dur="10s" fill="none" repeatCount="indefinite" /></path>
          <!-- 2nd -->
          <path d= "M 170 290 170 170" stroke="green" fill ="none"><animate attributeName="stroke" from="green" to="red" dur="10s" fill="none" repeatCount="indefinite" /></path>
          <path d= "M 180 290 180 170" stroke="green" fill ="none"><animate attributeName="stroke" from="green" to="red" dur="10s" fill="none" repeatCount="indefinite" /></path>
          <path d= "M 170 170 160 120" stroke="green" fill ="none"><animate attributeName="stroke" from="green" to="red" dur="10s" fill="none" repeatCount="indefinite" /></path>
          <path d= "M 180 170 170 120" stroke="green" fill ="none"><animate attributeName="stroke" from="green" to="red" dur="10s" fill="none" repeatCount="indefinite" /></path>
          <!-- 3rd -->
          <path d= "M 200 290 200 170" stroke="green" fill ="none"><animate attributeName="stroke" from="green" to="red" dur="10s" fill="none" repeatCount="indefinite" /></path>
          <path d= "M 210 290 210 170" stroke="green" fill ="none"><animate attributeName="stroke" from="green" to="red" dur="10s" fill="none" repeatCount="indefinite" /></path>
         <!-- Circle-->
         <circle cx="175" cy="230" r="37"
         stroke="red" fill="none">
         <animate attributeName="stroke" from="red" to="green" dur="10s" fill="none" repeatCount="indefinite" /></circle>
         <circle cx="175" cy="230" r="27"
         stroke="red" fill="none">
         <animate attributeName="stroke" from="red" to="green" dur="10s" fill="none" repeatCount="indefinite" /></circle>
            <!--Text-->
  <g > 
    <text id="TextElement" x="0" y="0" style="font-family:serif;font-size:40px; visibility:hidden"> Shaheed Minar
      <set attributeName="visibility" attributeType="CSS" to="visible" begin="1s" dur="5s" fill="freeze" />
      <animateMotion path="M 0 340 L 40 345" begin="1s" dur="1s" fill="freeze" />
      <animate attributeName="fill" attributeType="CSS" from="red" to="lightblue" begin="1s" dur="5s" fill="freeze" /> 
    </text> 
<!--
  </g> 
    <g > 
-->
    <text id="TextElement" x="0" y="0" style="font-family:serif;font-size:20px; visibility:hidden">   অ 
      <set attributeName="visibility" attributeType="CSS" to="visible" begin="1s" dur="5s" fill="freeze" />
      <animateMotion path="M 200 0 L 200 300" begin="1s" dur="5s" fill="none" repeatCount="indefinite" />
      <animate attributeName="fill" attributeType="CSS" from="red" to="lightblue" begin="1s" dur="2s" fill="freeze" /> 
    </text> 
      
    <text id="TextElement" x="0" y="0" style="font-family:serif;font-size:20px; visibility:hidden">   আ
      <set attributeName="visibility" attributeType="CSS" to="visible" begin="1s" dur="5s" fill="freeze" />
      <animateMotion path="M 10 0 L 10 300" begin="1s" dur="3s" fill="none" repeatCount="indefinite" />
      <animate attributeName="fill" attributeType="CSS" from="red" to="lightblue" begin="1s" dur="2s" fill="freeze" /> 
    </text> 
      
          <text id="TextElement" x="0" y="0" style="font-family:serif;font-size:20px; visibility:hidden">   ই
      <set attributeName="visibility" attributeType="CSS" to="visible" begin="1s" dur="5s" fill="freeze" />
      <animateMotion path="M 60 0 L 60 300" begin="1s" dur="5.6s" fill="none" repeatCount="indefinite" />
      <animate attributeName="fill" attributeType="CSS" from="red" to="lightblue" begin="1s" dur="2s" fill="freeze" /> 
    </text> 
      
    <text id="TextElement" x="0" y="0" style="font-family:serif;font-size:20px; visibility:hidden">  ঈ 
      <set attributeName="visibility" attributeType="CSS" to="visible" begin="1s" dur="5s" fill="freeze" />
      <animateMotion path="M 110 0 L 110 300" begin="1s" dur="3.7s" fill="none" repeatCount="indefinite" />
      <animate attributeName="fill" attributeType="CSS" from="red" to="lightblue" begin="1s" dur="2s" fill="freeze" /> 
    </text>
      
          <text id="TextElement" x="0" y="0" style="font-family:serif;font-size:20px; visibility:hidden">   উ
      <set attributeName="visibility" attributeType="CSS" to="visible" begin="1s" dur="5s" fill="freeze" />
      <animateMotion path="M 50 0 L 50 300" begin="1s" dur="4.2s" fill="none" repeatCount="indefinite" />
      <animate attributeName="fill" attributeType="CSS" from="red" to="lightblue" begin="1s" dur="2s" fill="freeze" /> 
    </text> 
      
    <text id="TextElement" x="0" y="0" style="font-family:serif;font-size:20px; visibility:hidden">   ঊ
      <set attributeName="visibility" attributeType="CSS" to="visible" begin="1s" dur="5s" fill="freeze" />
      <animateMotion path="M 100 0 L 100 300" begin="1s" dur="2s" fill="none" repeatCount="indefinite" />
      <animate attributeName="fill" attributeType="CSS" from="red" to="lightblue" begin="1s" dur="2s" fill="freeze" /> 
    </text>
      
    <text id="TextElement" x="0" y="0" style="font-family:serif;font-size:20px; visibility:hidden">   ঋ
      <set attributeName="visibility" attributeType="CSS" to="visible" begin="1s" dur="5s" fill="freeze" />
      <animateMotion path="M 150 0 L 150 300" begin="1s" dur="6s" fill="none" repeatCount="indefinite" />
      <animate attributeName="fill" attributeType="CSS" from="red" to="lightblue" begin="1s" dur="2s" fill="freeze" /> 
    </text> 
      
    <text id="TextElement" x="0" y="0" style="font-family:serif;font-size:20px; visibility:hidden">  ঌ
      <set attributeName="visibility" attributeType="CSS" to="visible" begin="1s" dur="5s" fill="freeze" />
      <animateMotion path="M 300 0 L 300 300" begin="1s" dur="3.7s" fill="none" repeatCount="indefinite" />
      <animate attributeName="fill" attributeType="CSS" from="red" to="lightblue" begin="1s" dur="2s" fill="freeze" /> 
    </text>
      
          <text id="TextElement" x="0" y="0" style="font-family:serif;font-size:20px; visibility:hidden">   এ
      <set attributeName="visibility" attributeType="CSS" to="visible" begin="1s" dur="5s" fill="freeze" />
      <animateMotion path="M 30 0 L 30 300" begin="1s" dur="5.5s" fill="none" repeatCount="indefinite" />
      <animate attributeName="fill" attributeType="CSS" from="red" to="lightblue" begin="1s" dur="2s" fill="freeze" /> 
    </text> 
      
    <text id="TextElement" x="0" y="0" style="font-family:serif;font-size:20px; visibility:hidden">   ঐ
      <set attributeName="visibility" attributeType="CSS" to="visible" begin="1s" dur="5s" fill="freeze" />
      <animateMotion path="M 70 0 L 70 300" begin="1s" dur="3.5s" fill="none" repeatCount="indefinite" />
      <animate attributeName="fill" attributeType="CSS" from="red" to="lightblue" begin="1s" dur="2s" fill="freeze" /> 
    </text>
      
          <text id="TextElement" x="0" y="0" style="font-family:serif;font-size:20px; visibility:hidden">   ও
      <set attributeName="visibility" attributeType="CSS" to="visible" begin="1s" dur="5s" fill="freeze" />
      <animateMotion path="M 130 0 L 130 300" begin="1s" dur="2.5s" fill="none" repeatCount="indefinite" />
      <animate attributeName="fill" attributeType="CSS" from="red" to="lightblue" begin="1s" dur="2s" fill="freeze" /> 
    </text> 
      
    <text id="TextElement" x="0" y="0" style="font-family:serif;font-size:20px; visibility:hidden">   ঔ
      <set attributeName="visibility" attributeType="CSS" to="visible" begin="1s" dur="5s" fill="freeze" />
      <animateMotion path="M 170 0 L 170 300" begin="1s" dur="4.5s" fill="none" repeatCount="indefinite" />
      <animate attributeName="fill" attributeType="CSS" from="red" to="lightblue" begin="1s" dur="2s" fill="freeze" /> 
    </text>
      
      <text id="TextElement" x="0" y="0" style="font-family:serif;font-size:20px; visibility:hidden">   ক
      <set attributeName="visibility" attributeType="CSS" to="visible" begin="1s" dur="5s" fill="freeze" />
      <animateMotion path="M 120 0 L 120 300" begin="1s" dur="5.2s" fill="none" repeatCount="indefinite" />
      <animate attributeName="fill" attributeType="CSS" from="red" to="lightblue" begin="1s" dur="2s" fill="freeze" /> 
    </text> 
      
    <text id="TextElement" x="0" y="0" style="font-family:serif;font-size:20px; visibility:hidden">   খ
      <set attributeName="visibility" attributeType="CSS" to="visible" begin="1s" dur="5s" fill="freeze" />
      <animateMotion path="M 220 0 L 220 300" begin="1s" dur="3.8s" fill="none" repeatCount="indefinite" />
      <animate attributeName="fill" attributeType="CSS" from="red" to="lightblue" begin="1s" dur="2s" fill="freeze" /> 
    </text> 
      
          <text id="TextElement" x="0" y="0" style="font-family:serif;font-size:20px; visibility:hidden">   গ
      <set attributeName="visibility" attributeType="CSS" to="visible" begin="1s" dur="5s" fill="freeze" />
      <animateMotion path="M 260 0 L 260 300" begin="1s" dur="5s" fill="none" repeatCount="indefinite" />
      <animate attributeName="fill" attributeType="CSS" from="red" to="lightblue" begin="1s" dur="2s" fill="freeze" /> 
    </text> 
      
    <text id="TextElement" x="0" y="0" style="font-family:serif;font-size:20px; visibility:hidden">   ঘ
      <set attributeName="visibility" attributeType="CSS" to="visible" begin="1s" dur="5s" fill="freeze" />
      <animateMotion path="M 175 0 L 175 300" begin="1s" dur="4.2s" fill="none" repeatCount="indefinite" />
      <animate attributeName="fill" attributeType="CSS" from="red" to="lightblue" begin="1s" dur="2s" fill="freeze" /> 
    </text>
      
          <text id="TextElement" x="0" y="0" style="font-family:serif;font-size:20px; visibility:hidden">   ঙ
      <set attributeName="visibility" attributeType="CSS" to="visible" begin="1s" dur="5s" fill="freeze" />
      <animateMotion path="M 50 0 L 50 300" begin="1s" dur="4.6s" fill="none" repeatCount="indefinite" />
      <animate attributeName="fill" attributeType="CSS" from="red" to="lightblue" begin="1s" dur="2s" fill="freeze" /> 
    </text> 
      
    <text id="TextElement" x="0" y="0" style="font-family:serif;font-size:20px; visibility:hidden">   চ
      <set attributeName="visibility" attributeType="CSS" to="visible" begin="1s" dur="5s" fill="freeze" />
      <animateMotion path="M 100 0 L 100 300" begin="1s" dur="2.4s" fill="none" repeatCount="indefinite" />
      <animate attributeName="fill" attributeType="CSS" from="red" to="lightblue" begin="1s" dur="2s" fill="freeze" /> 
    </text>
      
    <text id="TextElement" x="0" y="0" style="font-family:serif;font-size:20px; visibility:hidden">   ছ
      <set attributeName="visibility" attributeType="CSS" to="visible" begin="1s" dur="5s" fill="freeze" />
      <animateMotion path="M 280 0 L 280 300" begin="1s" dur="2.4s" fill="none" repeatCount="indefinite" />
      <animate attributeName="fill" attributeType="CSS" from="red" to="lightblue" begin="1s" dur="2s" fill="freeze" /> 
    </text> 
      
    <text id="TextElement" x="0" y="0" style="font-family:serif;font-size:20px; visibility:hidden">  জ
      <set attributeName="visibility" attributeType="CSS" to="visible" begin="1s" dur="5s" fill="freeze" />
      <animateMotion path="M 190 0 L 190 300" begin="1s" dur="2.7s" fill="none" repeatCount="indefinite" />
      <animate attributeName="fill" attributeType="CSS" from="red" to="lightblue" begin="1s" dur="2s" fill="freeze" /> 
    </text>
      
          <text id="TextElement" x="0" y="0" style="font-family:serif;font-size:20px; visibility:hidden">   ঝ
      <set attributeName="visibility" attributeType="CSS" to="visible" begin="1s" dur="5s" fill="freeze" />
      <animateMotion path="M 90 0 L 90 300" begin="1s" dur="5.5s" fill="none" repeatCount="indefinite" />
      <animate attributeName="fill" attributeType="CSS" from="red" to="lightblue" begin="1s" dur="2s" fill="freeze" /> 
    </text> 
      
    <text id="TextElement" x="0" y="0" style="font-family:serif;font-size:20px; visibility:hidden">   ঞ
      <set attributeName="visibility" attributeType="CSS" to="visible" begin="1s" dur="5s" fill="freeze" />
      <animateMotion path="M 320 0 L 320 300" begin="1s" dur="5.4s" fill="none" repeatCount="indefinite" />
      <animate attributeName="fill" attributeType="CSS" from="red" to="lightblue" begin="1s" dur="2s" fill="freeze" /> 
    </text>
      
          <text id="TextElement" x="0" y="0" style="font-family:serif;font-size:20px; visibility:hidden">   ট
      <set attributeName="visibility" attributeType="CSS" to="visible" begin="1s" dur="5s" fill="freeze" />
      <animateMotion path="M 270 0 L 270 300" begin="1s" dur="3.8s" fill="none" repeatCount="indefinite" />
      <animate attributeName="fill" attributeType="CSS" from="red" to="lightblue" begin="1s" dur="2s" fill="freeze" /> 
    </text> 
      
    <text id="TextElement" x="0" y="0" style="font-family:serif;font-size:20px; visibility:hidden">   ঠ
      <set attributeName="visibility" attributeType="CSS" to="visible" begin="1s" dur="5s" fill="freeze" />
      <animateMotion path="M 230 0 L 230 300" begin="1s" dur="4.2s" fill="none" repeatCount="indefinite" />
      <animate attributeName="fill" attributeType="CSS" from="red" to="lightblue" begin="1s" dur="2s" fill="freeze" /> 
    </text>


  </g> 
            
        </svg>
        <br>
        
        <div class = "t">
            <b>
        The Shaheed Minar is a national monument in Dhaka, Bangladesh, established to commemorate those killed during the Bengali Language Movement demonstrations of 1952 in then East Pakistan.
        </b><hr>
        <h3>International Mother Language Day</h3>
        <b>International Mother Language Day is celebrated every year on 21st February. The main purpose of celebrating this day is to promote the awareness of language and cultural diversity all across the world. It was first announced by UNESCO on November 17, 1999. Since then it is being celebrated every year. The date represents the day 21st February 1952 when four young students were killed in Dhaka, the capital of Bangladesh, because of Bengali and Urdu language controversy. Languages are the most powerful way to preserve and develop culture and to promote it all across the world. Because of this unfortunate incident, International Mother Language Day is celebrated in all over the world, while it is a public holiday in Bangladesh.</b>
        </div>
        </center> 
    </body>
</html>
<p>this is about corona virus</p>
<!DOCTYPE html>
<html>
    <head>
        <title>Page Title</title>
        <link href="https://fonts.googleapis.com/css?family=Dancing+Script|Squada+One&display=swap" rel="stylesheet">
    </head>
    <body>
        <center>
                <img src="https://imgcdn.cna.com.tw/Eng/WebEngPhotos/1024/2020/20200220/800x600_826865924885.jpg">
           
          <h2>  How Corona virus spread? </h2>
            <p>Current understanding about how the virus that causes coronavirus disease 2019 (COVID-19) spreads is largely based on what is known about similar coronaviruses.</p>

            <h2>Person-to-person spread</h2>
            <p>The virus is thought to spread mainly from person-to-person.

            Between people who are in close contact with one another (within about 6 feet)
            Via respiratory droplets produced when an infected person coughs or sneezes.
            These droplets can land in the mouths or noses of people who are nearby or possibly be inhaled into the lungs.
            Spread from contact with infected surfaces or objects
            It may be possible that a person can get COVID-19 by touching a surface or object that has the virus on it and thentouching their own mouth, nose, or possibly their eyes, but this is not thought to be the main way the virus spreads.</p>

            <h2>When does spread happen?</h2>
            <p>People are thought to be most contagious when they are most symptomatic (the sickest).
            Some spread might be possible before people show symptoms; there have been reports of this with this new coronavirus, but this is not thought to be the main way the virus spreads.
            How efficiently does the virus spread?
            How easily a virus spreads from person-to-person can vary. Some viruses are highly contagious (like measles), while other viruses are less so. Another factor is whether the spread continues over multiple generations of people (if spread is sustained). The virus that causes COVID-19 seems to be spreading easily and sustainably in Hubei province and other parts of China. In the United States, spread from person-to-person has occurred only among a few close contacts and has not spread any further to date.</p>
    </center>
    <footer>
        <br>
        <p><u><i>Source: Google search</i></u></p>
    </footer>
    </body>
</html>

<h1><span>contact me</span></h1>
<form>
<form autocomplete="off">
    <label for="name">name:   </label>
    <input type="text" name="name" placeholder="Arefin Ani" />
</form>
<form>
    <label for="email">e-mail: </label>
    <input type="text" name="email" placeholder="email@example.com"/>
</form><br/>
<textarea name="massage"></textarea>
<input type="submit" value="SEND" class="submit"/>
</form>
</body>
</html>
