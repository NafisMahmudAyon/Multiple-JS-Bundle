# How to Bundle Multiple JavaScript Files into a Single File

You can bundle multiple JavaScript files like `file1.js`, `file2.js`, etc., into a single file using a module bundler like Webpack. Below is a step-by-step guide to bundling these files:

## 1. Organize Your Project Structure

Make sure your project is structured in a way that makes it easy to work with multiple files. For example:

```
project/
│ 
├── src/ 
│ 
├── index.js // Entry point 
│ 
├── file1.js // First script 
│ 
├── file2.js // Second script 
│ 
├── file3.js // Third script 
│ └── webpack.config.js // Webpack configuration file
```

## 2. Ensure Your JavaScript Files Are Exporting Functions

If your JavaScript files contain logic that needs to be reused or invoked, modify them to export functions or objects. For example:

```js
/// file1.js
export function setupFile1() {
	// Your existing code here...
	document.addEventListener("DOMContentLoaded", function () {
		// Your code...
	});
}
```

```js
/// file2.js
export function setupFile2() {
	// Your existing code here...
	document.addEventListener("DOMContentLoaded", function () {
		// Your code...
	});
}
```
## 3. Create an Entry Point

```js
import { setupFile1 } from './file1';
import { setupFile2 } from './file2';

setupFile1();
setupFile2();
```

## 4. Set Up Webpack Configuration

Create a `webpack.config.js` file in your project root:

```js
const path = require('path');

module.exports = {
  entry: './src/index.js', // Entry point for the bundle
  output: {
    filename: 'bundle.js', // Output bundled file
    path: path.resolve(__dirname, 'dist'), // Output directory
  },
  module: {
    rules: [
      {
        test: /\.js$/, // Process all .js files
        exclude: /node_modules/, // Exclude node_modules
        use: {
          loader: 'babel-loader', // Transpile modern JavaScript
          options: {
            presets: ['@babel/preset-env'], // Compile ES6+
          },
        },
      },
    ],
  },
  mode: 'production', // or 'development' depending on your environment
};
```

## 5. Install Dependencies

If you haven't installed Webpack and Babel yet, you can do so by running:

```bash
npm install --save-dev webpack webpack-cli babel-loader @babel/core @babel/preset-env
```

## 6. Bundle Your Files

Now, run Webpack to bundle your files into a single output:

```bash
npx webpack
```

This command will generate a bundle.js file in the dist directory.

## 7. Include the Bundled File in Your HTML

Finally, include the generated bundle.js in your HTML file:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Bundled JavaScript</title>
</head>
<body>
    <!-- Other HTML content -->

    <!-- Include the bundled JavaScript -->
    <script src="./dist/bundle.js"></script>
</body>
</html>
```

Now, all your JavaScript files are bundled into a single file, making it easy to manage and include in your projects.