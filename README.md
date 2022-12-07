# Projects

React Practice Projects

## Tutorial

---

### [1-MOVIE SEARCH APP - E-SIDE](#)

Source: https://imdb-api.com/

Video: https://www.youtube.com/watch?v=Li40L8tZcaI

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

useQuery simple Usage:

```js
import { useEffect, useState } from "react";
import {
  QueryClient,
  QueryClientProvider,
  useQuery,
} from "@tanstack/react-query";
import "./styles.css";

export default function App() {
  const client = new QueryClient();

  return (
    <QueryClientProvider client={client}>
      <div className="App">
        <Cat />
      </div>
    </QueryClientProvider>
  );
}

const Cat = () => {
  const { data } = useQuery(["cat"], () =>
    fetch("https://api.thecatapi.com/v1/images/search").then((res) =>
      res.json()
    )
  );

  if (data) console.log(data);
  return <div> </div>;
};
```

useEffect Usage:

```js
import { useEffect, useState } from "react";
import "./styles.css";

export default function App() {
  const [count, setCount] = useState(0);

  // Mounts -> Update -> Unmounting
  useEffect(() => {
    console.log("Updating");
  }, [count]);

  return (
    <div className="App">
      {count}
      <button onClick={() => setCount((prev) => prev + 1)}>
        Increase Count
      </button>
    </div>
  );
}
```

useQuery Properties:

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

Other Examples:

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

Home.js:

```js
import { useState } from "react";
import { useQuery } from "@tanstack/react-query";
import axios from "axios";

export const Home = () => {
  const [tempWord, setTempWord] = useState("");
  const [keyWord, setKeyWord] = useState("");
  const [on, setOn] = useState(true);

  const fetchMovies = () => {
    if (on) {
      return axios
        .request(
          `https://imdb-api.com/en/API/SearchAll/k_3q9vhkmq/${
            keyWord || "Spider"
          }`
        )
        .then((res) => res.data);
    } else {
      return null;
    }
  };

  const { data, isLoading, isError, error, isRefetching, isLoadingError } =
    useQuery([keyWord], fetchMovies, { enabled: true });

  const SubmitHandler = (e) => {
    e.preventDefault();
    setKeyWord(tempWord);
    setTempWord("");
    console.log("refetching...");
  };

  const onChangeHandler = (e) => {
    setTempWord(e.target.value);
  };

  return (
    <div className="m-8">
      <div className="flex flex-col items-center">
        <h1 className="ml-6 text-6xl font-bold font-serif text-slate-300">
          The Movie Search App
        </h1>
        <form
          className="m-6 flex flex-col items-center"
          onSubmit={SubmitHandler}
        >
          <input
            className="text-[#e2e8f0] px-4 py-2 w-96 rounded-lg bg-[#334155] outline-0 ring-4 ring-[#e2e8f0]"
            type="text"
            onChange={onChangeHandler}
            value={tempWord}
            placeholder="Spider..."
          />
          <button
            className="bg-[#0ea5e9] rounded-lg text-white mt-4 w-48 px-2 py-2 border-0"
            type="submit"
          >
            Search
          </button>
        </form>
      </div>
      <div className="flex flex-wrap gap-4 justify-center">
        {isLoading
          ? "Loading...."
          : isRefetching
          ? "Refreshing page..."
          : isError || isLoadingError
          ? `Error Loading Page...${error.message}`
          : !on
          ? "Switched Off...."
          : data?.results.errorMessage
          ? data?.results.errorMessage
          : !data?.results
          ? "Maximum API calls has been used for today. Try again Tomorrow!"
          : data?.results.map((data) => {
              return (
                <div className="flex flex-col items-center" key={data.id}>
                  <img
                    className="w-[250px] h-[350px]"
                    src={
                      !data.image
                        ? "https://m.media-amazon.com/images/M/MV5BZWMyYzFjYTYtNTRjYi00OGExLWE2YzgtOGRmYjAxZTU3NzBiXkEyXkFqcGdeQXVyMzQ0MzA0NTM@._V1_Ratio0.6757_AL_.jpg"
                        : data.image
                    }
                    alt={data.title}
                  />
                  <p className="text-[14px] w-[150px] mt-4 font-bold text-center">
                    {data.title}
                  </p>
                </div>
              );
            })}
      </div>
    </div>
  );
};
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

### [2-CHAT BOT - E-SIDE](#)

Source: https://imdb-api.com/

Video: https://www.youtube.com/watch?v=Li40L8tZcaI

<details>
  <summary>7. Install React App</summary>

```bs
npx create-react-app .
```

```bs
npm start
```

Index.js:

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
      <h1>App</h1>
    </div>
  );
}

export default App;
```

</details>

<details>
  <summary>8. Get Rapid API setup for Chat Bot</summary>

Using Fetch:

