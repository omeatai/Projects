# Projects

React Practice Projects

## Tutorial

---

### [1-MOVIE SEARCH APP - E-SIDE](#)

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

```js
return (
  <div>
    <h1>Bot: {reply}</h1>
    <h2>status: {status}</h2> // loading -> success
    <h2>fetchStatus: {fetchStatus}</h2> // fetching -> idle
  </div>
);
```

</details>

<details>
  <summary>10. Completed Chat Bot 1 (without tailwindCSS)</summary>

App.js:

```js
import { useState, useEffect } from "react";
import {
  QueryClient,
  QueryClientProvider,
  useQuery,
} from "@tanstack/react-query";
import axios from "axios";
import "./App.css";

export default function App() {
  const client = new QueryClient({
    defaultOptions: {
      queries: {
        refetchOnWindowFocus: false,
      },
    },
  });

  return (
    <QueryClientProvider client={client}>
      <div className="App">
        <ChatBot />
      </div>
    </QueryClientProvider>
  );
}

const ChatBot = () => {
  const [started, setStarted] = useState(false);
  const [info, setInfo] = useState("");
  const [msg, setMsg] = useState("");
  const [reply, setReply] = useState("");

  const encodedParams = new URLSearchParams();
  encodedParams.append("in", msg);
  encodedParams.append("op", "in");
  encodedParams.append("cbot", "1");
  encodedParams.append("SessionID", "RapidAPI1");
  encodedParams.append("cbid", "1");
  encodedParams.append("key", "RHMN5hnQ4wTYZBGCF3dfxzypt68rVP");
  encodedParams.append("ChatSource", "RapidAPI");
  encodedParams.append("duration", "1");

  const options = {
    method: "POST",
    url: "https://robomatic-ai.p.rapidapi.com/api",
    headers: {
      "content-type": "application/x-www-form-urlencoded",
      "X-RapidAPI-Key": "7990c02530mshdf87db921c2401fp1f5e29jsn311b5da7e4a6",
      "X-RapidAPI-Host": "robomatic-ai.p.rapidapi.com",
    },
    data: encodedParams,
  };

  const submitHandler = (e) => {
    e.preventDefault();
    setStarted(true);
    setMsg(info);
    setInfo("");
  };

  const fetchData = () => {
    return axios.request(options).then((res) => res.data);
  };

  const { data, isInitialLoading, isError, error, status, fetchStatus } =
    useQuery({
      queryKey: [msg],
      queryFn: fetchData,
      enabled: true,
    });

  useEffect(() => {
    if (!started) {
      setReply("Hi! Want to chat with me?");
    } else if (data) {
      setReply(data.out);
    } else if (isError) {
      setReply(`Sorry there was an Error: ${error.message}`);
    } else if (isInitialLoading) {
      setReply("Typing....");
      const interval = setInterval(() => {
        if (!data) {
          setReply(
            "Sorry, I'm not sure I got that right... Can you say something else."
          );
        }
      }, 5000);
      return () => clearInterval(interval);
    }
  }, [data, isError, error, isInitialLoading, started]);

  return (
    <div>
      <form onSubmit={submitHandler}>
        <input
          onChange={(e) => setInfo(e.target.value)}
          type="text"
          value={info}
          placeholder="Say Something..."
        />
        <button>Chat</button>
      </form>
      <h1>Bot: {reply}</h1>
      <h2>status: {status}</h2>
      <h2>fetchStatus: {fetchStatus}</h2>
    </div>
  );
};
```

</details>

<details>
  <summary>11. Setup TailwindCSS</summary>

```bs
npx create-react-app my-project
cd my-project
```

```bs
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p
```

tailwind.config.js:

```js
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: ["./src/**/*.{js,jsx,ts,tsx}"],
  theme: {
    extend: {},
  },
  plugins: [],
};
```

index.css:

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

```js
"scripts": {
    "build-css": "tailwindcss build -i src/index.css -o public/index.css --watch"
  },
```

```bs
npm run build-css
npx tailwindcss -i ./src/styles.css -o ./public/styles.css --watch
npx tailwindcss -i ./src/input.css -o ./dist/output.css --watch

npm run start
```

App.js:

```js
export default function App() {
  return <h1 className="text-3xl font-bold underline">Hello world!</h1>;
}
```

</details>

<details>
  <summary>12. Install DOTENV</summary>

```bs
npm install dotenv --save
```

```bs
REACT_APP_KEY=RHMN5hnQ4wTYZBGCF
#process.env.REACT_APP_KEY
```

</details>

<details>
  <summary>13. Completed Project</summary>

App.js:

```js
import { useState, useEffect } from "react";
import {
  QueryClient,
  QueryClientProvider,
  useQuery,
} from "@tanstack/react-query";
import axios from "axios";
import "./App.css";

export default function App() {
  const client = new QueryClient({
    defaultOptions: {
      queries: {
        refetchOnWindowFocus: false,
      },
    },
  });

  return (
    <QueryClientProvider client={client}>
      <div className="App">
        <ChatBot />
      </div>
    </QueryClientProvider>
  );
}

const ChatBot = () => {
  const [started, setStarted] = useState(false);
  const [info, setInfo] = useState("");
  const [msg, setMsg] = useState("");
  const [reply, setReply] = useState("");

  const encodedParams = new URLSearchParams();
  encodedParams.append("in", msg);
  encodedParams.append("op", "in");
  encodedParams.append("cbot", "1");
  encodedParams.append("SessionID", "RapidAPI1");
  encodedParams.append("cbid", "1");
  encodedParams.append("key", "RHMN5hnQ4wTYZBGCF3dfxzy");
  encodedParams.append("ChatSource", "RapidAPI");
  encodedParams.append("duration", "1");

  const options = {
    method: "POST",
    url: "https://robomatic-ai.p.rapidapi.com/api",
    headers: {
      "content-type": "application/x-www-form-urlencoded",
      "X-RapidAPI-Key": "7990c02530mshdf87db921c2401fp1f5e29j",
      "X-RapidAPI-Host": "robomatic-ai.p.rapidapi.com",
    },
    data: encodedParams,
  };

  const submitHandler = (e) => {
    e.preventDefault();
    setStarted(true);
    setMsg(info);
    setInfo("");
  };

  const fetchData = () => {
    return axios.request(options).then((res) => res.data);
  };

  const { data, isInitialLoading, isError, error } = useQuery({
    queryKey: [msg],
    queryFn: fetchData,
    enabled: true,
  });

  useEffect(() => {
    if (!started) {
      setReply("Hi! Want to chat with me?");
    } else if (data) {
      setReply(data.out);
    } else if (isError) {
      setReply(`Sorry there was an Error: ${error.message}`);
    } else if (isInitialLoading) {
      setReply("Typing....");
      const interval = setInterval(() => {
        if (!data) {
          setReply("Sorry, I'm trying to understand what you just said...");
        }
      }, 8000);
      return () => clearInterval(interval);
    }
  }, [data, isError, error, isInitialLoading, started]);

  return (
    <div className="flex flex-col text-center mt-32">
      <h1 className="font-sans font-semibold text-7xl text-white">ChatBOT</h1>
      <form
        onSubmit={submitHandler}
        className="mt-12 flex flex-col items-center"
      >
        <input
          className="text-center w-[80%] rounded-full py-3 text-2xl border border-[#bdc1c6] outline-0 bg-[#202124] hover:bg-[#303134] text-[#bdc1c6] font-semibold"
          onChange={(e) => setInfo(e.target.value)}
          type="text"
          value={info}
          placeholder="Say Something..."
        />
        <button className="my-12 py-4 px-16 border-0 rounded-lg text-[#e8eaed] font-bold bg-[#303134] hover:bg-blue-600 active:bg-blue-800">
          Chat
        </button>
        <h2 className="text-[#bdc1c6] text-2xl">Bot:</h2>
        <div className="py-8 w-[60%] font-bold text-2xl rounded-2xl text-[#bdc1c6]">
          {reply}
        </div>
      </form>
    </div>
  );
};
```

tailwind.config.js:

```js
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: ["./src/**/*.{js,jsx,ts,tsx}"],
  theme: {
    fontFamily: {
      sans: ["ui-sans-serif", "system-ui"],
    },
    extend: {},
  },
  plugins: [],
};
```

</details>

<details>
  <summary>14. Deploy to Github</summary>

Git:

```bs
#Just follow next steps in console terminal ;)
git init	#Initialize git in folder
git add .	#add all files of folder to be pushed
git commit -m "First commit"	#add first commit
git remote add origin remote_repository_URL #replace with your remote repo url
git remote -v	#verify that your remote repository url is properly found
git branch -M main  #change main branch name to main
git push --force origin main	#force pushing your project into github repo

//make sure you're on the local branch, then:
git pull origin YourRemoteBranch
//which is the same as:
git fetch origin YourRemoteBranch
git merge origin/YourRemoteBranch

git push origin --delete feature/login
git push origin --delete master

# Push newly created local branch to remote
git push --set-upstream origin <branch name>
git push --force origin main //force pushing to remote github repo
git push -u origin new_branch

github@branch/c/remote/push  (new-branch)
git clone https://github.com/learn-git-fast/git-branch-examples.git
cd git*
git checkout -b new-branch

github@branch/c/remote/push (new-branch)
git branch -a
touch devolution.jpg
git add .
git commit -m "Are we not gender neutral people? We are Devo?"
git push --set-upstream origin new-branch

git pull --rebase origin main
# Resolve merge conflicts if needed
git push origin main
```

Github Pages:

```bs
echo "# my-project" >> README.md
git init
git add .
# git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/machadop1487/my-project.git
git push -u origin main
```

```bs
git remote add origin https://github.com/machadop1487/my-project.git
git branch -M main
git push -u origin main
```

```bs
git remote -v
git remote remove origin
git remote add origin https://<your-username>:<token>@github.com/<username>/<repo-name>.git
```

```bs
npm install gh-pages --save-dev
```

</details>

### [3-WEATHER API APP - CODE COMMERCE](#)

<details>
  <summary>15. Install Tailwind CSS with Next.js</summary>

```bs
npx create-next-app@latest my-project --typescript --eslint
cd my-project

npx create-next-app@latest .
```

```bs
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p
```

tailwind.config.js:

```js
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: [
    "./pages/**/*.{js,ts,jsx,tsx}",
    "./components/**/*.{js,ts,jsx,tsx}",
  ],
  theme: {
    extend: {},
  },
  plugins: [],
};
```

styles/globals.css:

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

Start your dev process:

```bs
npm run dev
```

Start using Tailwind in your project:

```js
export default function Home() {
  return <h1 className="text-3xl font-bold underline">Hello world!</h1>;
}
```

</details>

<details>
  <summary>16. Open Weather Map API</summary>

```bs
https://openweathermap.org/api
```

API call:

```bs
https://api.openweathermap.org/data/2.5/weather?lat={lat}&lon={lon}&appid={API key}
```

Parameters:

```bs
lat, lon = (required)

Geographical coordinates (latitude, longitude). If you need the geocoder to automatic convert city names and zip-codes to geo coordinates and the other way around, please use our Geocoding API.

appid =	(required)

Your unique API key (you can always find it on your account page under the "API key" tab)

mode =	(optional)

Response format. Possible values are xml and html. If you don't use the mode parameter format is JSON by default.

units =	(optional)

Units of measurement. standard, metric and imperial units are available. If you do not use the units parameter, standard units will be applied by default.

lang = (optional)
You can use this parameter to get the output in your language.
```

Example of API call:

```bs
https://api.openweathermap.org/data/2.5/weather?lat=44.34&lon=10.99&appid={API key}
```

```js
// {
//   "coord": {
//     "lon": 10.99,
//     "lat": 44.34
//   },
//   "weather": [
//     {
//       "id": 501,
//       "main": "Rain",
//       "description": "moderate rain",
//       "icon": "10d"
//     }
//   ],
//   "base": "stations",
//   "main": {
//     "temp": 298.48,
//     "feels_like": 298.74,
//     "temp_min": 297.56,
//     "temp_max": 300.05,
//     "pressure": 1015,
//     "humidity": 64,
//     "sea_level": 1015,
//     "grnd_level": 933
//   },
//   "visibility": 10000,
//   "wind": {
//     "speed": 0.62,
//     "deg": 349,
//     "gust": 1.18
//   },
//   "rain": {
//     "1h": 3.16
//   },
//   "clouds": {
//     "all": 100
//   },
//   "dt": 1661870592,
//   "sys": {
//     "type": 2,
//     "id": 2075663,
//     "country": "IT",
//     "sunrise": 1661834187,
//     "sunset": 1661882248
//   },
//   "timezone": 7200,
//   "id": 3163858,
//   "name": "Zocca",
//   "cod": 200
// }
```

