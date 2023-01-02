# Create react app

```sh
npx create-react-app frontend
```

# Set up git repository

# 7 List Products

- create file data products
- map data and display products
- add css (products, product, ...)

# 8 Add Routing

```sh
npm i react-router-dom
```

- add browser routing, routes, route
- create HomeScreen and ProductScreen
- change a href to Link to

# 9 Create Node.Js server

- create backend folder (root folder)
- run command

```sh
npm init
```

- add "type":"module" in package.json in backend folder

```sh
npm install express
```

- create server.js file and run it

```sh
node server.js
```

- user nodemon for dev (auto run)

```sh
npm install nodemon --save-dev
```

- in package.json script, write

```sh
"start":"nodemon server.js",
```

# 10 Fetch Products from backend

- in package.json of front end, add "proxy":"http://localhost:5000"
- in front end, run command

```sh
npm install axios
```

- HomeScreen.js apply axios

```js
const [products, setProducts] = useState([]);
useEffect(() => {
  const fetchData = async () => {
    const result = await axios.get('/api/products');
    setProducts(result.data);
  };
  fetchData();
}, []);
```

# 11 Manage State by Reducer

- set useReducer

```js
const reducer = (state, action) => {
  switch (action.type) {
    case 'FETCH_REQUEST':
      return { ...state, loading: true };
    case 'FETCH_SUCCESS':
      return { ...state, products: action.payload, loading: false };
    case 'FETCH_FAIL':
      return { ...state, loading: false, error: action.payload };
    default:
      return state;
  }
};

function HomeScreen() {
  const [{ loading, error, products }, dispatch] = useReducer(reducer, {
    products: [],
    loading: true,
    error: '',
  });
  // const [products, setProducts] = useState([]);
  useEffect(() => {
    const fetchData = async () => {
      dispatch({ type: 'FETCH_REQUEST' });
      try {
        const result = await axios.get('/api/products');
        dispatch({ type: 'FETCH_SUCCESS', payload: result.data });
      } catch (err) {
        dispatch({ type: 'FETCH_FAIL', payload: err.message });
      }
      // setProducts(result.data);
    };
    fetchData();
  }, []);
```

```js
  return (
    <div>
      <h1>Featured Products</h1>
      <div className="products">
        {loading ? (
          <div>Loading...</div>
        ) : error ? (
          <div>{error}</div>
        ) : (
          products.map((product) => (
```

# 12 Add bootstrap

```sh
npm install bootstrap
```

```sh
npm install react-bootstrap --force
```

```sh
npm install react-router-bootstrap --force
```

# 13 Create Product Component

- create product component
- create Rating component
