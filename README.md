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
  <summary>4. Create States for Search</summary>

App.js:

```js
import React, { useState } from "react";
import "./App.css";

function App() {
  const [endPoint, setEndPoint] = useState("");
  const [container, setContainer] = useState([]);

  const options = {
    method: "GET",
    headers: {
      "X-RapidAPI-Key": "7990c02530mshdf87d",
      "X-RapidAPI-Host": "online-movie-database.p.rapidapi.com",
    },
  };

  fetch(
    "https://online-movie-database.p.rapidapi.com/auto-complete?q=game%20of%20thr",
    options
  )
    .then((response) => response.json())
    .then((response) => console.log(response))
    .then((data) => setContainer(data))
    .catch((err) => console.error(err));

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
  <summary>5. useQuery</summary>

```js
const {
  data,
  dataUpdatedAt,
  error,
  errorUpdatedAt,
  failureCount,
  failureReason,
  isError,
  isFetched,
  isFetchedAfterMount,
  isFetching,
  isPaused,
  isLoading,
  isLoadingError,
  isPlaceholderData,
  isPreviousData,
  isRefetchError,
  isRefetching,
  isStale,
  isSuccess,
  refetch,
  remove,
  status,
  fetchStatus,
} = useQuery({
  queryKey,
  queryFn,
  cacheTime,
  enabled,
  networkMode,
  initialData,
  initialDataUpdatedAt,
  keepPreviousData,
  meta,
  notifyOnChangeProps,
  onError,
  onSettled,
  onSuccess,
  placeholderData,
  queryKeyHashFn,
  refetchInterval,
  refetchIntervalInBackground,
  refetchOnMount,
  refetchOnReconnect,
  refetchOnWindowFocus,
  retry,
  retryOnMount,
  retryDelay,
  select,
  staleTime,
  structuralSharing,
  suspense,
  useErrorBoundary,
});
```

```js
export const App = ({ props }) => {
  const queryClient = new QueryClient({
    defaultOptions: {
      queries: {
        refetchOnWindowFocus: false,
        refetchOnMount: false,
      },
    },
  });

  return (
    <QueryClientProvider client={queryClient}>
      {...restOfMyApp}
    </QueryClientProvider>
  );
};
```

```js
const client = useQueryClient();
client.invalidateQueries(YOUR_CACHE_KEY, { refetchInactive: true });
```

```js
// emulates a fetch (useQuery expects a Promise)
const emulateFetch = (_) => {
  return new Promise((resolve) => {
    resolve([{ data: "ok" }]);
  });
};

const handleClick = () => {
  // manually refetch
  refetch();
};

const { data, refetch } = useQuery("my_key", emulateFetch, {
  refetchOnWindowFocus: false,
  enabled: false, // disable this query from automatically running
});

return (
  <div>
    <button onClick={handleClick}>Click me</button>
    {JSON.stringify(data)}
  </div>
);
```

```js
// Get the user
const { data: user } = useQuery(["user", email], getUserByEmail);

// Then get the user's projects
const { isIdle, data: projects } = useQuery(
  ["projects", user.id],
  getProjectsByUser,
  {
    // `user` would be `null` at first (falsy),
    // so the query will not execute until the user exists
    enabled: user,
  }
);
```

</details>

<details>
  <summary>6. Completed Project</summary>

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
import { BrowserRouter as Router, Routes, Route } from "react-router-dom";
import { QueryClient, QueryClientProvider } from "@tanstack/react-query";
import "./App.css";
import { Home } from "./pages/Home";

function App() {
  const client = new QueryClient({
    defaultOptions: {
      queries: {
        refetchOnWindowFocus: false,
      },
    },
  });

  return (
    <div>
      <QueryClientProvider client={client}>
        <Router>
          <Routes>
            <Route path="/" element={<Home />} />
          </Routes>
        </Router>
      </QueryClientProvider>
    </div>
  );
}

export default App;
```

styles.css:

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

public/index.html:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <link rel="icon" href="%PUBLIC_URL%/favicon.ico" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <meta name="theme-color" content="#000000" />
    <meta
      name="description"
      content="Web site created using create-react-app"
    />
    <link rel="apple-touch-icon" href="%PUBLIC_URL%/logo192.png" />
    <link rel="manifest" href="%PUBLIC_URL%/manifest.json" />
    <link rel="stylesheet" href="styles.css" />
    <title>React App</title>
  </head>
  <body class="bg-[#334155] text-white">
    <noscript>You need to enable JavaScript to run this app.</noscript>
    <div id="root"></div>
  </body>
</html>
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