Fields in API response:

```bs
coord
    coord.lon = City geo location, longitude
    coord.lat = City geo location, latitude
weather (more info Weather condition codes)
    weather.id = Weather condition id
    weather.main = Group of weather parameters (Rain, Snow, Extreme etc.)
    weather.description = Weather condition within the group. You can get the output in your language.
    weather.icon = Weather icon id
base - (Internal parameter)
main
    main.temp = Temperature. Unit Default: Kelvin, Metric: Celsius, Imperial: Fahrenheit.
    main.feels_like = Temperature. This temperature parameter accounts for the human perception of weather. Unit Default: Kelvin, Metric: Celsius, Imperial: Fahrenheit.
    main.pressure = Atmospheric pressure (on the sea level, if there is no sea_level or grnd_level data), hPa
    main.humidity = Humidity, %
    main.temp_min = Minimum temperature at the moment. This is minimal currently observed temperature (within large megalopolises and urban areas). Unit Default: Kelvin, Metric: Celsius, Imperial: Fahrenheit.
    main.temp_max = Maximum temperature at the moment. This is maximal currently observed temperature (within large megalopolises and urban areas). Unit Default: Kelvin, Metric: Celsius, Imperial: Fahrenheit.
    main.sea_level = Atmospheric pressure on the sea level, hPa
    main.grnd_level = Atmospheric pressure on the ground level, hPa
visibility - (Visibility, meter. The maximum value of the visibility is 10km)
wind
    wind.speed = Wind speed. Unit Default: meter/sec, Metric: meter/sec, Imperial: miles/hour.
    wind.deg = Wind direction, degrees (meteorological)
    wind.gust = Wind gust. Unit Default: meter/sec, Metric: meter/sec, Imperial: miles/hour
clouds
    clouds.all = Cloudiness, %
rain
    rain.1h = Rain volume for the last 1 hour, mm
    rain.3h = Rain volume for the last 3 hours, mm
snow
    snow.1h = Snow volume for the last 1 hour, mm
    snow.3h = Snow volume for the last 3 hours, mm
dt - (Time of data calculation, unix, UTC)
sys
    sys.type = Internal parameter
    sys.id = Internal parameter
    sys.message = Internal parameter
    sys.country = Country code (GB, JP etc.)
    sys.sunrise = Sunrise time, unix, UTC
    sys.sunset = Sunset time, unix, UTC
timezone - (Shift in seconds from UTC)
id - (City ID. Please note that built-in geocoder functionality has been deprecated.)
name - (City name. Please note that built-in geocoder functionality has been deprecated.)
cod - Internal parameter
```

Built-in API request by city name

```bs
https://api.openweathermap.org/data/2.5/weather?q={city name}&appid={API key}

https://api.openweathermap.org/data/2.5/weather?q={city name},{country code}&appid={API key}

https://api.openweathermap.org/data/2.5/weather?q={city name},{state code},{country code}&appid={API key}
```

Parameters:

```bs
q	= (required)
City name, state code and country code divided by comma, Please, refer to ISO 3166 for the state codes or country codes. You can specify the parameter not only in English. In this case, the API response should be returned in the same language as the language of requested location name if the location is in our predefined list of more than 200,000 locations.

appid	= (required)
Your unique API key (you can always find it on your account page under the "API key" tab)

mode	= (optional)
Response format. Possible values are xml and html. If you don't use the mode parameter format is JSON by default.

units	= (optional)
Units of measurement. standard, metric and imperial units are available. If you do not use the units parameter, standard units will be applied by default.

lang	= (optional)	You can use this parameter to get the output in your language.
```

Examples of API calls:

```bs
https://api.openweathermap.org/data/2.5/weather?q=London&appid={API key}

https://api.openweathermap.org/data/2.5/weather?q=London,uk&appid={API key}
```

```js
//  {
//      "coord": {
//        "lon": -0.13,
//        "lat": 51.51
//      },
//      "weather": [
//        {
//          "id": 300,
//          "main": "Drizzle",
//          "description": "light intensity drizzle",
//          "icon": "09d"
//        }
//      ],
//      "base": "stations",
//      "main": {
//        "temp": 280.32,
//        "pressure": 1012,
//        "humidity": 81,
//        "temp_min": 279.15,
//        "temp_max": 281.15
//      },
//      "visibility": 10000,
//      "wind": {
//        "speed": 4.1,
//        "deg": 80
//      },
//      "clouds": {
//        "all": 90
//      },
//      "dt": 1485789600,
//      "sys": {
//        "type": 1,
//        "id": 5091,
//        "message": 0.0103,
//        "country": "GB",
//        "sunrise": 1485762037,
//        "sunset": 1485794875
//      },
//      "id": 2643743,
//      "name": "London",
//      "cod": 200
//      }
```

</details>

<details>
  <summary>17. process.env.NEXT_PUBLIC_WEATHER_KEY</summary>

.env:

```bs
NEXT_PUBLIC_WEATHER_KEY=3cca10d146d8b3c13a253d4b5a8
```

index.js:

```js
import Head from "next/head";
import Image from "next/image";

export default function Home() {
  const url = `https://api.openweathermap.org/data/2.5/weather?q=dubai&appid=${process.env.NEXT_PUBLIC_WEATHER_KEY}`;

  return (
    <div>
      <Head>
        <title>Weather App</title>
        <meta name="description" content="Generated by create next app" />
        <link rel="icon" href="/favicon.ico" />
      </Head>

      <h1>Hello</h1>
    </div>
  );
}
```

</details>

<details>
  <summary>18. Install Axios and React-Icons Dependencies</summary>

```bs
npm install axios
npm install react-icons
```

```bs
yarn add axios
yarn add react-icons
```

</details>

<details>
  <summary>19. Fetch Weather</summary>

index.js:

```js
import Head from "next/head";
import Image from "next/image";
import axios from "axios";
import { useState } from "react";
import { BsSearch } from "react-icons/bs";

export default function Home() {
  const [city, setCity] = useState(" ");
  const [weather, setWeather] = useState({});
  const [loading, setLoading] = useState(false);

  const url = `https://api.openweathermap.org/data/2.5/weather?q=dubai&units=metric&appid=${process.env.NEXT_PUBLIC_WEATHER_KEY}`;

  const fetchWeather = (e) => {
    e.preventDefault();
    setLoading(true);
    axios.get(url).then((response) => {
      setWeather(response.data);
      console.log(response.data);
    });
    setCity("");
    setLoading(false);
  };

  return (
    <div>
      <Head>
        <title>Create Next App</title>
        <meta name="description" content="Generated by create next app" />
        <link rel="icon" href="/favicon.ico" />
      </Head>

      <button onClick={fetchWeather}>Fetch data</button>
    </div>
  );
}
```

```js
// {
//     "coord": {
//         "lon": 55.3047,
//         "lat": 25.2582
//     },
//     "weather": [
//         {
//             "id": 800,
//             "main": "Clear",
//             "description": "clear sky",
//             "icon": "01n"
//         }
//     ],
//     "base": "stations",
//     "main": {
//         "temp": 24.54,
//         "feels_like": 24.2,
//         "temp_min": 22.16,
//         "temp_max": 24.96,
//         "pressure": 1016,
//         "humidity": 44
//     },
//     "visibility": 10000,
//     "wind": {
//         "speed": 3.09,
//         "deg": 340
//     },
//     "clouds": {
//         "all": 0
//     },
//     "dt": 1670858181,
//     "sys": {
//         "type": 1,
//         "id": 7537,
//         "country": "AE",
//         "sunrise": 1670813685,
//         "sunset": 1670851811
//     },
//     "timezone": 14400,
//     "id": 292223,
//     "name": "Dubai",
//     "cod": 200
// }
```

</details>

<details>
  <summary>20. Set Background Image</summary>

pages/index.js:

```js
import Head from "next/head";
import Image from "next/image";
import axios from "axios";
import { useState } from "react";
import { BsSearch } from "react-icons/bs";

export default function Home() {
  const [city, setCity] = useState(" ");
  const [weather, setWeather] = useState({});
  const [loading, setLoading] = useState(false);

  const url = `https://api.openweathermap.org/data/2.5/weather?q=dubai&units=metric&appid=${process.env.NEXT_PUBLIC_WEATHER_KEY}`;

  const fetchWeather = (e) => {
    e.preventDefault();
    setLoading(true);
    axios.get(url).then((response) => {
      setWeather(response.data);
      console.log(response.data);
    });
    setCity("");
    setLoading(false);
  };

  return (
    <div>
      <Head>
        <title>WEATHER APP</title>
        <meta name="description" content="Generated by create next app" />
        <link rel="icon" href="/favicon.ico" />
      </Head>
      {/* Overlay */}
      <div className="absolute top-0 right-0 bottom-0 left-0 bg-black/50 z-[1]" />

      {/* Background Image */}
      <Image
        src="https://images.unsplash.com/photo-1542574115512-0444396fc6fb?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1470&q=80"
        alt="Background Image"
        className="object-cover"
        fill
      />

      <button onClick={fetchWeather}>Fetch data</button>
    </div>
  );
}
```

next.config.js

```js
/** @type {import('next').NextConfig} */
const nextConfig = {
  reactStrictMode: true,
};

module.exports = {
  nextConfig,
  images: {
    domains: ["images.unsplash.com"],
  },
};
```

Restart Server:

```bs
clear
npm run dev
yarn dev
```

</details>

<details>
  <summary>21. Create and Style Search Input</summary>

pages/index.js:

```js
import Head from "next/head";
import Image from "next/image";
import axios from "axios";
import { useState } from "react";
import { BsSearch } from "react-icons/bs";

export default function Home() {
  const [city, setCity] = useState(" ");
  const [weather, setWeather] = useState({});
  const [loading, setLoading] = useState(false);

  const url = `https://api.openweathermap.org/data/2.5/weather?q=dubai&units=metric&appid=${process.env.NEXT_PUBLIC_WEATHER_KEY}`;

  const fetchWeather = (e) => {
    e.preventDefault();
    setLoading(true);
    axios.get(url).then((response) => {
      setWeather(response.data);
      console.log(response.data);
    });
    setCity("");
    setLoading(false);
  };

  return (
    <div>
      <Head>
        <title>WEATHER APP</title>
        <meta name="description" content="Generated by create next app" />
        <link rel="icon" href="/favicon.ico" />
      </Head>
      {/* Overlay */}
      <div className="absolute top-0 right-0 bottom-0 left-0 bg-black/50 z-[1]" />

      {/* Background Image */}
      <Image
        src="https://images.unsplash.com/photo-1598899246709-c8273815f3ef?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1932&q=80"
        alt="Background Image"
        className="object-cover"
        fill
      />

      {/* Search */}
      <div className="relative flex justify-between items-center max-w-[500px] w-full m-auto pt-4 text-white z-10">
        <form className="flex justify-between items-center w-full m-auto p-3 bg-transparent border border-gray-300 text-white rounded-2xl">
          <div>
            <input
              className="bg-transparent border-none text-white focus:outline-none text-2xl placeholder:text-gray-400 w-[400px] pl-4"
              type="text"
              placeholder="Search city"
            />
          </div>
          <button onClick={fetchWeather}>
            <BsSearch size={25} />
          </button>
        </form>
      </div>
    </div>
  );
}
```

</details>

<details>
  <summary>22. setCity and Fetch Weather</summary>

```js
import Head from "next/head";
import Image from "next/image";
import axios from "axios";
import { useState } from "react";
import { BsSearch } from "react-icons/bs";

