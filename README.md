# Using React without NodeJS

## Steps
### Download libraries (if not using CDN)
Mainly, `react`, `react-dom` and `babel-standalone`.

### Example codes (with context hook)
`index.html` file:
```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title> React without NodeJS </title>

  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link
    href="https://fonts.googleapis.com/css2?family=Lora:ital,wght@0,400;0,500;0,600;0,700;1,400;1,500;1,600;1,700&display=swap"
    rel="stylesheet">
    
  <!-- Import the React, React-Dom and Babel libraries from unpkg -->
  <script type="application/javascript" src="/lib/react.production.min.js"></script>
  <script type="application/javascript" src="/lib/react-dom.production.min.js"></script>
  <script type="application/javascript" src="/lib/babel.min.js"></script>

  <link rel="stylesheet" href="/src/style/main.css">
</head>

<body>
  <main id="root"></main>

  <script type="text/babel" src="/src/code/main.js"> </script>
</body>

</html>
```

`/src/code/main.js` file:
```js
const ThemeContext = React.createContext("light");

function ButtonNew(props) {
    const theme = React.useContext(ThemeContext);
    const handleTheme = function(e) {
        console.log(e);
        theme.toggleTheme();
    };
    return (
        <button className={`btn-custom ${theme.currentTheme}`} type="button" onClick={handleTheme}> Theme: {theme.currentTheme} </button>
    );
}

function Article() {
    const theme = React.useContext(ThemeContext);
    return (<article className={`article-custom ${theme.currentTheme}`}> 
        <h3> Random article title</h3>
        <p> Some random artivle content.</p>
    </article>);
}

function ArticleGrid() {
    const theme = React.useContext(ThemeContext);
    return (<section className={`article-grid-container ${theme.currentTheme}`}> 
        <h2 className="heading"> Article list</h2>
        <div className="article-grid">
        <Article />
        <Article />
        <Article />
        <Article />
        </div>
    </section>);
}

function App(props) {
    const [currentTheme, setTheme] = React.useState("dark");

    function toggleTheme() {
        setTheme(theme => (theme === "light" ? "dark" : "light"));
    }
    return (<ThemeContext.Provider value={{currentTheme, toggleTheme}}>
        <div className={`main-app ${currentTheme}`}>
            <ButtonNew />
            <ArticleGrid />
        </div>
    </ThemeContext.Provider>);
}

const rootElement = document.getElementById('root');

ReactDOM.render(
    <App />,
    rootElement
)
```
