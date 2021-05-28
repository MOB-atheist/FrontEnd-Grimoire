# learning

Things i learn daily, so i can remember

# Javascript

### if shorthands

```javascript
    const trueValue = true
    const falseValue = true

    console.log(trueValue ? "its true": "its false")
    // returns its true or its false

    console.log(trueValue && "its true")
    // returns its true Or boolean false

    console.log(trueValue && "its true" && "its false")
    // returns its true Or its false

    console.log(falseValue || "its false")
    // returns value not (undefined, false, null, 0)

```

### Destructuring assign shorthands

```javascript
    import { observable, action, runInAction } from 'mobx';

    const { store, form, loading, errors, entity } = this.props;
```

### assign custom names

```javascript
    const { store, form, loading, errors, entity:contact } = this.props;
```

### Spread Operator

```javascript
    // joining arrays
    const odd = [1, 3, 5 ];
    const nums = [2 ,4 , 6, ...odd];
    console.log(nums); // [ 2, 4, 6, 1, 3, 5 ]

    // cloning arrays
    const arr = [1, 2, 3, 4];
    const arr2 = [...arr];
```

```javascript
    const odd = [1, 3, 5 ];
    const nums = [2, ...odd, 4 , 6];
```

```javascript
    const { a, b, ...z } = { a: 1, b: 2, c: 3, d: 4 };
    console.log(a) // 1
    console.log(b) // 2
    console.log(z) // { c: 3, d: 4 }
```

### Mandatory parameter shorthand

```javascript
    mandatory = () => {
        throw new Error('Missing parameter!');
    }

    foo = (bar = mandatory()) => {
        return bar;
    }
```

### Math.floor shorthand

```javascript
    ~~4.9 // 4
```

### Exponent Power shorthand

```javascript

    2**3 // 8
    2**4 // 4
    4**3 // 64

```

### Bitwise IndexOf Shorthand

```javascript
    if(~arr.indexOf(item)) { // Confirm item IS found

    }

    if(!~arr.indexOf(item)) { // Confirm item IS NOT found

    }
```

### Object.entries()

```javascript
    const credits = { producer: 'John', director: 'Jane', assistant: 'Peter' };
    const arr = Object.entries(credits);
    console.log(arr);

    /** Output:
    [ [ 'producer', 'John' ],
    [ 'director', 'Jane' ],
    [ 'assistant', 'Peter' ]
    ]
    **/
```

### Object.values()

```javascript
    const credits = { producer: 'John', director: 'Jane', assistant: 'Peter' };
    const arr = Object.values(credits);
    console.log(arr);

    /** Output:
    [ 'John', 'Jane', 'Peter' ]
    **/
```


```javascript
    function App(props){
        const test = () => ("test")
        return(
            <p>App {test()}</p>
        )
    }
```

# Javascript odities

## Null is an object so to evaluate it  

```javascript
    alert(typeof null); // alerts 'object'
    alert(null instanceof Object); // evaluates false
```

### NaN is a number, to evaluate it you can just compare it with another NaN

```javascript
    alert(typeof NaN); // alerts 'Number'
    alert(NaN === NaN); // evaluated false
```

### Replace has a callBack, for every match callBack is called

```javascript
    alert('10 13 21 48 52'.replace(/\d/g, function(match) {
        return parseInt(match) < 3 ? '*' : match; 
    })); ** *3 ** 48  5*
```

### Undefined is not reserved, it can be used inside scopes

```javascript
    (function() {
        var undefined = 'foo'; 
        alert(undefined, typeof undefined); // foo string
    })(); 
```

### Array with no keys evaluates to false when no type evaluation is used

```javascript
    alert(new Array() == false); // evaluates true
```

# React.js

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

## Sources 
- [sitepoint](https://www.sitepoint.com/shorthand-javascript-techniques/)

- [devdojo](https://devdojo.com/emmaturner/20-javascript-shorthand-to-save-time)

- [Fireshit](https://youtu.be/TNhaISOUy6Q)