export default function Home() {
  const [city, setCity] = useState(" ");
  const [weather, setWeather] = useState({});
  const [loading, setLoading] = useState(false);
  const [errorMessage, setErrorMessage] = useState("");

  const url = `https://api.openweathermap.org/data/2.5/weather?q=${city}&units=metric&appid=${process.env.NEXT_PUBLIC_WEATHER_KEY}`;

  const fetchWeather = (e) => {
    e.preventDefault();
    setLoading(true);
    setErrorMessage("");
    axios
      .get(url)
      .then((response) => {
        setWeather(response.data);
        console.log(response.data);
      })
      //.catch((err) => console.error(err))
      .catch((err) => {
        err.response.status === 404 ? setErrorMessage(err) : console.log(err);
      });
    setCity("");
    setLoading(false);
  };

  return (
    <div>
      <Head>
        <title>WEATHER APP</title>
        <meta name="description" content="Generated by create next app" />
        <link rel="icon" href="/favicon.ico" />
      </Head>
      {/* Overlay */}
      <div className="absolute top-0 right-0 bottom-0 left-0 bg-black/50 z-[1]" />

      {/* Background Image */}
      <Image
        src="https://images.unsplash.com/photo-1598899246709-c8273815f3ef?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1932&q=80"
        alt="Background Image"
        className="object-cover"
        fill
      />

      {/* Search */}
      <div className="relative flex flex-col justify-between items-center max-w-[500px] w-full m-auto pt-4 text-white z-10">
        <form
          onSubmit={fetchWeather}
          className="flex justify-between items-center w-full m-auto p-3 bg-transparent border border-gray-300 text-white rounded-2xl"
        >
          <div>
            <input
              onChange={(e) => setCity(e.target.value)}
              className="bg-transparent border-none text-white focus:outline-none text-2xl placeholder:text-gray-400 w-[400px] pl-4"
              type="text"
              placeholder="Search city"
            />
          </div>
          <button>
            <BsSearch size={25} />
          </button>
        </form>
        <p className="mt-8 text-2xl">
          {errorMessage ? "Sorry, no records for city." : null}
        </p>
      </div>
    </div>
  );
}
```

</details>

<details>
  <summary>23. Setting up Weather Component</summary>

pages/index.js:

```js
import Head from "next/head";
import Image from "next/image";
import axios from "axios";
import { useState } from "react";
import { BsSearch } from "react-icons/bs";
import Weather from "../components/Weather";

export default function Home() {
  const [city, setCity] = useState(" ");
  const [weather, setWeather] = useState({});
  const [loading, setLoading] = useState(false);
  const [errorMessage, setErrorMessage] = useState("");

  const url = `https://api.openweathermap.org/data/2.5/weather?q=${city}&units=metric&appid=${process.env.NEXT_PUBLIC_WEATHER_KEY}`;

  const fetchWeather = (e) => {
    e.preventDefault();
    setLoading(true);
    setErrorMessage("");
    axios
      .get(url)
      .then((response) => {
        setWeather(response.data);
        // console.log(response.data)
      })
      //.catch((err) => console.error(err))
      .catch((err) => {
        err.response.status === 404 ? setErrorMessage(err) : console.log(err);
      });
    setCity("");
    setLoading(false);
  };

  return (
    <div>
      <Head>
        <title>WEATHER APP</title>
        <meta name="description" content="Generated by create next app" />
        <link rel="icon" href="/favicon.ico" />
      </Head>
      {/* Overlay */}
      <div className="absolute top-0 right-0 bottom-0 left-0 bg-black/50 z-[1]" />

      {/* Background Image */}
      <Image
        src="https://images.unsplash.com/photo-1598899246709-c8273815f3ef?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1932&q=80"
        alt="Background Image"
        className="object-cover"
        fill
      />

      {/* Search */}
      <div className="relative flex flex-col justify-between items-center max-w-[500px] w-full m-auto pt-4 text-white z-10">
        <form
          onSubmit={fetchWeather}
          className="flex justify-between items-center w-full m-auto p-3 bg-transparent border border-gray-300 text-white rounded-2xl"
        >
          <div>
            <input
              onChange={(e) => setCity(e.target.value)}
              className="bg-transparent border-none text-white focus:outline-none text-2xl placeholder:text-gray-400 w-[400px] pl-4"
              type="text"
              placeholder="Search city"
              value={city}
            />
          </div>
          <button>
            <BsSearch size={25} />
          </button>
        </form>
        <p className="mt-8 text-2xl">
          {errorMessage ? "Sorry, no records for city." : null}
        </p>
      </div>

      {/* Weather */}
      {weather?.main && <Weather data={weather} />}
    </div>
  );
}
```

components/Weather.js:

```js
import React from "react";

const Weather = ({ data }) => {
  return (
    <div className="relative justify-between items-center max-w-[500px] w-full m-auto pt-4 text-white z-10">
      {Object.keys(data.main).map((key) => {
        return (
          <p key={key}>
            {key}: {data.main[key]}
          </p>
        );
      })}
    </div>
  );
};

export default Weather;
```

</details>

<details>
  <summary>24. Set up Spinner</summary>

pages/index.js:

```js
import Head from "next/head";
import Image from "next/image";
import axios from "axios";
import { useState } from "react";
import { BsSearch } from "react-icons/bs";
import Weather from "../components/Weather";
import Spinner from "../components/Spinner";

export default function Home() {
  const [city, setCity] = useState("");
  const [weather, setWeather] = useState({});
  const [loading, setLoading] = useState(false);
  const [errorMessage, setErrorMessage] = useState("");

  const url = `https://api.openweathermap.org/data/2.5/weather?q=${city}&units=metric&appid=${process.env.NEXT_PUBLIC_WEATHER_KEY}`;

  const fetchWeather = (e) => {
    e.preventDefault();
    setLoading(true);
    setErrorMessage("");
    axios
      .get(url)
      .then((response) => {
        setWeather(response.data);
        // console.log(response.data)
      })
      //.catch((err) => console.error(err))
      .catch((err) => {
        err?.response.status === 404 ? setErrorMessage(err) : console.log(err);
      });
    setCity("");
    setLoading(false);
  };

  return (
    <div>
      <Head>
        <title>WEATHER APP</title>
        <meta name="description" content="Generated by create next app" />
        <link rel="icon" href="/favicon.ico" />
      </Head>
      {/* Overlay */}
      <div className="absolute top-0 right-0 bottom-0 left-0 bg-black/50 z-[1]" />

      {/* Background Image */}
      <Image
        src="https://images.unsplash.com/photo-1598899246709-c8273815f3ef?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1932&q=80"
        alt="Background Image"
        className="object-cover"
        fill
      />

      {/* Search */}
      <div className="relative flex flex-col justify-between items-center max-w-[500px] w-full m-auto pt-4 text-white z-10">
        <form
          onSubmit={fetchWeather}
          className="flex justify-between items-center w-full m-auto p-3 bg-transparent border border-gray-300 text-white rounded-2xl"
        >
          <div>
            <input
              onChange={(e) => setCity(e.target.value)}
              className="bg-transparent border-none text-white focus:outline-none text-2xl placeholder:text-gray-400 w-[400px] pl-4"
              type="text"
              placeholder="Search city"
              value={city}
            />
          </div>
          <button>
            <BsSearch size={25} />
          </button>
        </form>
        <p className="mt-8 text-2xl">
          {errorMessage ? "Sorry, no records for city." : null}
        </p>
      </div>

      {/* Weather */}
      {loading ? (
        <Spinner />
      ) : weather?.main ? (
        <Weather data={weather} />
      ) : null}
    </div>
  );
}
```

components/Spinner.jsx:

```js
import React from "react";
import spinner from "../public/spinner2.svg";
import Image from "next/image";

const Spinner = () => {
  return (
    <>
      <Image
        className="relative z-10 w-[200px] m-auto block"
        src={spinner}
        alt="Loading..."
      />
    </>
  );
};

export default Spinner;
```

</details>

<details>
  <summary>25. Set Weather Image</summary>

pages/index.js:

```js
import Head from "next/head";
import Image from "next/image";
import axios from "axios";
import { useState } from "react";
import { BsSearch } from "react-icons/bs";
import Weather from "../components/Weather";
import Spinner from "../components/Spinner";

export default function Home() {
  const [city, setCity] = useState("");
  const [weather, setWeather] = useState({});
  const [loading, setLoading] = useState(false);
  const [errorMessage, setErrorMessage] = useState("");

  const url = `http://api.openweathermap.org/data/2.5/weather?q=${city}&units=metric&appid=${process.env.NEXT_PUBLIC_WEATHER_KEY}`;

  const fetchWeather = (e) => {
    e.preventDefault();
    setLoading(true);
    setErrorMessage("");
    axios
      .get(url)
      .then((response) => {
        setWeather(response.data);
        // console.log(response.data)
      })
      //.catch((err) => console.error(err))
      .catch((err) => {
        err?.response.status === 404 ? setErrorMessage(err) : console.log(err);
      });
    setCity("");
    setLoading(false);
  };

  return (
    <div>
      <Head>
        <title>Weather - Next App</title>
        <meta name="description" content="Generated by create next app" />
        <link rel="icon" href="/favicon.ico" />
      </Head>
      {/* Overlay */}
      <div className="absolute top-0 right-0 bottom-0 left-0 bg-black/50 z-[1]" />

      {/* Background Image */}
      <Image
        src="https://images.unsplash.com/photo-1598899246709-c8273815f3ef?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1932&q=80"
        alt="Background Image"
        className="object-cover"
        fill
      />

      {/* Search */}
      <div className="relative flex flex-col justify-between items-center max-w-[500px] w-full m-auto pt-4 text-white z-10">
        <form
          onSubmit={fetchWeather}
          className="flex justify-between items-center w-full m-auto p-3 bg-transparent border border-gray-300 text-white rounded-2xl"
        >
          <div>
            <input
              onChange={(e) => setCity(e.target.value)}
              className="bg-transparent border-none text-white focus:outline-none text-2xl placeholder:text-gray-400 w-[400px] pl-4"
              type="text"
              placeholder="Search city"
              value={city}
            />
          </div>
          <button>
            <BsSearch size={25} />
          </button>
        </form>
        <p className="mt-8 text-2xl">
          {errorMessage ? "Sorry, no records for city." : null}
        </p>
      </div>

      {/* Weather */}
      <div className="relative items-center max-w-[500px] w-full m-auto pt-4 text-white z-10">
        {loading ? (
          <Spinner />
        ) : weather?.main ? (
          <Weather data={weather} />
        ) : null}
      </div>
    </div>
  );
}
```

components/Weather.jsx:

```js
import React from "react";
import Image from "next/image";

const Weather = ({ data }) => {
  console.log(data);

  return (
    <div>
      <div>
        <div>
          <Image
            src={`https://openweathermap.org/img/wn/${data.weather[0].icon}@2x.png`}
            alt="icon"
            width="100"
            height="100"
          />
        </div>
      </div>
    </div>
  );
};

export default Weather;
```

next.config.js:

```js
/** @type {import('next').NextConfig} */
const nextConfig = {
  reactStrictMode: true,
};

module.exports = {
  nextConfig,
  images: {
    domains: ["images.unsplash.com", "openweathermap.org"],
  },
};
```

restart server:

```bs
npm run dev
yarn dev
```

</details>

<details>
  <summary>26. Final Project</summary>

index.js:

```js
import Head from "next/head";
import Image from "next/image";
import axios from "axios";
import { useState } from "react";
import { BsSearch } from "react-icons/bs";
import Weather from "../components/Weather";
import Spinner from "../components/Spinner";

export default function Home() {
  const [city, setCity] = useState("");
  const [weather, setWeather] = useState({});
  const [loading, setLoading] = useState(false);
  const [errorMessage, setErrorMessage] = useState("");

  const url = `http://api.openweathermap.org/data/2.5/weather?q=${city}&units=metric&appid=${process.env.NEXT_PUBLIC_WEATHER_KEY}`;

  const fetchWeather = (e) => {
    e.preventDefault();
    setLoading(true);
    setErrorMessage("");
    axios
      .get(url)
      .then((response) => {
        setWeather(response.data);
        // console.log(response.data)
      })
      //.catch((err) => console.error(err))
      .catch((err) => {
        err?.response.status === 404 ? setErrorMessage(err) : console.log(err);
      });
    setCity("");
    setLoading(false);
  };

  return (
    <div>
      <Head>
        <title>Weather - Next App</title>
        <meta name="description" content="Generated by create next app" />
        <link rel="icon" href="/favicon.ico" />
      </Head>
      {/* Overlay */}
      <div className="absolute top-0 right-0 bottom-0 left-0 bg-black/50 z-[1]" />

      {/* Background Image */}
      <Image
        src="https://images.unsplash.com/photo-1598899246709-c8273815f3ef?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1932&q=80"
        alt="Background Image"
        className="object-cover"
        fill
      />

      {/* Search */}
      <div className="relative flex flex-col justify-between items-center max-w-[500px] w-full m-auto pt-4 text-white z-10">
        <form
          onSubmit={fetchWeather}
          className="flex justify-between items-center w-full m-auto p-3 bg-transparent border border-gray-300 text-white rounded-2xl"
        >
          <div>
            <input
              onChange={(e) => setCity(e.target.value)}
              className="bg-transparent border-none text-white focus:outline-none text-2xl placeholder:text-gray-400 w-[400px] pl-4"
              type="text"
              placeholder="Search city"
              value={city}
            />
          </div>
          <button>
            <BsSearch size={25} />
          </button>
        </form>
        <p className="mt-8 text-2xl">
          {errorMessage ? "Sorry, no records for city." : null}
        </p>
      </div>

      {/* Weather */}
      <div>
        {loading ? (
          <Spinner />
        ) : weather?.main ? (
          <Weather data={weather} />
        ) : null}
      </div>
    </div>
  );
}
```

components/Weather.js:

```js
import React from "react";
import Image from "next/image";

