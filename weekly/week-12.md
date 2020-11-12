# Week-12 (11/10/20 & 11/12/20)

## Topics: React FSCs & React Class Components

### I. React FSCs & React Class Components

#### I-A. FSC (Functional Stateless Components) Overview
- https://reactjs.org/
- Can make single page apps where the content on the page can refresh without the page having to load\
- Unlike handlebars, the rendering is happening on the client-side (although React can also do server-side rendering)

#### I-B. About Demos
- start code at: https://github.com/IGM-RichMedia-at-RIT/React-FSCs
- done code at: https://github.com/IGM-RichMedia-at-RIT/React-FSCs-Done
- video for demo is here: https://www.youtube.com/watch?v=kAMb0sEp9js&feature=emb_logo
- **package.json** has multiple build scripts for each example
- look at **example1.handlebars** - it is importing the needed client-side libs for React
- **client folder** is where we'll write most of the the code
- Functional Stateless Component
- A functional component is a JavaScript *function* (not a surprise!) that returns [JSX ("JavaScript XML")](https://reactjs.org/docs/introducing-jsx.html)
- Very simple to setup and use, actually
- JSX is a syntax for creating your own HTML tags
 
#### I-C. Example 1 - a no parameter function

**client/example1.js**

```js
 // React components need to be capitalized
 // always need some "root" HTML that wraps all the other HTML
const HelloWorld = () => {
  return (
    <div>
      Hello World
    </div>
  );
};
```
 
- change file extensions to **.jsx**

```js
// ReactDOM is imported by the client (example1.handlebars)
// render out the JSX tag <HelloWorld />, and put it in the #app div
const init = () => {
  ReactDOM.render(<HelloWorld />, document.querySelector("#app"));
};

window.onload = init;
```

- run the build script - `npm run buildExample1`
- look at **hosted/exampleBundle1.js** to see the transpiled code
- `npm start` to see the results
- "View Source" in the browser
- "Inspect Elements" in the browser
- React is running on the client-side, and updating the UI dynamically


#### I-D. Example 2 - a FSC that takes an argument

**client/example2.jsx**

```js
// Note that React events (like `onChange` below) are camel-cased
const HelloUser = (props) => {
  return (
    <div>
      Hello {props.username}
      <p>Change Name:</p>
      <input type="text" value={props.username} onChange={handleNameChange} />
    </div>
  );
};

// re-render <HelloUser> every time the 
const handleNameChange = (e) => {
  ReactDOM.render(
    <HelloUser username={e.target.value} />,
    document.querySelector("#app")
  );
};

const init = () => {
  ReactDOM.render(
    <HelloUser username='Ace Coder' />,
    document.querySelector("#app")
  );
};

window.onload = init;
```

- `npm run buildExample2`
- look at **hosted/exampleBundle2.js** to see the transpiled code
- `npm start`
- http://localhost:3000/example2
- "View Source" in the browser
- "Inspect Elements" in the browser



#### I-E. Example 3 - a FSC that hits up the server for data

**client/example3.jsx**

```js
const SongContainer = (props) => {
  if(props.songs.length === 0){
    return (
      <div>
        <h3>No Songs Yet!</h3>
      </div>
    );
  }

  // return JSX for all the songs in the list
  const songList = props.songs.map((song) => {
    return (
      <div>
        <h2>{song.artist} - <i>{song.title}</i></h2>
      </div>
    );
  })

  return (
    <div>
      <h1>My favorite songs!</h1>
      {songList}
    </div>
  );
};

const init = () => {
  ReactDOM.render(
    <SongContainer songs={[]} />,
    document.querySelector("#app")
  );
};
```

- `npm run buildExample3`
- look at **hosted/exampleBundle3.js** to see the transpiled code
- `npm start`
- http://localhost:3000/example3

- now load some data
- head to **controllers/index.js**

```js
const getSongs = (req,res) => {
  res.json([
    {artist: "Bruce", title: "Born to Run"},
    {artist: "Unknown", title: "I'm a little Teapot"}
  ])
};
```

- export it, and then add a route for **/getSongs** to **router.js**
- test **getSongs** endpoint
- back in **example3.jsx** implement `loadSongsFromServer();`

```js
const loadSongsFromServer = () => {
  const xhr = new XMLHttpRequest();

  const setSongs = () => {
    const songResponse = JSON.parse(xhr.response);

    ReactDOM.render(
      <SongContainer songs={songResponse} />,
      document.querySelector("#app")
    );
  };

  xhr.onload = setSongs;
  xhr.open('GET', '/getSongs')
  xhr.send();
};
```
- and call it from `init()`

<hr>  

### II. React Class components 

- React Class components are in an older syntax, and they can contain *state* information about a Component
- (*BTW - React hooks are newer, and allow you to add *state* to a FSC - https://reactjs.org/docs/hooks-intro.html*)
- keep track of state
- these classes have their own `render()` method
- start code: https://github.com/IGM-RichMedia-at-RIT/React-Class-Components
- done code: https://github.com/IGM-RichMedia-at-RIT/React-Class-Components-Done
- video for demo is here: https://www.youtube.com/watch?v=EzgxSVN-AzI&feature=emb_logo


#### II-A. Example 1 - a no parameter function

```jsx
class HelloWorld extends React.Component{
  render(){
    return (
      <div>
        Hello World
      </div>
    );
  }
}

const init = () => {
  ReactDOM.render(<HelloWorld />, 
    document.querySelector("#app"));
};

window.onload = init;
```

- run the build script - `npm run buildExample1`
- look at **hosted/exampleBundle1.js** to see the transpiled code - a lot more than last time
- `npm start` to see the results
- "View Source" in the browser
- "Inspect Elements" in the browser



#### II-B. Example 2 - a Class Component that takes an argument

- this is done though the constructor
- now the component will hang onto the state
- https://reactjs.org/docs/faq-state.html#what-is-the-difference-between-state-and-props
- let's walk though this one together
- Reference:
  - https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_objects/Function/bind
  - https://medium.com/front-end-weekly/do-i-still-need-to-bind-react-functions-in-2019-6d0fe72f40d7


#### II-C. Example 3 - a Class Component that hits up the server for data

- the whole point of these frameworks is to offload work from the server
  - handlebars is a server-side technology that does all of the work - if even a small piece of information on a page changes - a stock price for example - the whole page needs to re-render
  - React is primarily a client-side technology
    - if part of a page changes, the client contacts the server to get the new info (like the stock price) and then updates the page by changing just part of it (ex. the innerHTML of the div that holds the stock price)
    - thus the server doesn't have to do as much work, and not as much bandwidth needs to be used because only small bits of information (like a stock price) are sent back and forth (as opposed to the whole page)
    

<hr>

### III. React Function components (with hooks)

- start code is the `create-react-app` script:
  - https://reactjs.org/docs/create-a-new-react-app.html#create-react-app
  - running version on Heroku: https://gif-finder-2201.herokuapp.com
  - https://www.fastcompany.com/90505929/the-real-reason-facebook-bought-giphy-for-400-million
  
- here's a XHR helper function that will save you a lot of typing:

```js
 // Helper function to fetch data from Giphy
  const fetchData = ()=>{
    const GIPHY_URL = "https://api.giphy.com/v1/gifs/search";
    const GIPHY_KEY = "dc6zaTOxFJmzC"; // public API key from here: https://github.com/Giphy/GiphyAPI
   
    term = encodeURIComponent(term.trim());
		if(term.length < 2) return;
    
    let url = `${GIPHY_URL}?api_key=${GIPHY_KEY}&q=${term}`;

    const xhr = new XMLHttpRequest();

    xhr.onerror = (e) => console.log("XHR error");

    xhr.onload = (e) => {
      const jsonString = e.target.response;
      const json = JSON.parse(jsonString);
    
     // TODO
    // update `results` array an the UI
     
    }; // end xhr.onload
    
    xhr.open("GET",url);
    xhr.send();
  };
```

<hr><hr>  

| <-- Previous Unit | Home | Next Unit -->
| --- | --- | --- 
| [**week-10.md**](week-10.md)  |  [**IGME-430 Home**](../README.md) | week-13.md
