### Intro

In order to provide advertisers with the ability to create dynamic content, we've enabled running HTML apps on Spoteer enabled screens.

#### Requirements:
- The app has to be compressed into one zip file.
- The zip file has to contain file named `index.html` in the zip's base folder. This will be the file that will be loaded first.
- Any other files that are required by the app has to exist in the zip folder in the same structure that they are required. 
For example:
If `index.html` contains an image `<img src="img/logo.png" />`, then the file `logo.png` has to be under the directory `img` in the zip fiolder
- Build the app with "offline-first" concepts. In order for your message to deliver itself 100% of the time, even when connection problems occur, follow these basic guidelines:
  - Include external libraries and assets in your package and refer to then instead of refering to them on the web
  - Load the data needed for the app asynchronously and cache it in local storage for fast fetching or even offline fetching.
  - Make the creative relvant even if the app failed to fetch the data it needs in order to handle both connectivity or data servers issues.