const Weather = ({ data }) => {
  console.log(data);

  return (
    <div className="relative flex flex-col justify-between h-[80vh]  max-w-[500px] w-full m-auto pt-4 text-gray-300 z-10">
      {/* Top */}
      <div className="relative flex justify-between pt-12">
        <div className="flex flex-col items-center">
          <Image
            src={`https://openweathermap.org/img/wn/${data.weather[0].icon}@2x.png`}
            alt="icon"
            width="100"
            height="100"
          />
          <p>{data.weather[0].main}</p>
        </div>
        <p className="text-9xl">{data.main.temp.toFixed(0)}&#176;C</p>
      </div>

      {/* Bottom */}
      <div className="relative bg-black/50 p-8 rounded-md">
        <p className="text-2xl text-center pb-6">Weather in {data.name}</p>
        <div className="flex justify-between text-center">
          <div>
            <p className="font-bold text-2xl">
              {data.main.feels_like.toFixed(0)}&#176;C
            </p>
            <p className="text-xl">Feels Like</p>
          </div>
          <div>
            <p className="font-bold text-2xl">{data.main.humidity}%</p>
            <p className="text-xl">Humidity</p>
          </div>
          <div>
            <p className="font-bold text-2xl">{data.wind.speed} M/S</p>
            <p className="text-xl">Wind Speed</p>
          </div>
        </div>
      </div>
    </div>
  );
};

export default Weather;
```

components/Spinner.jsx:

```js
import React from "react";
import spinner from "../public/spinner2.svg";
import Image from "next/image";

const Spinner = () => {
  return (
    <>
      <Image
        className="relative z-10 w-[200px] m-auto block"
        src={spinner}
        alt="Loading..."
      />
    </>
  );
};

export default Spinner;
```

</details>

<details>
  <summary>27. **Get Time and Weather Data</summary>

Get Time Data:

```js
// ### Get Time data ###
axios
  .get("https://www.timeapi.io/api/Time/current/coordinate", {
    params: {
      latitude: "6.4550575",
      longitude: "3.3941795",
    },
    headers: {
      accept: "application/json",
      "Access-Control-Allow-Origin": "*",
    },
  })
  .then((response) => {
    console.log(response.data);
  })
  .catch((err) => {
    console.error(err);
  });
```

```js
const cityTimeURL = `https://www.timeapi.io/api/Time/current/coordinate?latitude=6.4550575&longitude=3.3941795`;

// ### Get Time data ###
axios({
  method: "get",
  url: cityTimeURL,
  headers: { "Access-Control-Allow-Origin": "*" },
})
  .then((response) => {
    console.log(response.data);
  })
  .catch((err) => {
    console.error(err);
  });
```

```js
const cityTimeURL = `https://www.timeapi.io/api/Time/current/coordinate?latitude=6.4550575&longitude=3.3941795`;

// ### Get Time data ###
axios
  .get(cityTimeURL, {
    withCredentials: true,
    headers: {
      "Access-Control-Allow-Origin": "*",
      "Access-Control-Allow-Credentials": true,
      "Access-Control-Allow-Methods": "GET,PUT,POST,DELETE,PATCH,OPTIONS",
    },
  })
  .then((response) => {
    console.log(response.data);
  })
  .catch((err) => {
    console.error(err);
  });
```

```js
// ### Get Time data ###
axios
  .post(cityTimeURL, {
    withCredentials: true,
    responseType: "json",
    timeout: 30000,
    headers: {
      "Access-Control-Allow-Origin": "*",
      "Access-Control-Allow-Credentials": true,
      "Access-Control-Allow-Methods": "GET,PUT,POST,DELETE,PATCH,OPTIONS",
    },
  })
  .then((response) => {
    console.log(response.data);
  })
  .catch((err) => {
    console.error(err);
  });
```

Get Weather Data:

```js
// ### Get Weather data ###
axios
  .get(weatherURL)
  .then((response) => {
    setWeather(response.data);
    setCityGeo({ lat: response.data.coord.lat, lon: response.data.coord.lon });
    console.log(cityGeo);
  })
  //.catch((err) => console.error(err))
  .catch((err) => {
    setWeather("");
    err?.response.status === 404 && setErrorMessage(err);
  });
```

Others:

```js
axios({
  method: "get",
  url: `https://api.someurl.com/subject/v2/resource/somevalue`,
  withCredentials: false,
  params: {
    access_token: SECRET_TOKEN,
  },
});
```

```bs
npm i cors

const express = require('express')
const app = express()
app.use(cors())

const cors = require('cors');
app.use(cors());

const cors = require('cors');
app.use(cors({credentials: true, origin: 'http://localhost:5003'}));

Access-Control-Allow-Origin: http://localhost:3000
Access-Control-Allow-Origin: *

headers: {"Access-Control-Allow-Origin": "*"}

app.use(
  cors({
    credentials: true,
    methods: 'GET,HEAD,PUT,PATCH,POST,DELETE,OPTIONS',
    allowedHeaders: ['Content-Type', 'Authorization'],
    origin: ['http://localhost:3000', 'http://localhost:3030'], // whatever ports you used in frontend
  })
);
```

</details>

<details>
  <summary>28. Completed Project</summary>

globals.css:

```css
@tailwind base;
@tailwind components;
@tailwind utilities;

@layer base {
  body {
    @apply bg-[url('https://images.unsplash.com/photo-1598899246709-c8273815f3ef?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1932&q=80')] bg-cover bg-center bg-fixed min-h-full min-w-full;
  }
}
```

index.js:

```js
import Head from "next/head";
import Image from "next/image";
import axios from "axios";
import { useState } from "react";
import { BsSearch } from "react-icons/bs";
import { AiOutlineClose } from "react-icons/ai";
import Weather from "../components/Weather";
import Spinner from "../components/Spinner";

export default function Home() {
  const [city, setCity] = useState("");
  const [weather, setWeather] = useState({});
  const [cityTime, setCityTime] = useState({});
  const [loading, setLoading] = useState(false);
  const [errorMessage, setErrorMessage] = useState("");
  const [cache, setCache] = useState([]);

  const fetchWeather = (e) => {
    const weatherURL = `https://api.openweathermap.org/data/2.5/weather?q=${city}&units=metric&appid=${process.env.NEXT_PUBLIC_WEATHER_KEY}`;

    const cityTimeURL = `https://timezone.abstractapi.com/v1/current_time/?api_key=${process.env.NEXT_PUBLIC_TIME_KEY}&location=${city}`;

    e.preventDefault();
    setLoading(true);
    setErrorMessage("");
    if (city) {
      // ### Get Weather data ###
      axios
        .get(weatherURL)
        .then((response) => {
          setWeather(response.data);
          setCache((prev) => [...prev, city]);
        }) //.catch((err) => console.error(err))
        .catch((err) => {
          setWeather("");
          err?.response.status === 404 && setErrorMessage(err);
        });

      // ### Get Time data ###
      axios
        .get(cityTimeURL)
        .then((response) => {
          setCityTime(response.data);
        })
        .catch((err) => {
          setCityTime("");
          console.error(err);
        });
    }
    setLoading(false);
  };

  return (
    <div className="absolute object-cover bg-black/50 z-[9] p-4 text-center max-[500px]:h-[250%] min-h-full min-w-full">
      <Head>
        <title>Weather - Next App</title>
        <meta name="description" content="Generated by create next app" />
        <link rel="icon" href="/favicon.ico" />
      </Head>

      {/* Heading */}
      <h1 className="relative flex justify-center items-center max-w-[500px] w-full m-auto pt-16 text-gray-300 text-6xl z-10">
        Open Weather App
      </h1>

      {/* Search */}
      <div className="relative flex flex-col justify-between items-center max-w-[500px] w-full m-auto pt-4 mt-8 text-white z-10">
        <form
          onSubmit={fetchWeather}
          className="flex justify-between items-center w-full m-auto p-3 bg-transparent border border-gray-300 text-white rounded-2xl"
        >
          <div>
            <input
              onChange={(e) => setCity(e.target.value)}
              className="bg-transparent border-none text-white focus:outline-none text-2xl placeholder:text-gray-400 w-[400px] pl-4"
              type="text"
              placeholder="Search city"
              value={city}
            />
          </div>
          <button type="button" className="mr-4" onClick={() => setCity("")}>
            <AiOutlineClose size={25} />
          </button>
          <button type="submit" className="mr-4">
            <BsSearch size={25} />
          </button>
        </form>
      </div>

      {/* Weather */}
      <p className="text-2xl relative flex justify-center max-w-[500px] w-full m-auto pt-4 text-gray-300 z-10">
        {errorMessage && "Sorry, no records for city."}
      </p>
      <div>
        {loading ? (
          <Spinner />
        ) : weather?.main ? (
          <Weather
            data={weather}
            datatime={cityTime}
            fetchWeather={fetchWeather}
            setCity={setCity}
            temp={cache}
          />
        ) : null}
      </div>
    </div>
  );
}
```

components/Weather.jsx:

```js
import React from "react";
import Image from "next/image";
import { FiRefreshCw } from "react-icons/fi";

const Weather = ({ data, datatime, fetchWeather, temp, setCity }) => {
  const dtime = datatime.datetime?.slice(11, 16);
  const dH = dtime?.slice(0, 2);
  const dM = dtime?.slice(3);
  const dday = datatime.datetime?.slice(8, 10);
  const dmonth = datatime.datetime?.slice(5, 7);
  const dyear = datatime.datetime?.slice(0, 4);
  const months = {
    1: "January",
    2: "February",
    3: "March",
    4: "April",
    5: "May",
    6: "June",
    7: "July",
    8: "August",
    9: "September",
    10: "October",
    11: "November",
    12: "December",
  };

  const refreshData = (e) => {
    setCity(temp[temp.length - 1]);
    fetchWeather(e);
  };

  return (
    <div className="relative flex flex-col max-w-[1280px] w-full m-auto p-4 text-gray-300 z-10">
      {/* Top */}
      <div className="flex justify-center items-center text-4xl text-gray-400 text-center pb-8">
        <p className="mr-2">Weather in {data.name}</p>
        <button onClick={(e) => refreshData(e)}>
          <FiRefreshCw />
        </button>
      </div>

      {/* Bottom */}
      <div className="relative flex flex-wrap max-[600px]:justify-center justify-between items-center">
        {/* Time */}
        <div className="bg-black/50 p-8 rounded-md w-[250px] h-[250px] mt-4 text-center">
          <p className="text-2xl font-bold  text-center">TIME</p>
          <p className="font-bold text-6xl flex justify-center items-center">
            {dH > 12 ? `${dH - 12}:${dM}` : dtime}
            <span className="text-[30px] inline">{dH < 12 ? "AM" : "PM"}</span>
          </p>
          <p className="text-xl font-bold">
            {months[dmonth]} {dday}, {dyear}
          </p>
          <p className="text-sm">
            {datatime.timezone_location} ({datatime.timezone_abbreviation})
          </p>
          <p className="text-sm">Latitude: {datatime.latitude}</p>
          <p className="text-sm">Longitude: {datatime.longitude}</p>
        </div>
        {/* Temp */}
        <div className="bg-black/50 p-8 rounded-md w-[250px] h-[250px] mt-4">
          <p className="text-2xl font-bold  text-center">TEMP</p>
          <div className="relative flex justify-between items-center">
            <div className="flex flex-col items-center mr-2">
              <Image
                src={`https://openweathermap.org/img/wn/${data.weather[0].icon}@2x.png`}
                alt="icon"
                width="100"
                height="100"
              />
              <p className="mt-[-10px] font-bold">{data.weather[0].main}</p>
            </div>
            <p className="text-5xl font-bold ">
              {data.main.temp.toFixed(0)}&#176;C
            </p>
          </div>
          <p className="text-xl mt-2 text-center">
            (Feels Like {data.main.feels_like.toFixed(0)}&#176;C)
          </p>
        </div>
        {/* Humidity */}
        <div className="bg-black/50 p-8 rounded-md w-[250px] h-[250px] mt-4 text-center">
          <p className="text-2xl font-bold text-center">HUMIDITY</p>
          <p className="font-bold text-6xl p-2">{data.main.humidity}%</p>
          <p className="text-xl">{data.weather[0].description}</p>
        </div>
        {/* Wind Speed */}
        <div className="bg-black/50 p-8 rounded-md w-[250px] h-[250px] mt-4 text-center">
          <p className="text-2xl font-bold text-center">WIND SPEED</p>
          <p className="font-bold text-4xl p-2">{data.wind.speed} M/S</p>
          <p className="text-lg">Angle: {data.wind.deg}&#176;</p>
        </div>
      </div>
    </div>
  );
};

export default Weather;
```

components/Spinner.jsx:

```js
import React from "react";
import spinner from "../public/spinner2.svg";
import Image from "next/image";

const Spinner = () => {
  return (
    <>
      <Image
        className="relative z-10 w-[200px] m-auto block"
        src={spinner}
        alt="Loading..."
      />
    </>
  );
};

export default Spinner;
```

global.css:

```css
@tailwind base;
@tailwind components;
@tailwind utilities;

@layer base {
  body {
    @apply bg-[url('https://images.unsplash.com/photo-1598899246709-c8273815f3ef?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1932&q=80')] bg-cover bg-center bg-fixed min-h-full min-w-full;
  }
}
```

</details>

### [4-FIREBASE TODO APP - CODE COMMERCE](#)

<details>
  <summary>29. Create Todo Project App</summary>

```bs
https://tailwindcss.com/docs/guides/create-react-app
```

```bs
yarn create-react-app todo-react-app

npx create-react-app todo-react-app
cd my-project
```

```bs
npm install -D tailwindcss
npx tailwindcss init
```

tailwind.config.js:

```js
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: ["./src/**/*.{js,jsx,ts,tsx}"],
  theme: {
    extend: {},
  },
  plugins: [],
};
```

Add the Tailwind directives to your CSS -

index.css:

```bs
@tailwind base;
@tailwind components;
@tailwind utilities;
```

```bs
npm run start

