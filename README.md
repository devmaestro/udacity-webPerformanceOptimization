### Getting started

Setting up the workspace on local:

1. Check out the repository
1. You can run a local server

  ```bash
  $> cd /path/to/your-project-folder
  $> python -m SimpleHTTPServer 8080
  ```

1. Open a browser and visit localhost:8080
1. To allow the localhost to be available over public web
1. Download and install [ngrok](https://ngrok.com/) to make your local server accessible remotely.

  ``` bash
  $> cd /path/to/your-project-folder
  $> ngrok 8080
  ```

1. Copy the public URL ngrok gives you and try running it through PageSpeed Insights! [More on integrating ngrok, Grunt and PageSpeed.](http://www.jamescryer.com/2014/06/12/grunt-pagespeed-and-ngrok-locally-testing/)

### Optimizations performed

##### Pagespeed Score in index.html

##### FPS on scroll in pizza.html
- Javascript document selectors are expensive operations since they search
  over the entire DOM to get the elements matching the specified criteria. Running
  such an operation EVERYTIME 'scroll' is triggered affects the page performance (eg. animation)
  and decreases the fps.
- In pizza.html, in main.js, everytime scroll event is triggered, updatePositions function is being called.
  updatePositions basically gets all elements in the document with class 'mover' (using a document selector)
  and populates the object 'items'. So, everytime scroll event is triggered, the document selector
  is called. Since the elements in the document don't change on scroll, there is no need to call the selector
  everytime. Rather, we can call the selector once and cache the results and the subsequent calls
  are just accessing the stored values, thereby increasing the frame performance while scrolling.

##### Pizza resize time in pizza.html
- In pizza.html, in main.js, everytime resize event is triggered on pizza, selectors are called
  - to change the label on the slidebar
  - to get the element with id 'randomPizzas'
  - to get the elements with class 'randomPizzaContainer'
  Similar to the fps optimization, caching the results removes the performance bottleneck.
  Performing these optimizations reduces the resize time from ~255ms to ~4ms
