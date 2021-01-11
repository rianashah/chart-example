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

### ![#c5f015](https://placehold.it/15/c5f015/000000?text=+) Example - Task 1: Splitting out HTML, CSS, and JavaScript
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