yarn start
```

index.js:

```js
import React from "react";
import ReactDOM from "react-dom/client";
import "./index.css";
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
function App() {
  return (
    <div className="App">
      <h1 className="text-5xl font-bold underline">Hello world!</h1>
    </div>
  );
}

export default App;
```

index.css:

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

</details>

<details>
  <summary>30. Build Todo App Visual Components</summary>

install react-icons:

```bs
npm install react-icons --save
```

App.js:

```js
import React, { useState } from "react";
import { AiOutlinePlus } from "react-icons/ai";
import Todo from "./Todo";

const style = {
  bg: `h-screen w-screen p-4 bg-gradient-to-r from-[#2F80ED] to-[#1CB5E0]`,
  container: `bg-slate-100 max-w-[500px] w-full m-auto rounded-md shadow-xl p-4`,
  heading: `text-3xl font-bold text-center text-gray-800 p-2`,
  form: `flex justify-between`,
  input: `border p-2 w-full text-xl`,
  button: `border p-4 ml-2 bg-purple-500 text-slate-100`,
  count: `text-center p-2`,
};

function App() {
  const [todos, setTodos] = useState(["Learn React", "Take out the trash"]);

  return (
    <div className={style.bg}>
      <div className={style.container}>
        <h3 className={style.heading}>Todo App</h3>
        <form className={style.form}>
          <input className={style.input} type="text" placeholder="Add Todo" />
          <button className={style.button}>
            <AiOutlinePlus size={30} />
          </button>
        </form>
        <ul>
          {todos.map((todo, index) => (
            <Todo key={index} todo={todo} />
          ))}
        </ul>
        <p className={style.count}>You have {todos.length} todos</p>
      </div>
    </div>
  );
}

export default App;
```

Todo.js:

```js
import React from "react";
import { FaRegTrashAlt } from "react-icons/fa";

const style = {
  li: `flex justify-between bg-slate-200 p-4 my-2 capitalize`,
  liComplete: `flex justify-between bg-slate-400 p-4 my-2 capitalize`,
  row: `flex`,
  text: `ml-2 cursor-pointer`,
  textComplete: `ml-2 cursor-pointer line-through`,
  button: `cursor-pointer flex items-center`,
};

const Todo = ({ todo }) => {
  return (
    <li className={style.li}>
      <div className={style.row}>
        <input type="checkbox" />
        <p className={style.text}>{todo}</p>
      </div>
      <button> {<FaRegTrashAlt />}</button>
    </li>
  );
};

export default Todo;
```

Project:

![proj1](https://user-images.githubusercontent.com/32337103/213242102-d840beb4-a781-48c7-8fed-89a7df5a292c.png)

</details>

<details>
  <summary>31. Setup Firebase Database</summary>

```bs
yarn add firebase

npm install firebase
```

console.firebase.google.com -> Add a Project -> todo-app-firebase

firebase.js:

```js
// Import the functions you need from the SDKs you need
import { initializeApp } from "firebase/app";
import { getFirestore } from "firebase/firestore";

// TODO: Add SDKs for Firebase products that you want to use
// https://firebase.google.com/docs/web/setup#available-libraries

// Your web app's Firebase configuration
const firebaseConfig = {
  apiKey: "........",
  authDomain: "........",
  projectId: "........",
  storageBucket: "........",
  messagingSenderId: "........",
  appId: "........",
};

// Initialize Firebase
const app = initializeApp(firebaseConfig);
// Initialize Cloud Firestore and get a reference to the service
export const db = getFirestore(app);
```

console.firebase.google.com -> Build -> Firestore Database -> Create Database

- A collection is a set of documents that contain data
- Example: Collection "users" would contain a unique document for each user

Start collection -> Collection ID -> "todos"

![proj2](https://user-images.githubusercontent.com/32337103/213251517-1a4cfcc0-9300-4986-81cd-44c0e3412d77.png)

![proj4](https://user-images.githubusercontent.com/32337103/213252813-55d989cf-4c27-43c2-90f2-1fb6bbbd5d1d.png)

</details>

<details>
  <summary>32. CRUD - Read Todo from Firebase</summary>

Web version 8:

```bs
db.collection("users").get().then((querySnapshot) => {
    querySnapshot.forEach((doc) => {
        console.log(`${doc.id} => ${doc.data()}`);
    });
});
```

Web version 9:

```bs
import { collection, getDocs } from "firebase/firestore";

const querySnapshot = await getDocs(collection(db, "users"));
querySnapshot.forEach((doc) => {
  console.log(`${doc.id} => ${doc.data()}`);
});
```

App.js:

```bs
  // Read todo from firebase
  useEffect(() => {
    const q = query(collection(db, "todos"));
    const unsubscribe = onSnapshot(q, (querySnapshot) => {
      let todosArr = [];
      querySnapshot.forEach((doc) => {
        todosArr.push({ ...doc.data(), id: doc.id });
      });
      setTodos(todosArr);
    });
    return () => unsubscribe();
  }, []);
```

```js
import React, { useState, useEffect } from "react";
import { AiOutlinePlus } from "react-icons/ai";
import Todo from "./Todo";
import { db } from "./firebase";
import { query, collection, onSnapshot } from "firebase/firestore";

const style = {
  bg: `h-screen w-screen p-4 bg-gradient-to-r from-[#2F80ED] to-[#1CB5E0]`,
  container: `bg-slate-100 max-w-[500px] w-full m-auto rounded-md shadow-xl p-4`,
  heading: `text-3xl font-bold text-center text-gray-800 p-2`,
  form: `flex justify-between`,
  input: `border p-2 w-full text-xl`,
  button: `border p-4 ml-2 bg-purple-500 text-slate-100`,
  count: `text-center p-2`,
};

function App() {
  const [todos, setTodos] = useState([]);

  // Create todo

  // Read todo from firebase
  useEffect(() => {
    const q = query(collection(db, "todos"));
    const unsubscribe = onSnapshot(q, (querySnapshot) => {
      let todosArr = [];
      querySnapshot.forEach((doc) => {
        todosArr.push({ ...doc.data(), id: doc.id });
      });
      setTodos(todosArr);
    });
    return () => unsubscribe();
  }, []);

  // Update todo in firebase
  // Delete todo

  return (
    <div className={style.bg}>
      <div className={style.container}>
        <h3 className={style.heading}>Todo App</h3>
        <form className={style.form}>
          <input className={style.input} type="text" placeholder="Add Todo" />
          <button className={style.button}>
            <AiOutlinePlus size={30} />
          </button>
        </form>
        <ul>
          {todos.map((todo, index) => (
            <Todo key={index} todo={todo} />
          ))}
        </ul>
        <p className={style.count}>You have {todos.length} todos</p>
      </div>
    </div>
  );
}

export default App;
```

Todo.jsx:

```bs
<p className={style.text}>{todo.task}</p>
```

```js
import React from "react";
import { FaRegTrashAlt } from "react-icons/fa";

const style = {
  li: `flex justify-between bg-slate-200 p-4 my-2 capitalize`,
  liComplete: `flex justify-between bg-slate-400 p-4 my-2 capitalize`,
  row: `flex`,
  text: `ml-2 cursor-pointer`,
  textComplete: `ml-2 cursor-pointer line-through`,
  button: `cursor-pointer flex items-center`,
};

const Todo = ({ todo }) => {
  return (
    <li className={style.li}>
      <div className={style.row}>
        <input type="checkbox" />
        <p className={style.text}>{todo.task}</p>
      </div>
      <button> {<FaRegTrashAlt />}</button>
    </li>
  );
};

export default Todo;
```

![proj5](https://user-images.githubusercontent.com/32337103/213258385-534439a7-c617-4cb2-89d9-1f4a6e712516.png)

</details>

<details>
  <summary>33. CRUD - Update state of Todo from Firebase</summary>

```bs
import {
  query,
  collection,
  onSnapshot,
  updateDoc,
  doc,
} from "firebase/firestore";

// Update todo in firebase
const toggleComplete = async (todo) => {
  await updateDoc(doc(db, "todos", todo.id), {
    completed: !todo.completed,
  });
};
```

App.js:

```js
import React, { useState, useEffect } from "react";
import { AiOutlinePlus } from "react-icons/ai";
import Todo from "./Todo";
import { db } from "./firebase";
import {
  query,
  collection,
  onSnapshot,
  updateDoc,
  doc,
} from "firebase/firestore";

const style = {
  bg: `h-screen w-screen p-4 bg-gradient-to-r from-[#2F80ED] to-[#1CB5E0]`,
  container: `bg-slate-100 max-w-[500px] w-full m-auto rounded-md shadow-xl p-4`,
  heading: `text-3xl font-bold text-center text-gray-800 p-2`,
  form: `flex justify-between`,
  input: `border p-2 w-full text-xl`,
  button: `border p-4 ml-2 bg-purple-500 text-slate-100`,
  count: `text-center p-2`,
};

function App() {
  const [todos, setTodos] = useState([]);

  // Create todo

  // Read todo from firebase
  useEffect(() => {
    const q = query(collection(db, "todos"));
    const unsubscribe = onSnapshot(q, (querySnapshot) => {
      let todosArr = [];
      querySnapshot.forEach((doc) => {
        todosArr.push({ ...doc.data(), id: doc.id });
      });
      setTodos(todosArr);
    });
    return () => unsubscribe();
  }, []);

  // Update todo in firebase
  const toggleComplete = async (todo) => {
    await updateDoc(doc(db, "todos", todo.id), {
      completed: !todo.completed,
    });
  };

  // Delete todo

  return (
    <div className={style.bg}>
      <div className={style.container}>
        <h3 className={style.heading}>Todo App</h3>
        <form className={style.form}>
          <input className={style.input} type="text" placeholder="Add Todo" />
          <button className={style.button}>
            <AiOutlinePlus size={30} />
          </button>
        </form>
        <ul>
          {todos.map((todo, index) => (
            <Todo key={index} todo={todo} toggleComplete={toggleComplete} />
          ))}
        </ul>
        <p className={style.count}>You have {todos.length} todos</p>
      </div>
    </div>
  );
}

export default App;
```

Todo.jsx:

```js
import React from "react";
import { FaRegTrashAlt } from "react-icons/fa";

const style = {
  li: `flex justify-between bg-slate-200 p-4 my-2 capitalize`,
  liComplete: `flex justify-between bg-slate-400 p-4 my-2 capitalize`,
  row: `flex`,
  text: `ml-2 cursor-pointer`,
  textComplete: `ml-2 cursor-pointer line-through`,
  button: `cursor-pointer flex items-center`,
};

const Todo = ({ todo, toggleComplete }) => {
  return (
    <li className={todo.completed ? style.liComplete : style.li}>
      <div className={style.row}>
        <input
          onChange={() => toggleComplete(todo)}
          type="checkbox"
          checked={todo.completed ? "checked" : ""}
        />
        <p
          onClick={() => toggleComplete(todo)}
          className={todo.completed ? style.textComplete : style.text}
        >
          {todo.task}
        </p>
      </div>
      <button> {<FaRegTrashAlt />}</button>
    </li>
  );
};

