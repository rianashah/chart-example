# Chart Example

In your home directory, make a folder called `Development`, if it doesn't exist. This is where we will keep all of the code for the class. Next, make sure that you are inside that folder, by checking the output of the following command:

```shell
pwd
```

If `pwd` shows that you are in a different directory, run `cd ~/Development` and check with `pwd` again.

## How to clone this repo

Next, clone this repository by clicking the green button in the upper right corner, selecting `SSH` and copying the string that looks like `git@github.com:code4policy/<REPO-NAME>.git` (`<REPO-NAME>` will be the name of your repository). Then, in the terminal run the following:

```
git clone git@github.com:code4policy/<REPO-NAME>.git
```

Note that by default, git will clone the repository into a folder with name `<REPO-NAME>`. After the repo is cloned, open that directory (use `cd`).

## Run a local server

D3.js charts won't work unless you're running a web server. This can be done locally with:

```
python3 -m http.server
```

Once you run this, you can open up the website by typing `http://localhost:8000/` into the browser. You'll need to open up a new tab in the terminal to continue your work. Make sure to `cd` back into this project folder and then open up the project in sublime text with `subl .`

# Tasks 

Now we're ready to start editing the code! 

### ![#c5f015](https://placehold.it/15/c5f015/000000?text=+) Example - Part 1: Splitting out HTML, CSS, and JavaScript
The problem with the code currently in this repository is that the HTML is ill-formed (there is no head and body). Also the CSS and the JavaScript is all in the same file as the HTML. Messy! I will demand that you always keep them separated for this class. Lets go ahead and do that.


Remember, a good HTML document has a head and body.

```html
<!DOCTYPE html>
<html>

<head>
  <title> Example Site </title>
</head>

<body>
</body>

</html>
```

You can link a separate CSS file with the following code. Remember, linking CSS always happens in the **\<head> \</head>** of the document.

```html
<link href="styles/style.css" rel="stylesheet" type="text/css">
```

You can call a JavaScript file like with this code. In this case we're linking one peice of code (the D3 library itself) from a website, and another peice of code (our specific chart) form a local file. Javascript is customarily placed at the end of the **\<body> \</body>** of the document. It is usually the last line before you close the body tag.

```html
<script src="//d3js.org/d3.v3.min.js"></script>
<script src="scripts/chart.js"></script>
```

Tasks:

1. Your task is to extract the parts of `example-chart.html` and move them into three separate files. Grab the styles and move them into `styles/style.css`. Grab the javascript and move it into `scripts/chart.js`. Finally, grab the valid HTML and move it into `index.html`. Now your directory structure should look something like this:
	
	```
	.
	├── data.tsv
	├── example-chart.html
	├── index.html
	├── scripts
	│   └── main.js
	└── styles
	    └── style.css
   ```


2. The next step is to link the CSS and Javascript to `index.html`. Your `index.html` might look something like this now:

	```html
	<!DOCTYPE html>
	<html>
	
	<head>
		<title> Example Site </title>
		
		<!--Link to StyleSheets in the head-->
		<link href="styles/style.css" rel="stylesheet" type="text/css">
	</head>
	
	<body>
		<h1> Apple: The Profitable Fruit </h1>
	
		<p> If you bought apple stock a long time ago you're probably rich. That's because it went up really fast! See for yourself in the chart below. </p>
	
		<h2> Apple Stocks are Really Rising! </h2>
		<h3> ...more than any other fruit-based corporation. </h3>
	
		<!-- Run JavaScript scripts in the body -->
		<script src="//d3js.org/d3.v3.min.js"></script>
		<script src="scripts/main.js"></script>
	</body>
	
	</html>
	```
3. Commit and push to GitHub

### ![#c5f015](https://placehold.it/15/c5f015/000000?text=+) Example - Part 2: Avoiding Conflicting CSS


Right now the chart works fine, however, that is because the chart is the only thing on the page. The CSS in these example D3 examples often assume the D3 is the only thing on the page. So if there were other things on the page, the CSS might also end up applying to those things as well! To avoid that, we must specify that the CSS only apply to the chart. Lets modify the CSS selectors to do just that.

### Using `id` and `class` tags Properly

If you look closely at `index.html`, you'll notice that there is no element in the HTML code for the chart. That's because the chart is being generated by the JavaScript file. After the HTML is initially loaded, the JavaScript code runs and creates an `<svg></svg>` element on the page containing the chart. (SVG stands for "Scalable Vector Graphic"). You can see that by right clicking on the chart and hitting "inspect" as shown below:

![](../assets/stockchart.png)

So lets suppose we wanted to add an `id` and a `class` attribute to that SVG tag. How would we do that without knowing JavaScript? Lets look at the code and try to deduce how.

You'll notice the SVG element in the image above contains a `width` and a `height`. We can first figure out how those came to be and then use the same mechanism to write additional attributes like `class` or `id`.

If you look inside the JavaScript file that generates the chart, and try to read it, you'll find the following:

```javascript
var svg = d3.select("body").append("svg")
    .attr("width", width + margin.left + margin.right)
    .attr("height", height + margin.top + margin.bottom)
```

Notice how that code is adding a width and a height attribute? We can add an id attribute in the same way.

```javascript
var svg = d3.select("body").append("svg")
    .attr("width", width + margin.left + margin.right)
    .attr("height", height + margin.top + margin.bottom)
    .attr("class", "chart")
    .attr("id", "apple-stock-chart")
```

This change will change the SVG to include a `class` and an `id`

![](../assets/stockchartidclass.png)

Finally, we can modify the CSS to **only** match this chart by adding a new id selector (`#apple-stock-chart`) to each style so that the style doesn't spill over and start to conflict with other charts. Your CSS may ultimately look like this:

```css
body {
  font: 10px sans-serif;
}

#apple-stock-chart .axis path,
#apple-stock-chart .axis line {
  fill: none;
  stroke: #000;
  shape-rendering: crispEdges;
}

#apple-stock-chart .x.axis path {
  display: none;
}

#apple-stock-chart .line {
  fill: none;
  stroke: steelblue;
  stroke-width: 1.5px;
}

#apple-stock-chart .overlay {
  fill: none;
  pointer-events: all;
}

#apple-stock-chart .focus circle {
  fill: none;
  stroke: steelblue;
}
```

Tasks:

1. Modify the JavaScript code for the chart so that it appends a `class=chart` and `id=apple-stock-chart` when it generates the chart.
2. Modify the CSS so that it applies only to the `apple-stock-chart` and doesn't spill over to any other charts that may be on the page.
3. Commit and push to GitHub

