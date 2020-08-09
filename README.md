# Just-Eat Bikes availability map

### Screenshots of the finished project
<p align="center">
  <img src="https://raw.githubusercontent.com/Ollie-Boyd/JustEat-bikes-mapping-with-Leaflet.js-and-Vue.js/master/screenshots/just-eat.png" width=80% height=auto%>
</p>

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
* To make multiple API calls I needed to use multiple promises. Initially I used nested promises which was horribly unreadable but then I read about [Promise.all](https://gomakethings.com/waiting-for-multiple-all-api-responses-to-complete-with-the-vanilla-js-promise.all-method/) and that let me make a nice refactor. 
* To merge the data from the two requests I found [Object.merge](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/assign) which is such a pleasingly clean way to make the merge! 
* To refresh the data I used setTimeout to create a 1 minute delay then used recursion so the fetchStationAvailability would call itself after the delay. I couldn't find any arguments on the internet against using this solution so I hope it's OK. 
* Vue2Leaflet had a few bugs and the support and docs weren't great. For example [this](https://stackoverflow.com/questions/50864855/vue-js-leaflet-marker-is-not-visible) bug was a real pain and the official docs still referenced the broken way of making markers. It was my first experience not using the 'normal' version of an open-source project. Reading the community guidance on how to accomplish something in the normal Leaflet.js version and translating that into the Vue version was tricky. 
## What I could improve on
* Response caching - My app would be really harsh to the Just Eat server if there were multiple users. I would need to make a proxy server that would cache the Just Eat results and only make new API requests once it received user requests and its cached copy had expired. 
* I wouldn't use Vue2Leaflet again. I just can't quite understand the benefit of it over using Leaflet.js in Vue. Vue2Leaflet is a bit buggy and I think there would be more crossover benefit to other projects in learning normal Leaflet. 


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