export default Todo;
```

![proj6](https://user-images.githubusercontent.com/32337103/213406204-9ecbdbf9-3859-4886-8c19-0045cae256ac.png)

</details>

<details>
  <summary>34. CRUD - Create/ADD Todo from Firebase</summary>

Web version 8:

```bs
db.collection("users").add({
    first: "Ada",
    last: "Lovelace",
    born: 1815
})
.then((docRef) => {
    console.log("Document written with ID: ", docRef.id);
})
.catch((error) => {
    console.error("Error adding document: ", error);
});
```

Web version 9:

```bs
import { collection, addDoc } from "firebase/firestore";

try {
  const docRef = await addDoc(collection(db, "users"), {
    first: "Ada",
    last: "Lovelace",
    born: 1815
  });
  console.log("Document written with ID: ", docRef.id);
} catch (e) {
  console.error("Error adding document: ", e);
}
```

```bs
import {
  query,
  collection,
  onSnapshot,
  updateDoc,
  doc,
  addDoc,
} from "firebase/firestore";

// Create todo
const createTodo = async (e) => {
  e.preventDefault();
  if (inputValue === "") {
    alert("Please enter a value");
    return;
  }
  await addDoc(collection(db, "todos"), {
    task: inputValue,
    completed: false,
  });
  setInputValue("");
};
```

App.js:

```js
import React, { useState, useEffect } from "react";
import { AiOutlinePlus } from "react-icons/ai";
import Todo from "./Todo";
import { db } from "./firebase";
import {
  query,
  collection,
  onSnapshot,
  updateDoc,
  doc,
  addDoc,
} from "firebase/firestore";

const style = {
  bg: `h-screen w-screen p-4 bg-gradient-to-r from-[#2F80ED] to-[#1CB5E0]`,
  container: `bg-slate-100 max-w-[500px] w-full m-auto rounded-md shadow-xl p-4`,
  heading: `text-3xl font-bold text-center text-gray-800 p-2`,
  form: `flex justify-between`,
  input: `border p-2 w-full text-xl`,
  button: `border p-4 ml-2 bg-purple-500 text-slate-100`,
  count: `text-center p-2`,
};

function App() {
  const [todos, setTodos] = useState([]);
  const [inputValue, setInputValue] = useState("");

  // Create todo
  const createTodo = async (e) => {
    e.preventDefault();
    if (inputValue === "") {
      alert("Please enter a value");
      return;
    }
    await addDoc(collection(db, "todos"), {
      task: inputValue,
      completed: false,
    });
    setInputValue("");
  };

  // Read todo from firebase
  useEffect(() => {
    const q = query(collection(db, "todos"));
    const unsubscribe = onSnapshot(q, (querySnapshot) => {
      let todosArr = [];
      querySnapshot.forEach((doc) => {
        todosArr.push({ ...doc.data(), id: doc.id });
      });
      setTodos(todosArr);
    });
    return () => unsubscribe();
  }, []);

  // Update todo in firebase
  const toggleComplete = async (todo) => {
    await updateDoc(doc(db, "todos", todo.id), {
      completed: !todo.completed,
    });
  };

  // Delete todo

  return (
    <div className={style.bg}>
      <div className={style.container}>
        <h3 className={style.heading}>Todo App</h3>
        <form onSubmit={createTodo} className={style.form}>
          <input
            value={inputValue}
            onChange={(e) => setInputValue(e.target.value)}
            className={style.input}
            type="text"
            placeholder="Add Todo"
          />
          <button className={style.button}>
            <AiOutlinePlus size={30} />
          </button>
        </form>
        <ul>
          {todos.map((todo, index) => (
            <Todo key={index} todo={todo} toggleComplete={toggleComplete} />
          ))}
        </ul>
        {todos.length < 1 ? null : (
          <p className={style.count}>You have {todos.length} todos</p>
        )}
      </div>
    </div>
  );
}

export default App;
```

Todo.jsx:

```js
import React from "react";
import { FaRegTrashAlt } from "react-icons/fa";

const style = {
  li: `flex justify-between bg-slate-200 p-4 my-2 capitalize`,
  liComplete: `flex justify-between bg-slate-400 p-4 my-2 capitalize`,
  row: `flex`,
  text: `ml-2 cursor-pointer`,
  textComplete: `ml-2 cursor-pointer line-through`,
  button: `cursor-pointer flex items-center`,
};

const Todo = ({ todo, toggleComplete }) => {
  return (
    <li className={todo.completed ? style.liComplete : style.li}>
      <div className={style.row}>
        <input
          onChange={() => toggleComplete(todo)}
          type="checkbox"
          checked={todo.completed ? "checked" : ""}
        />
        <p
          onClick={() => toggleComplete(todo)}
          className={todo.completed ? style.textComplete : style.text}
        >
          {todo.task}
        </p>
      </div>
      <button> {<FaRegTrashAlt />}</button>
    </li>
  );
};

export default Todo;
```

![proj7](https://user-images.githubusercontent.com/32337103/213413904-04aaaf61-9455-4ca1-9dca-2e7972fea8f6.png)

</details>

<details>
  <summary>35. CRUD - DELETE Todo from Firebase</summary>

```bs
import {
  query,
  collection,
  onSnapshot,
  updateDoc,
  doc,
  addDoc,
  deleteDoc,
} from "firebase/firestore";

// Delete todo
const deleteTodo = async (id) => {
  await deleteDoc(doc(db, "todos", id));
};
```

App.js:

```js
import React, { useState, useEffect } from "react";
import { AiOutlinePlus } from "react-icons/ai";
import Todo from "./Todo";
import { db } from "./firebase";
import {
  query,
  collection,
  onSnapshot,
  updateDoc,
  doc,
  addDoc,
  deleteDoc,
} from "firebase/firestore";

const style = {
  bg: `h-screen w-screen p-4 bg-gradient-to-r from-[#2F80ED] to-[#1CB5E0]`,
  container: `bg-slate-100 max-w-[500px] w-full m-auto rounded-md shadow-xl p-4`,
  heading: `text-3xl font-bold text-center text-gray-800 p-2`,
  form: `flex justify-between`,
  input: `border p-2 w-full text-xl`,
  button: `border p-4 ml-2 bg-purple-500 text-slate-100`,
  count: `text-center p-2`,
};

function App() {
  const [todos, setTodos] = useState([]);
  const [inputValue, setInputValue] = useState("");

  // Create todo
  const createTodo = async (e) => {
    e.preventDefault();
    if (inputValue === "") {
      alert("Please enter a value");
      return;
    }
    await addDoc(collection(db, "todos"), {
      task: inputValue,
      completed: false,
    });
    setInputValue("");
  };

  // Read todo from firebase
  useEffect(() => {
    const q = query(collection(db, "todos"));
    const unsubscribe = onSnapshot(q, (querySnapshot) => {
      let todosArr = [];
      querySnapshot.forEach((doc) => {
        todosArr.push({ ...doc.data(), id: doc.id });
      });
      setTodos(todosArr);
    });
    return () => unsubscribe();
  }, []);

  // Update todo in firebase
  const toggleComplete = async (todo) => {
    await updateDoc(doc(db, "todos", todo.id), {
      completed: !todo.completed,
    });
  };

  // Delete todo
  const deleteTodo = async (id) => {
    await deleteDoc(doc(db, "todos", id));
  };

  return (
    <div className={style.bg}>
      <div className={style.container}>
        <h3 className={style.heading}>Todo App</h3>
        <form onSubmit={createTodo} className={style.form}>
          <input
            value={inputValue}
            onChange={(e) => setInputValue(e.target.value)}
            className={style.input}
            type="text"
            placeholder="Add Todo"
          />
          <button className={style.button}>
            <AiOutlinePlus size={30} />
          </button>
        </form>
        <ul>
          {todos.map((todo, index) => (
            <Todo
              key={index}
              todo={todo}
              toggleComplete={toggleComplete}
              deleteTodo={deleteTodo}
            />
          ))}
        </ul>
        {todos.length < 1 ? null : (
          <p className={style.count}>You have {todos.length} todos</p>
        )}
      </div>
    </div>
  );
}

export default App;
```

Todo.jsx:

```js
import React from "react";
import { FaRegTrashAlt } from "react-icons/fa";

const style = {
  li: `flex justify-between bg-slate-200 p-4 my-2 capitalize`,
  liComplete: `flex justify-between bg-slate-400 p-4 my-2 capitalize`,
  row: `flex`,
  text: `ml-2 cursor-pointer`,
  textComplete: `ml-2 cursor-pointer line-through`,
  button: `cursor-pointer flex items-center`,
};

const Todo = ({ todo, toggleComplete, deleteTodo }) => {
  return (
    <li className={todo.completed ? style.liComplete : style.li}>
      <div className={style.row}>
        <input
          onChange={() => toggleComplete(todo)}
          type="checkbox"
          checked={todo.completed ? "checked" : ""}
        />
        <p
          onClick={() => toggleComplete(todo)}
          className={todo.completed ? style.textComplete : style.text}
        >
          {todo.task}
        </p>
      </div>
      <button onClick={() => deleteTodo(todo.id)}> {<FaRegTrashAlt />}</button>
    </li>
  );
};

export default Todo;
```

![proj8](https://user-images.githubusercontent.com/32337103/213422648-63214724-4a0d-44f9-bab9-fd09667cfdf7.png)

</details>

<details>
  <summary>36. Order and Limit data</summary>

- By default, a query retrieves all documents that satisfy the query in ascending order by document ID.
- You can specify the sort order for your data using orderBy(), and you can limit the number of documents retrieved using limit().
- Note: An orderBy() clause also filters for existence of the given field. The result set will not include documents that do not contain the given field.

For example, you could query for the first 3 cities alphabetically with:

```bs
import { query, orderBy, limit } from "firebase/firestore";

const q = query(citiesRef, orderBy("name"), limit(3));
```

```bs
citiesRef.orderBy("name").limit(3);
```

You could also sort in descending order to get the last 3 cities:

```bs
import { query, orderBy, limit } from "firebase/firestore";

const q = query(citiesRef, orderBy("name", "desc"), limit(3));
```

```bs
citiesRef.orderBy("name", "desc").limit(3);
```

- You can also order by multiple fields.

For example, if you wanted to order by state, and within each state order by population in descending order:

```bs
import { query, orderBy } from "firebase/firestore";

const q = query(citiesRef, orderBy("state"), orderBy("population", "desc"));
```

```bs
citiesRef.orderBy("state").orderBy("population", "desc");
```

- You can combine where() filters with orderBy() and limit().

In the following example, the queries define a population threshold, sort by population in ascending order, and return only the first few results that exceed the threshold:

```bs
import { query, where, orderBy, limit } from "firebase/firestore";

const q = query(citiesRef, where("population", ">", 100000), orderBy("population"), limit(2));
```

```bs
citiesRef.where("population", ">", 100000).orderBy("population").limit(2);
```

Limitations:

- An orderBy() clause also filters for existence of the given fields. The result set will not include documents that do not contain the given fields.

- If you include a filter with a range comparison (<, <=, >, >=), your first ordering must be on the same field.

- You cannot order your query by any field included in an equality (=) or in clause.

```bs
import { query, where, orderBy } from "firebase/firestore";

const q = query(citiesRef, where("population", ">", 100000), orderBy("population"));
```

```bs
citiesRef.where("population", ">", 100000).orderBy("population");
```

</details>

<details>
  <summary>37. Completed Project</summary>

Install Prop-types:

```bs
npm install prop-types
```

config/firebase.js:

```js
// Import the functions you need from the SDKs you need
import { initializeApp } from "firebase/app";
import { getFirestore } from "firebase/firestore";

// TODO: Add SDKs for Firebase products that you want to use
// https://firebase.google.com/docs/web/setup#available-libraries

// Your web app's Firebase configuration
const firebaseConfig = {
  apiKey: process.env.REACT_APP_APIKEY,
  authDomain: process.env.REACT_APP_AUTHDOMAIN,
  projectId: process.env.REACT_APP_PROJECT_ID,
  storageBucket: process.env.REACT_APP_STORAGE_BUCKET,
  messagingSenderId: process.env.REACT_APP_MESSAGING_SENDER_ID,
  appId: process.env.REACT_APP_APPID,
};

// Initialize Firebase
const app = initializeApp(firebaseConfig);
// Initialize Cloud Firestore and get a reference to the service
export const db = getFirestore(app);
```

context/AppContext.js:

```js
//import React dependencies
import { useState, useEffect, createContext } from "react";

