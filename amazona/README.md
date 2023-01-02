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

# 14 Add Product Screen

- display picture on Col md-6, info on Col md-3, and status on Col md-3
- install helmet on front end to display product name on title when move to product detail screen

```sh
npm install react-helmet-async
```

# 15 Create Loading and Message Component

- create utils file to handle error from server
- create LoadingBox used Spinner from bootstrap
- crate MessageBox used Alert from bootstrap

# 16 (Super important) Create React Context for Card screen

- add nav cart to App.js
- create Store.js (App context) export Store and export function StoreProvider
- add useReducer to Cart

# 17 (Super important) Complete add to cart functionality

- fix logic in StoreProvider
