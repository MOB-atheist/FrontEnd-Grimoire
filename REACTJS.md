
[Go Back](README.md)

# React.js

## usefull links

[React cheat sheet](http://www.developer-cheatsheets.com/react)

[Redux cheat sheet](http://www.developer-cheatsheets.com/redux)

[React Router cheat sheet](http://www.developer-cheatsheets.com/react-router)

### useState

```jsx
    function App(){
        const [count, setCount] = useState(0)
    
        useEffect(() => {

        }, [])
        // [] specifies useEffect to watch none, so it only runs once
    }
```

```jsx
    function App(){
        const [count, setCount] = useState(0)
        const [loaded, setLoaded] = useState(false)
    
        useEffect(() => {
            fetch("foo").then(() => setLoaded(true))
        }, [count])
        // [count] ony watch count changes
    }
```


```jsx
    function App(){
        const [count, setCount] = useState(0)
    
        useEffect(() => {
            return () => console.log("component unmount")
        })
        //  funcion returned on useEffect will rin when component is destroyed
    }
```

### useContext

```jsx
    const moods = {
        happy: ":)",
        sad: ":("
    }

    const MoodContext = createContext(moods)

    function App(){
        return(
            <MoodContext.Provider>
                <MoodEmoji />
            </MoodCOntext.Provider>
        )
    }

    function MoodEmoji(){
        const mood = useContext(MoodContext)
        return <p>{mood}</p>
    }
```

```jsx
    const moods = {
        happy: ":)",
        sad: ":("
    }

    const MoodContext = createContext(moods)

    function App(){
        return(
            <MoodContext.Consumer>
                { ({mood}) => <p>{mood}</p> }
            </MoodCOntext.Consumer>
        )
    }
```

### useRef

```jsx
    function App(){
        const myBtn = useRef(null)

        const clickIt = () => myBtn.current.click()

        return (
            <button ref={myBtn}>Click Me</button>
        )
    }

```

### useReducer

```jsx

    function reducer(state, action){
        switch(action.type){
            case 'increment' : 
                return {count: state + 1};
            case 'decrement' : 
                return {count: state - 1};
            default: 
                throw new Error();
        }
    }

    function App(){
        const [state, dispatch] = useReducer()

        return (
            <>
                Count: {state}
                <button onCLick={() => dispatch({type: 'decrement'})}>-</button>
                <button onCLick={() => dispatch({type: 'increment'})}>+</button>
            </>
        )
    }

```

### useMemo

```jsx
// MEMORIZE FUNCTION RESULT
    function App(){
        const [count, setCount] = useState(60)

        const expensiveCount = useMemo(() => {
            return count ** 2
        }, [count])
        // [count] only recompute if count changes

        return (
            <>
                
            </>
        )
    }

```

### useCallback

```jsx
// MEMORIZE FUNCTION
    function App(){
        const [count, setCount] = useState(60)

        const showCount = useCallback(() => {
            alert(`count ${count}`)
        }, [count])

        return (
            <>
                <SomeCHild handler={showCount} />
            </>
        )
    }

```