//import Firebase dependencies
import {
  query,
  collection,
  onSnapshot,
  updateDoc,
  doc,
  addDoc,
  deleteDoc,
} from "firebase/firestore";

//import Firebase configuration
import { db } from "../config/firebase";

//import Firebase CRUD Hooks (Actions)
import createTodoAction from "../hooks/createTodoAction";
import readTodoAction from "../hooks/readTodoAction";
import updateTodoAction from "../hooks/updateTodoAction";
import deleteTodoAction from "../hooks/deleteTodoAction";
import readTodoLocalAction from "../hooks/readTodoLocalAction";
import createTodoLocalAction from "../hooks/createTodoLocalAction";
import updateTodoLocalAction from "../hooks/updateTodoLocalAction";
import deleteTodoLocalAction from "../hooks/deleteTodoLocalAction";

//Tailwindcss (for styling)
const style = {
  bg: `h-screen w-screen p-4 bg-gradient-to-r from-[#6a85b6] to-[#80d0c7]`,
  bgDark: `h-screen w-screen p-4 bg-[#000000]`,
  container: `bg-slate-100 max-w-[500px] w-full m-auto rounded-md shadow-xl p-4`,
  containerDark: `bg-[#353a49] max-w-[500px] w-full m-auto rounded-md shadow-xl p-4`,
  heading: `text-3xl font-bold text-center text-gray-800 p-2`,
  headingDark: `text-3xl font-bold text-center text-gray-100 p-2`,
  form: `flex justify-between`,
  input: `border p-2 w-full text-xl`,
  button: `border p-4 ml-2 bg-[#6a85b6] text-slate-100`,
  buttonDark: `border p-4 ml-2 bg-[#555d75] text-slate-100`,
  count: `text-center p-2`,
  countDark: `text-center p-2 text-white`,
  nav: `flex flex-row items-center justify-end child:ml-4`,
  navDark: `flex flex-row items-center justify-end child:ml-4 bg-gray-300 mb-2`,
  navSection: `flex flex-row items-center child:mx-1`,
  hr: `w-full h-1 bg-gray-200 border-0 rounded`,
  hrDark: `w-full h-1 bg-gray-500 border-0 rounded dark:bg-gray-500`,
};

//Create App Context API
const AppContext = createContext({});

//Create App Parent Provider to store context
export const AppProvider = ({ children }) => {
  const [darkMode, setDarkMode] = useState(false);
  const [isLocal, setIsLocal] = useState(false);
  const [todos, setTodos] = useState([]);
  const [inputValue, setInputValue] = useState("");

  // Create todo in firebase
  const createTodo = (e) => {
    isLocal
      ? createTodoLocalAction(e, todos, setTodos, inputValue, setInputValue)
      : createTodoAction(e, inputValue, setInputValue, addDoc, collection, db);
  };

  // Read todo from firebase
  useEffect(() => {
    isLocal
      ? readTodoLocalAction(setTodos)
      : readTodoAction(setTodos, query, collection, db, onSnapshot);
  }, [isLocal]);

  // Update todo in firebase
  const toggleComplete = (todo) => {
    isLocal
      ? updateTodoLocalAction(todo, todos, setTodos)
      : updateTodoAction(todo, updateDoc, doc, db);
  };

  // Delete todo in firebase
  const deleteTodo = (id) => {
    isLocal
      ? deleteTodoLocalAction(id, todos, setTodos)
      : deleteTodoAction(id, deleteDoc, doc, db);
  };

  return (
    <AppContext.Provider
      value={{
        style,
        darkMode,
        setDarkMode,
        isLocal,
        setIsLocal,
        todos,
        setTodos,
        inputValue,
        setInputValue,
        createTodo,
        toggleComplete,
        deleteTodo,
      }}
    >
      {children}
    </AppContext.Provider>
  );
};

export default AppContext;
```

App.js:

```js
import { AppProvider } from "./context/AppContext";
import Home from "./components/Home";

//App
function App() {
  return (
    <AppProvider>
      <Home />
    </AppProvider>
  );
}

export default App;
```

components/Home.jsx:

```js
import React, { useContext } from "react";
import Header from "./Header";
import AddTodo from "./AddTodo";
import ListTodo from "./ListTodo";
import Footer from "./Footer";
import Nav from "./Nav";

import AppContext from "../context/AppContext";

//Home component
const Home = () => {
  const { style, darkMode } = useContext(AppContext);
  return (
    <React.Fragment>
      <div className={darkMode ? style.bgDark : style.bg}>
        <div className={darkMode ? style.containerDark : style.container}>
          <Header />
          <Nav />
          <AddTodo />
          <ListTodo />
          <Footer />
        </div>
      </div>
    </React.Fragment>
  );
};

export default Home;
```

components/Header.jsx:

```js
import { useContext } from "react";
import AppContext from "../context/AppContext";

const Header = () => {
  const { style, darkMode } = useContext(AppContext);
  return (
    <header>
      <h3 className={darkMode ? style.headingDark : style.heading}>
        Firebase Todo App
      </h3>
      <hr className={darkMode ? style.hrDark : style.hr} />
    </header>
  );
};

export default Header;
```

components/Nav.jsx:

```js
import { useContext } from "react";
import { SelectMode, SelectStorage } from "./molecules";
import AppContext from "../context/AppContext";

const Nav = () => {
  const { style, darkMode } = useContext(AppContext);
  return (
    <nav className={darkMode ? style.navDark : style.nav}>
      <SelectStorage />
      <SelectMode />
    </nav>
  );
};

export default Nav;
```

components/AddTodo.jsx:

```js
import { useContext } from "react";
import { AiOutlinePlus } from "react-icons/ai";
import AppContext from "../context/AppContext";

const AddTodo = () => {
  const { style, darkMode, createTodo, inputValue, setInputValue } =
    useContext(AppContext);
  return (
    <form onSubmit={createTodo} className={style.form}>
      <input
        value={inputValue}
        onChange={(e) => setInputValue(e.target.value)}
        className={style.input}
        type="text"
        placeholder="Add Todo"
      />
      <button className={darkMode ? style.buttonDark : style.button}>
        <AiOutlinePlus size={30} />
      </button>
    </form>
  );
};

export default AddTodo;
```

components/ListTodo.jsx:

```js
import { useContext } from "react";
import Todo from "./Todo";
import AppContext from "../context/AppContext";

const ListTodo = () => {
  const { todos } = useContext(AppContext);
  return (
    <ul>
      {todos.map((todo, index) => (
        <Todo key={index} todo={todo} />
      ))}
    </ul>
  );
};

export default ListTodo;
```

components/Todo.jsx:

```js
import { useContext } from "react";
import { FaRegTrashAlt } from "react-icons/fa";
import AppContext from "../context/AppContext";

const style = {
  li: `flex justify-between bg-slate-200 p-4 my-2 capitalize`,
  liComplete: `flex justify-between bg-[#80d0c7] p-4 my-2 capitalize`,
  liCompleteDark: `flex justify-between bg-[#373c4b] p-4 my-2 capitalize border-2 border-slate-300 rounded-lg`,
  row: `flex`,
  text: `ml-2 cursor-pointer`,
  textComplete: `ml-2 cursor-pointer line-through`,
  textCompleteDark: `ml-2 cursor-pointer line-through text-slate-200`,
  button: `cursor-pointer flex items-center`,
};

const Todo = ({ todo }) => {
  const { darkMode, toggleComplete, deleteTodo } = useContext(AppContext);
  return (
    <li
      className={
        todo.completed && darkMode
          ? style.liCompleteDark
          : todo.completed
          ? style.liComplete
          : style.li
      }
    >
      <div className={style.row}>
        <input
          onChange={() => toggleComplete(todo)}
          type="checkbox"
          checked={todo.completed ? "checked" : ""}
        />
        <p
          onClick={() => toggleComplete(todo)}
          className={
            todo.completed && darkMode
              ? style.textCompleteDark
              : todo.completed
              ? style.textComplete
              : style.text
          }
        >
          {todo.task}
        </p>
      </div>
      <button onClick={() => deleteTodo(todo.id)}> {<FaRegTrashAlt />}</button>
    </li>
  );
};

export default Todo;
```

components/Footer.jsx:

```js
import { useContext } from "react";
import AppContext from "../context/AppContext";

const Footer = () => {
  const { style, darkMode, todos } = useContext(AppContext);
  return todos.length < 1 ? null : (
    <footer>
      <p className={darkMode ? style.countDark : style.count}>
        You have {todos.length} todos
      </p>
    </footer>
  );
};

export default Footer;
```

Atoms -

components/atoms/index.js:

```js
// export { ReactComponent as ButtonOneOn } from "./ButtonOneOn.svg";
export { Button } from "./Button";
export { ToggleMoon } from "./ToggleMoon";
export { ToggleSun } from "./ToggleSun";
export { ToggleCloud } from "./ToggleCloud";
export { ToggleLocal } from "./ToggleLocal";
```

components/atoms/Button.jsx:

```js
import React from "react";
import PropTypes from "prop-types";

export const Button = ({ height, width, colorON, colorOFF, toggle }) => {
  let btnTransform = "scale(1 1)";
  let color = colorON;
  if (!["ON", "on"].includes(toggle)) {
    btnTransform = "scale(-1 1)";
    color = colorOFF;
  }

  return (
    <svg
      stroke={color}
      fill={color}
      transform={btnTransform}
      strokeWidth="0"
      viewBox="0 0 512 512"
      height={height}
      width={width}
      xmlns="http://www.w3.org/2000/svg"
    >
      <path d="M368 112H144C64.6 112 0 176.6 0 256s64.6 144 144 144h224c79.4 0 144-64.6 144-144s-64.6-144-144-144zm0 256a112 112 0 11112-112 112.12 112.12 0 01-112 112z"></path>
    </svg>
  );
};

Button.propTypes = {
  height: PropTypes.string.isRequired,
  width: PropTypes.string.isRequired,
  colorON: PropTypes.string.isRequired,
  colorOFF: PropTypes.string.isRequired,
  toggle: PropTypes.string.isRequired,
};
```

components/atoms/ToggleCloud.jsx:

```js
import React from "react";
import PropTypes from "prop-types";

export const ToggleCloud = ({ size }) => {
  return (
    <svg
      stroke="#000"
      fill="#000"
      strokeWidth="0"
      viewBox="0 0 16 16"
      height={size}
      width={size}
      xmlns="http://www.w3.org/2000/svg"
    >
      <path
        fillRule="evenodd"
        d="M4.406 1.342A5.53 5.53 0 0 1 8 0c2.69 0 4.923 2 5.166 4.579C14.758 4.804 16 6.137 16 7.773 16 9.569 14.502 11 12.687 11H10a.5.5 0 0 1 0-1h2.688C13.979 10 15 8.988 15 7.773c0-1.216-1.02-2.228-2.313-2.228h-.5v-.5C12.188 2.825 10.328 1 8 1a4.53 4.53 0 0 0-2.941 1.1c-.757.652-1.153 1.438-1.153 2.055v.448l-.445.049C2.064 4.805 1 5.952 1 7.318 1 8.785 2.23 10 3.781 10H6a.5.5 0 0 1 0 1H3.781C1.708 11 0 9.366 0 7.318c0-1.763 1.266-3.223 2.942-3.593.143-.863.698-1.723 1.464-2.383z"
      ></path>
      <path
        fillRule="evenodd"
        d="M7.646 4.146a.5.5 0 0 1 .708 0l3 3a.5.5 0 0 1-.708.708L8.5 5.707V14.5a.5.5 0 0 1-1 0V5.707L5.354 7.854a.5.5 0 1 1-.708-.708l3-3z"
      ></path>
    </svg>
  );
};

ToggleCloud.propTypes = {
  size: PropTypes.string.isRequired,
};
```

components/atoms/ToggleLocal.jsx:

```js
import React from "react";
import PropTypes from "prop-types";

export const ToggleLocal = ({ size }) => {
  return (
    <svg
      stroke="#000"
      fill="#000"
      strokeWidth="0"
      viewBox="0 0 24 24"
      height={size}
      width={size}
      xmlns="http://www.w3.org/2000/svg"
    >
      <path fill="none" d="M0 0h24v24H0V0z"></path>
      <path d="M20 18c1.1 0 1.99-.9 1.99-2L22 6c0-1.1-.9-2-2-2H4c-1.1 0-2 .9-2 2v10c0 1.1.9 2 2 2H0v2h24v-2h-4zM4 6h16v10H4V6z"></path>
    </svg>
  );
};

