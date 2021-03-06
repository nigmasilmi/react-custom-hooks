# Http request custom hook

## To make it fully configurable

1. Identify the variables that will change depending on the use case
2. Pass those variables as parameters to the hook.
3. If there is a transformation related, create a specific function in the component that uses the hook, because it will vary depending on the use case, and pass it also as a parameter, that function will be called from inside the hook but will be executed inside the component.
4. The component is the one that must trigger the sendRequest and be aware of the states so, we must export these pieces from the hook.
5. Import the hook when it will be used and clean the unnecessary states that now are managed inside the hook
6. Call the hook with the required parameters
7. Refactor the hook to make it versatile for all request methods (get is the default and does not require a body, so give a default value and make it optional)
8. Create a function that will receive the data (refered in step 3)
9. Manage the return of the call with destructuring
10. Keep the call to the function that makes the http request inside of useEffect()
11. Remember that any piece of code used in useEffect and defined inside of the component, must be part of the dependencies, but if we add the same function executed inside the useEffect as a dependency, it will create an infinite loop because inside of the hook there are states been managed, and those states changes will trigger the re-render of the component where the hook is used, then the hook will execute again and the fuction that is used in the useEffect will be a different one (diferenct object after re-rendering), that will trigger the same chain of events again and again
12. To solve 11, we must use useCallback for the function used inside useEffect
13. 12 brings another issue, as the dependencies are objects (one is a function and one is an object literal), we can solve this issue wrapping the function with useCallback, but the object literal will be another tricky challenge we can solve with useMemo, although, this indicates that the logic inside the custom hook is a good place to refactor and avoid all those issues
14. Make the requestConfig (the object literal referred in 13) as parameter of the sendRequest itself and not a parameter for the hook, in that sense, this won't be a dependency for the useCallback
15. Place the requestConfig object as parameter for the sendRequest function
16. To avoid the useCallback for the data transformation function, define the latter inside the useEffect and pass it as a parameter for the sendRequest function
17. Use the hook in other files. E.g. NewTask.js => Refactor to accommodate to the hook.
18. One important piece of data is not available now: the taskText
19. To solve 18:
    19.1 Pass the taskText as a parameter for createTask
    19.2 But the correspondent function in the custom hook expects just one argument, that can be solved using bind()
    19.3 bind() allows to pre-configure a function, receives 2 arguments, the first is to configure the "this" and the second will be the first argument to receive by that "to be function"
20. Now the custom hook is fully configurable for any kind of request and will perform optimally
