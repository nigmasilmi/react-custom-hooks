# Http request custom hook

## To make it fully configurable

1. Identify the variables that will change depending on the use case
2. Pass that variables as parameters to the hook.
3. If there is a transformation related, create a specific function in the component that uses the hook, because it will vary depending on the use case, and pass it also as a parameter, that function will be called from inside the hook but will be executed inside the component.
4. The component is the one that must trigger the sendRequest and be aware of the states so, we must export this pieces from the hook.
5. Import the hook when it will be used and clean the unecessary states that now are managed inside the hook
6. Call the hook with the required parameters
7. Refactor the hook to make it versatile for all request methods (get is the default and does not require a body, so give a default value and make it optional)
8. Create a function that will recieve the data (refered in step 3)
9. Manage the return of the call with destructuring
10. Keep the call to the function that makes the http request inside of useEffect()