ToggleLocal.propTypes = {
  size: PropTypes.string.isRequired,
};
```

components/atoms/ToggleMoon.jsx:

```js
import React from "react";
import PropTypes from "prop-types";

export const ToggleMoon = ({ size, color }) => {
  return (
    <svg
      stroke={color}
      fill={color}
      strokeWidth="0"
      viewBox="0 0 512 512"
      height={size}
      width={size}
      xmlns="http://www.w3.org/2000/svg"
    >
      <path d="M283.211 512c78.962 0 151.079-35.925 198.857-94.792 7.068-8.708-.639-21.43-11.562-19.35-124.203 23.654-238.262-71.576-238.262-196.954 0-72.222 38.662-138.635 101.498-174.394 9.686-5.512 7.25-20.197-3.756-22.23A258.156 258.156 0 0 0 283.211 0c-141.309 0-256 114.511-256 256 0 141.309 114.511 256 256 256z"></path>
    </svg>
  );
};

ToggleMoon.propTypes = {
  size: PropTypes.string.isRequired,
  color: PropTypes.string.isRequired,
};
```

components/atoms/ToggleSun.jsx:

```js
import React from "react";
import PropTypes from "prop-types";

export const ToggleSun = ({ size, color }) => {
  return (
    <svg
      stroke={color}
      fill={color}
      strokeWidth="0"
      viewBox="0 0 16 16"
      height={size}
      width={size}
      xmlns="http://www.w3.org/2000/svg"
    >
      <path d="M8 12a4 4 0 1 0 0-8 4 4 0 0 0 0 8zM8 0a.5.5 0 0 1 .5.5v2a.5.5 0 0 1-1 0v-2A.5.5 0 0 1 8 0zm0 13a.5.5 0 0 1 .5.5v2a.5.5 0 0 1-1 0v-2A.5.5 0 0 1 8 13zm8-5a.5.5 0 0 1-.5.5h-2a.5.5 0 0 1 0-1h2a.5.5 0 0 1 .5.5zM3 8a.5.5 0 0 1-.5.5h-2a.5.5 0 0 1 0-1h2A.5.5 0 0 1 3 8zm10.657-5.657a.5.5 0 0 1 0 .707l-1.414 1.415a.5.5 0 1 1-.707-.708l1.414-1.414a.5.5 0 0 1 .707 0zm-9.193 9.193a.5.5 0 0 1 0 .707L3.05 13.657a.5.5 0 0 1-.707-.707l1.414-1.414a.5.5 0 0 1 .707 0zm9.193 2.121a.5.5 0 0 1-.707 0l-1.414-1.414a.5.5 0 0 1 .707-.707l1.414 1.414a.5.5 0 0 1 0 .707zM4.464 4.465a.5.5 0 0 1-.707 0L2.343 3.05a.5.5 0 1 1 .707-.707l1.414 1.414a.5.5 0 0 1 0 .708z"></path>
    </svg>
  );
};

ToggleSun.propTypes = {
  size: PropTypes.string.isRequired,
  color: PropTypes.string.isRequired,
};
```

Molecules -

components/molecules/index.js:

```js
export { SelectStorage } from "./SelectStorage";
export { SelectMode } from "./SelectMode";
```

components/molecules/SelectMode.jsx:

```js
import { useContext } from "react";
import { Button, ToggleMoon, ToggleSun } from "../atoms";
import AppContext from "../../context/AppContext";

export const SelectMode = () => {
  const { style, darkMode, setDarkMode } = useContext(AppContext);

  return (
    <section className={style.navSection}>
      <ToggleSun size="1.5em" color="black" />
      <button onClick={() => setDarkMode(!darkMode)}>
        <Button
          height="3em"
          width="3em"
          colorON="#6a85b6"
          colorOFF="gray"
          toggle={darkMode ? "ON" : "OFF"}
        />
      </button>
      <ToggleMoon size="1.5em" color="black" />
    </section>
  );
};
```

components/molecules/SelectStorage.jsx:

```js
import { useContext } from "react";
import { Button, ToggleCloud, ToggleLocal } from "../atoms";
import AppContext from "../../context/AppContext";

export const SelectStorage = () => {
  const { style, isLocal, setIsLocal } = useContext(AppContext);
  return (
    <section className={style.navSection}>
      <ToggleLocal size="1.5em" />
      <button onClick={() => setIsLocal(!isLocal)}>
        <Button
          height="3em"
          width="3em"
          colorON="#48bbae"
          colorOFF="#d65d6d"
          toggle={isLocal ? "OFF" : "ON"}
        />
      </button>
      <ToggleCloud size="1.5em" />
    </section>
  );
};
```

Hooks -

Remote -

hooks/createTodoAction.js:

```js
const createTodoAction = async (
  e,
  inputValue,
  setInputValue,
  addDoc,
  collection,
  db
) => {
  e.preventDefault();
  if (inputValue === "") {
    alert("Please enter a value");
    return;
  }
  await addDoc(collection(db, "todos"), {
    task: inputValue,
    completed: false,
  });
  setInputValue("");
};

export default createTodoAction;
```

hooks/readTodoAction.js:

```js
const readTodoAction = async (setTodos, query, collection, db, onSnapshot) => {
  const q = await query(collection(db, "todos"));
  const unsubscribe = await onSnapshot(q, (querySnapshot) => {
    let todosArr = [];
    querySnapshot.forEach((doc) => {
      todosArr.push({ ...doc.data(), id: doc.id });
    });
    setTodos(todosArr);
  });
  return () => unsubscribe();
};

export default readTodoAction;
```

hooks/updateTodoAction.js:

```js
const updateTodoAction = async (todo, updateDoc, doc, db) => {
  await updateDoc(doc(db, "todos", todo.id), {
    completed: !todo.completed,
  });
};

export default updateTodoAction;
```

hooks/deleteTodoAction.js:

```js
const deleteTodoAction = async (id, deleteDoc, doc, db) => {
  await deleteDoc(doc(db, "todos", id));
};

export default deleteTodoAction;
```

Local -

hooks/createTodoLocalAction.js:

```js
const createTodoLocalAction = (
  e,
  todos,
  setTodos,
  inputValue,
  setInputValue
) => {
  e.preventDefault();
  if (inputValue === "") {
    alert("Please enter a value");
    return;
  }

  const newTodoId = todos.length < 1 ? 1 : todos[todos.length - 1].id + 1;
  const newTodo = {
    id: newTodoId,
    completed: false,
    task: inputValue,
  };
  const newTodos = [...todos, newTodo];
  const sortedTodos = newTodos.sort((a, b) => a.id - b.id);
  setTodos(sortedTodos);
  localStorage.setItem("todos", JSON.stringify(sortedTodos));
  setInputValue("");
};

export default createTodoLocalAction;
```

hooks/readTodoLocalAction.js:

```js
const readTodoLocalAction = (setTodos) => {
  const localData = JSON.parse(localStorage.getItem("todos"));
  localData ? setTodos(localData) : setTodos([]);
};

export default readTodoLocalAction;
```

hooks/updateTodoLocalAction.js:

```js
const updateTodoLocalAction = (todo, todos, setTodos) => {
  const todoId = todo.id;
  const unalteredTodos = todos.filter((todo) => todo.id !== todoId);
  const newTodos = [
    ...unalteredTodos,
    {
      id: todoId,
      completed: !todo.completed,
      task: todo.task,
    },
  ];
  const sortedTodos = newTodos.sort((a, b) => a.id - b.id);
  setTodos(sortedTodos);
  localStorage.setItem("todos", JSON.stringify(sortedTodos));
};

export default updateTodoLocalAction;
```

hooks/deleteTodoLocalAction.js:

```js
const deleteTodoLocalAction = (id, todos, setTodos) => {
  const unalteredTodos = todos.filter((todo) => todo.id !== id);
  const sortedTodos = unalteredTodos.sort((a, b) => a.id - b.id);
  setTodos(sortedTodos);
  localStorage.setItem("todos", JSON.stringify(sortedTodos));
};

export default deleteTodoLocalAction;
```

tailwind.config.js:

```js
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: ["./src/**/*.{js,jsx,ts,tsx}"],
  theme: {
    extend: {},
  },
  plugins: [
    function ({ addVariant }) {
      addVariant("child", "& > *");
      addVariant("child-hover", "& > *:hover");
    },
  ],
};
```

package.json:

```js
{
  "name": "todo-react-app",
  "version": "0.1.0",
  "private": true,
  "dependencies": {
    "@testing-library/jest-dom": "^5.16.5",
    "@testing-library/react": "^13.4.0",
    "@testing-library/user-event": "^13.5.0",
    "firebase": "^9.15.0",
    "prop-types": "^15.8.1",
    "react": "^18.2.0",
    "react-dom": "^18.2.0",
    "react-icons": "^4.7.1",
    "react-scripts": "5.0.1",
    "web-vitals": "^2.1.4"
  },
  "scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "test": "react-scripts test",
    "eject": "react-scripts eject"
  },
  "eslintConfig": {
    "extends": [
      "react-app",
      "react-app/jest"
    ]
  },
  "browserslist": {
    "production": [
      ">0.2%",
      "not dead",
      "not op_mini all"
    ],
    "development": [
      "last 1 chrome version",
      "last 1 firefox version",
      "last 1 safari version"
    ]
  },
  "devDependencies": {
    "tailwindcss": "^3.2.4"
  }
}
```

.gitignore:

```bs
# See https://help.github.com/articles/ignoring-files/ for more about ignoring files.

# dependencies
/node_modules
/.pnp
.pnp.js

# testing
/coverage

# production
/build

# misc
.DS_Store
.env.local
.env.development.local
.env.test.local
.env.production.local

npm-debug.log*
yarn-debug.log*
yarn-error.log*
```

```bs
# Created by https://www.toptal.com/developers/gitignore/api/react
# Edit at https://www.toptal.com/developers/gitignore?templates=react

### react ###
.DS_*
*.log
logs
**/*.backup.*
**/*.back.*

node_modules
bower_components

*.sublime*

psd
thumb
sketch

# End of https://www.toptal.com/developers/gitignore/api/react
```

</details>

<details>
  <summary>38. **TailwindCSS direct children Config</summary>

If you want to access the direct children of div with selector, please use @layer directive. see below:

```bs
@tailwind base;
@tailwind components;
@tailwind utilities;

@layer base {
  div.section > div {
    @apply text-xl;
  }
}
```

I use these simple lines in tailwind.config.js to give me child and child-hover options.

```bs
plugins: [
    function ({ addVariant }) {
        addVariant('child', '& > *');
        addVariant('child-hover', '& > *:hover');
    }
],
```

```js
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: ["./src/**/*.{js,jsx,ts,tsx}"],
  theme: {
    extend: {},
  },
  plugins: [
    function ({ addVariant }) {
      addVariant("child", "& > *");
      addVariant("child-hover", "& > *:hover");
    },
  ],
};
```

```bs
<div class="child:text-gray-200 child-hover:text-blue-500">...</div>
```

</details>

### [5-FIREBASE NETFLIX APP - CODE COMMERCE](#)

<details>
  <summary>39. sample</summary>

```bs

```

```js

```

```js

```

```js

```

```js

```

</details>

<details>
  <summary>40. sample</summary>

```bs

```

```bs

```

```js

```

```js

```

```js

```

```js

```

</details>

<details>
  <summary>41. sample</summary>

```bs

```

```bs

```

```js

```

```js

```

```js

```

```js

```

</details>

<details>
  <summary>42. sample</summary>

```bs

```

```bs

```

```js

```

```js

```

```js

```

```js

```

</details>

<details>
  <summary>43. sample</summary>

```bs

```

```bs

```

```js

```

```js

```

```js

```

```js

```

</details>

<details>
  <summary>44. sample</summary>

```bs

```

```bs

```

```js

```

```js

```

```js

```

```js

```

</details>

<details>
  <summary>45. sample</summary>

```bs

```

```bs

```

```js

```

```js

```

```js

```

```js

```

</details>

<details>
  <summary>46. sample</summary>

```bs

```

```bs

```

```js

```

```js

```

```js

```

```js

```

</details>

<details>
  <summary>47. sample</summary>

```bs

```

```bs

```

```js

```

```js

```

```js

```

```js

```

</details>

<details>
  <summary>48. sample</summary>

```bs

```

```bs

```

```js

```

```js

```

```js

```

```js

```

</details>

<details>
  <summary>49. sample</summary>

```bs

```

```bs

```

```js

```

```js

```

```js

```

```js

```

</details>

<details>
  <summary>50. sample</summary>

```bs

```

```bs

```

```js

```

```js

```

```js

```

```js

```

</details>