```js
const options = {
	method: 'GET',
	headers: {
		'X-RapidAPI-Key': '7990c02530mshdf87db921c2401fp1f5e29jsn311b5da7e4a6',
		'X-RapidAPI-Host': 'chatbot-chatari.p.rapidapi.com'
	}
};

fetch('https://chatbot-chatari.p.rapidapi.com/?message=%2FThat's%20funny!', options)
	.then(response => response.json())
	.then(response => console.log(response))
	.catch(err => console.error(err));
```

Using Axios:

```js
import axios from "axios";

const options = {
  method: "GET",
  url: "https://chatbot-chatari.p.rapidapi.com/",
  params: { message: "/That's funny!" },
  headers: {
    "X-RapidAPI-Key": "7990c02530mshdf87db921c2401fp1f5e29jsn311b5da7e4a6",
    "X-RapidAPI-Host": "chatbot-chatari.p.rapidapi.com",
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

</details>

<details>
  <summary>9. useQuery</summary>

```bs
npm install @tanstack/react-query
npm install axios
```

```js
function Todos() {
  const { isInitialLoading, isError, data, error, refetch, isFetching } =
    useQuery({
      queryKey: ["todos"],
      queryFn: fetchTodoList,
      enabled: false,
    });

  return (
    <div>
      <button onClick={() => refetch()}>Fetch Todos</button>

      {data ? (
        <>
          <ul>
            {data.map((todo) => (
              <li key={todo.id}>{todo.title}</li>
            ))}
          </ul>
        </>
      ) : isError ? (
        <span>Error: {error.message}</span>
      ) : isInitialLoading ? (
        <span>Loading...</span>
      ) : (
        <span>Not ready ...</span>
      )}

      <div>{isFetching ? "Fetching..." : null}</div>
    </div>
  );
}
```

```js
function Todos() {
  const [filter, setFilter] = React.useState('')

  const { data } = useQuery({
      queryKey: ['todos', filter],
      queryFn: () => fetchTodos(filter),
      // ⬇️ disabled as long as the filter is empty
      enabled: !!filter
  })

  return (
      <div>
        // 🚀 applying the filter will enable and execute the query
        <FiltersForm onApply={setFilter} />
        {data && <TodosTable data={data}} />
      </div>
  )
}
```

```js
import "./App.css";
import { useState, useEffect } from "react";

function App() {
  const [time, setTime] = useState("00:00:00 AM");
  const [isON, setIsON] = useState(true);
  const [counter, setCounter] = useState(0);
  const [isBelow, setIsBelow] = useState(false);

  useEffect(() => {
    if (isON) {
      const interval = setInterval(setCurrentTime, 1000);
      return () => clearInterval(interval);
    }
  }, [isON]);

  function setCurrentTime() {
    const date = new Date();
    setTime(date.toLocaleTimeString("en-US"));
  }

  useEffect(() => {
    if (counter < 0) {
      setIsBelow(true);
      setCounter(0);
    } else {
      setIsBelow(false);
    }
  }, [counter]);

  const btnStyleStart = {
    padding: "10px 40px",
    marginRight: "10px",
    color: "white",
    border: "none",
    cursor: "pointer",
    backgroundColor: "green",
  };

  const btnStyleStop = {
    ...btnStyleStart,
    backgroundColor: "red",
  };

  return (
    <div className="App">
      <h1>My Digital Clock</h1>
      <h2 style={{ fontSize: "3rem", color: "gray" }}>{time}</h2>
      <button
        onClick={() => {
          setIsON(true);
          console.log("Starting....");
        }}
        style={btnStyleStart}
      >
        Start
      </button>
      <button
        onClick={() => {
          setIsON(false);
          console.log("Stopping....");
        }}
        style={btnStyleStop}
      >
        Stop
      </button>

      <h2 style={{ fontSize: "4rem", backgroundColor: "#f4f4f4" }}>
        Counter: {counter}
      </h2>
      {isBelow && (
        <h3 style={{ fontSize: "1.5rem", color: "red" }}>
          Sorry, you can't go below zero!
        </h3>
      )}
      <button
        onClick={() => setCounter((count) => count + 1)}
        style={btnStyleStart}
      >
        Increment
      </button>
      <button
        onClick={() => setCounter((count) => count - 1)}
        style={btnStyleStop}
      >
        Decrement
      </button>
    </div>
  );
}

export default App;
```

```js
import {
  QueryClient,
  QueryClientProvider,
  useQuery,
} from "@tanstack/react-query";

const queryClient = new QueryClient();

function Example() {
  const query = useQuery({ queryKey: ["todos"], queryFn: fetchTodos });

  return (
    <div>
      {query.isLoading
        ? "Loading..."
        : query.isError
        ? "Error!"
        : query.data
        ? query.data.map((todo) => <div key={todo.id}>{todo.title}</div>)
        : null}
    </div>
  );
}

function App() {
  return (
    <QueryClientProvider client={queryClient}>
      <Example />
    </QueryClientProvider>
  );
}
```

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
