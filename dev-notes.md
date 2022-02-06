# Http request custom hook

## To make it fully configurable

1. Identify the variables that will change depending on the use case
2. Pass that variables as parameters to the hook.
3. If there is a transformation related, create a specific function in the component that uses the hook, because it will vary depending on the use case, and pass it also as a parameter, that function will be called from inside the hook but will be executed inside the component.
4. The component is the one that must trigger the sendRequest and be aware of the states so, we must export this pieces from the hook.
5.
