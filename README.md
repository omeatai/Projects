# Projects

React Practice Projects

## Tutorial

---

### [1-REACT API TUTORIAL - E-SIDE](#)

+IMDB PROJECT:

<details>
  <summary>1. Create React App</summary>

```bash
npx create-react-app .
```

index.js:

```js
import React from "react";
import ReactDOM from "react-dom/client";
import App from "./App";

const root = ReactDOM.createRoot(document.getElementById("root"));
root.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
);
```

App.js:

```js
import "./App.css";

function App() {
  return (
    <div className="App">
      <h1>Hello</h1>
    </div>
  );
}

export default App;
```

</details>

<details>
  <summary>2. Fetch Online Movie Database </summary>

```js
const axios = require("axios");

const options = {
  method: "GET",
  url: "https://online-movie-database.p.rapidapi.com/auto-complete",
  params: { q: "game of thr" },
  headers: {
    "X-RapidAPI-Key": "7990c02530mshd",
    "X-RapidAPI-Host": "online-movie-database.p.rapidapi.com",
  },
};

axios
  .request(options)
  .then(function (response) {
    console.log(response.data);
  })
  .catch(function (error) {
    console.error(error);
  });
```

```js
const options = {
  method: "GET",
  headers: {
    "X-RapidAPI-Key": "7990c02530mshd",
    "X-RapidAPI-Host": "online-movie-database.p.rapidapi.com",
  },
};

fetch(
  "https://online-movie-database.p.rapidapi.com/auto-complete?q=game%20of%20thr",
  options
)
  .then((response) => response.json())
  .then((response) => console.log(response))
  .catch((err) => console.error(err));
```

App.js:

```js
import "./App.css";

function App() {
  const options = {
    method: "GET",
    headers: {
      "X-RapidAPI-Key": "7990c02530mshdf87db921c2401fp1f5e29jsn311b5da7e4a6",
      "X-RapidAPI-Host": "online-movie-database.p.rapidapi.com",
    },
  };

  fetch(
    "https://online-movie-database.p.rapidapi.com/auto-complete?q=game%20of%20thr",
    options
  )
    .then((response) => response.json())
    .then((response) => console.log(response))
    .catch((err) => console.error(err));

  return (
    <div className="App">
      <h1>Hello</h1>
    </div>
  );
}

export default App;
```

</details>

<details>
  <summary>3. Create Search Input and Button</summary>

App.js:

```js
import "./App.css";

function App() {
  const options = {
    method: "GET",
    headers: {
      "X-RapidAPI-Key": "7990c02530mshdf87db921c2401fp1f5e29jsn311b5da7e4a6",
      "X-RapidAPI-Host": "online-movie-database.p.rapidapi.com",
    },
  };

  fetch(
    "https://online-movie-database.p.rapidapi.com/auto-complete?q=game%20of%20thr",
    options
  )
    .then((response) => response.json())
    .then((response) => console.log(response))
    .catch((err) => console.error(err));

  return (
    <div className="App">
      <h1>Movie Search</h1>
      <form action="">
        <input type="text" />
        <button type="submit">Search</button>
      </form>
    </div>
  );
}

export default App;
```

</details>

<details>
  <summary>4. Create State for Search</summary>

App.js:

```js
import React, { useState } from "react";
import "./App.css";

function App() {
  const [endPoint, setEndPoint] = useState("");

  const options = {
    method: "GET",
    headers: {
      "X-RapidAPI-Key": "7990c02530mshdf87db921c2401fp1f5e29jsn311b5da7e4a6",
      "X-RapidAPI-Host": "online-movie-database.p.rapidapi.com",
    },
  };

  // fetch('https://online-movie-database.p.rapidapi.com/auto-complete?q=game%20of%20thr', options)
  //   .then(response => response.json())
  //   .then(response => console.log(response))
  //   .catch(err => console.error(err));

  const onChangeHandler = (e) => {
    setEndPoint(e.target.value);
  };

  return (
    <div className="App">
      <h1>Movie Search</h1>
      <h2>{endPoint}</h2>
      <form action="">
        <input type="text" onChange={onChangeHandler} value={endPoint} />
        <button type="submit">Search</button>
      </form>
    </div>
  );
}

export default App;
```

</details>

<details>
  <summary>5. sample</summary>

```bs

```

```js

```

```js

```

</details>

<details>
  <summary>6. sample</summary>

```bs

```

```js

```

```js

```

</details>

<details>
  <summary>7. sample</summary>

```bs

```

```js

```

```js

```

</details>

<details>
  <summary>8. sample</summary>

```bs

```

```js

```

```js

```

</details>

<details>
  <summary>9. sample</summary>

```bs

```

```js

```

```js

```

</details>

<details>
  <summary>10. sample</summary>

```bs

```

```js

```

```js

```

</details>

<details>
  <summary>11. sample</summary>

```bs

```

```js

```

```js

```

</details>

<details>
  <summary>12. sample</summary>

```bs

```

```js

```

```js

```

</details>

<details>
  <summary>13. sample</summary>

```bs

```

```js

```

```js

```

</details>

<details>
  <summary>14. sample</summary>

```bs

```

```js

```

```js

```

</details>

<details>
  <summary>15. sample</summary>

```bs

```

```js

```

```js

```

</details>

<details>
  <summary>16. sample</summary>

```bs

```

```js

```

```js

```

</details>

<details>
  <summary>17. sample</summary>

```bs

```

```js

```

```js

```

</details>

<details>
  <summary>18. sample</summary>

```bs

```

```js

```

```js

```

</details>

<details>
  <summary>19. sample</summary>

```bs

```

```js

```

```js

```

</details>

<details>
  <summary>20. sample</summary>

```bs

```

```js

```

```js

```

</details>
