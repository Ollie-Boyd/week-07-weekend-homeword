# Just-Eat Bikes availability map

>### Brief
>
>Your task is to create an application that makes a request to an API and displays the data.
>
>Suggested APIs:
>1. Studio Ghibli: https://ghibliapi.herokuapp.com/
>2. Reddit: (Append `.json` to any Reddit URL - for example https://www.reddit.com/r/javascript.json)
>3. Guardian search: https://content.guardianapis.com/search?q=brexit&format=json&api-key=test

>#### MVP
>- The application should display data from an API request.
>- The application should have a clear separation of concerns (multiple components)
>- Take input from the user to update the page. You could update the page by filtering or manipulating the data on user interaction, or you might make further API requests to load more data that is then displayed.

## Planning
* I knew that I wanted to try my hand at mapping so I looked at the official [Vue2Leaflet](https://github.com/vue-leaflet/Vue2Leaflet) library that Leaflet.js have made to support Vue. There was not a huge amount of documentation compared with their native implementation of Vue and there were the warning signs of a number of StackOverflow questions and not so many answers, but I thought Vue2Leaflet might be better than Leaflet.js as it was built for Vue. 
* I found the Just-Eat rental bikes' API for my city and decided to make a little web-app that let a user see which docks had bikes and which didn't.
* When the user clicks on the dock, a popup would display the available bikes and empty docks. 
* The Just Eat bikes Edinburgh [realtime data API](https://edinburghcyclehire.com/open-data/realtime) has two endpoints that I would need to use. Their "Stations" endpoint with station lat/long coords and their "Availability" endpoint with availability data on bikes and docks. I knew I would need to query both of these endpoints and somehow merge the responses into one object. 
* I wanted the data displayed on the screen to be somewhat realtime, and I needed to figure out how to refresh the data the user saw every few minutes. Enough so the user could rely on the results' accuracy but not so much that the API was hammered with requests. 

## What I learned

## What I could improve on
* Response caching



## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
