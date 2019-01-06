# tutorial-express-leaflet

Richard Wen <rwen@ryerson.ca>  
  
A tutorial for creating a leaflet webmap with express in Node.js

## Step 1. Install Software

1. Install [Node.js](https://nodejs.org/)
2. Install [express-generator](https://www.npmjs.com/package/express-generator) globally `-g` with [npm](https://docs.npmjs.com/cli/install)
3. Check that the `express` command works by using the `-h` help option

```
npm install -g express-generator
express -h
```

## Step 2. Create an Express Project

### 2.1 Open a Command Line Interface (CLI)

Open a [command line interface](https://en.wikipedia.org/wiki/Command-line_interface) or terminal:

![command_line](images/command_line.gif)

### 2.2 Generate a Project Folder with the express Command

Create an express project with the `express` command, replacing `<project_name>` with the name of your project:

* `<project_name>` should be a valid folder name with no spaces and starting with a letter

```
express <project_name> --no-view
```

### 2.3 Inspect the Project Folder Structure

A folder named `<project_name>` will be created with the following structure inside (note that the structure may change with `express --version` that is not 4.16.0):

![project_structure](images/project_structure.png)

* `app.js`: JavaScript file that contains code needed to create and run your express server or application
* `package.json`: [JSON](https://www.json.org/) structured [package file](https://docs.npmjs.com/files/package.json) holding all the dependencies and information about your project (can be modified with the [npm](https://docs.npmjs.com/cli/npm) command)
* `/bin`: folder containing executable code
	* `www`: executable file for starting the server
* `/public`: folder containing files served to the client side or front end
	* `index.html`: landing page served to the clients
	* `/images`: folder containing images to be served to clients
	* `/javascripts`: folder containing [JavaScript](https://www.w3schools.com/js/) code files to be served to clients
	* `/stylesheets`: folder containing [Cascading Style Sheets (CSS)](https://www.w3schools.com/css/) files to be served to clients
		* `style.css`: CSS file used to define how your web page elements will look
* `/routes`: folder containing JavaScript files for defining [routes](https://expressjs.com/en/guide/routing.html) that direct how the server responds to client requests (these files are often used in file `app.js`)
	* `index.js`: defines the response to client requests at `<address>/` depending on how it is used in file `app.js`
	* `users.js`: defines the response to client requests at `<address>/users` depending on how it is used in file `app.js`

## Step 3. Install Project Dependencies

### 3.1 Change directory

Move into the project folder, where `<project_name>` is the name of the folder you created in [Step 2.2](#step-22-generate-a-project-folder-with-the-express-command):

```
cd <project_name>
```

### 3.2 Install express Dependencies

Inside your `<project_name>` folder, install the dependencies with `npm`, where a folder called `/node_modules` will contain the code files of the installed dependencies:

```
npm install
```

### 3.3 Install leaflet as a Dependency

Install leaflet with `npm install` and save it as a dependency `--save` to `package.json`:

```
npm install --save leaflet
```

## Step 4. Creating a leaflet Map

### 4.1 Create leaflet JavaScript File

Create a file for the leaflet map by sending an empty line with `echo.` into `>` a file called `webmap.js`:

```
echo. > webmap.js
```

### 4.2 Add leaflet Code

Open `webmap.js` for editing and add the following JavaScript code:

```javascript
// Import the leaflet package
var L = require('leaflet');

// Creates a leaflet map binded to an html <div> with id "map"
// setView will set the initial map view to the location at coordinates
// 13 represents the initial zoom level
var map = L.map('map').setView([43.659752, -79.378161], 13);

// Adds the basemap tiles to your web map
// Additional providers are available at: https://leaflet-extras.github.io/leaflet-providers/preview/
L.tileLayer('https://{s}.basemaps.cartocdn.com/dark_nolabels/{z}/{x}/{y}{r}.png', {
	attribution: '&copy; <a href="http://www.openstreetmap.org/copyright">OpenStreetMap</a> &copy; <a href="https://carto.com/attributions">CARTO</a>',
	subdomains: 'abcd',
	maxZoom: 19
}).addTo(map);

// Adds a popup marker to the webmap for GGL address
L.marker([43.659752, -79.378161]).addTo(map)
	.bindPopup(
		'Monetary Times Building, MON 304<br>' +
		'341 Victoria Street<br>' + 
		'Toronto, Ontario, Canada<br>' +
		'M5B 2K3<br><br>' + 
		'Tel: 416-9795000 Ext. 5192')
	.openPopup();
```
