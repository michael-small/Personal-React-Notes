# Hooks

The way that Styled Components uses hooks, the components should be declared in a file above the use of other hooks. For example, the following is fine:

```jsx
export default function BlogPosts() {
	const StyledCard = styled(Card)`
		margin-bottom: 0.5rem;
		max-width: 600px;
	`;

	const { loading, error, data } = useQuery(GET_POSTS);
  ...
}
```
However, the following order produces the error that follows it:

```jsx
	const { loading, error, data } = useQuery(GET_POSTS);
  
  	const StyledCard = styled(Card)`
		margin-bottom: 0.5rem;
		max-width: 600px;
	`;
```
> Warning: React has detected a change in the order of Hooks called by BlogPosts. This will lead to bugs and errors if not fixed. For more information, read the Rules of Hooks: https://reactjs.org/link/rules-of-hooks

>   Previous render            Next render
> ------------------------------------------------------
> 1. useContext                 useContext
> 2. useReducer                 useReducer
> 3. useRef                     useRef
> 4. useRef                     useRef
> 5. useEffect                  useEffect
> 6. useEffect                  useEffect
> 7. undefined                  useRef
   ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

    at BlogPosts (http://localhost:3000/static/js/main.chunk.js:410:70)
    at aux (http://localhost:3000/static/js/main.chunk.js:1789:28)
    at Home (http://localhost:3000/static/js/main.chunk.js:560:1)
    at Route (http://localhost:3000/static/js/vendors~main.chunk.js:84246:29)
    at Router (http://localhost:3000/static/js/vendors~main.chunk.js:83881:30)
    at BrowserRouter (http://localhost:3000/static/js/vendors~main.chunk.js:83501:35)
    at div
    at CssBaseline (http://localhost:3000/static/js/vendors~main.chunk.js:13445:31)
    at WithStyles(CssBaseline) (http://localhost:3000/static/js/vendors~main.chunk.js:21513:31)
    at App
    at ApolloProvider (http://localhost:3000/static/js/vendors~main.chunk.js:6836:19)
