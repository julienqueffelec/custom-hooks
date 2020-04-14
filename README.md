# useLocalStorage

`useLocalStorage` behaves just like the native react `useState` hook, except that any and all state updates are automatically saved in the browser\'s localstorage under the provided key. The first argument is the name of the key to save it under, and the second argument is the initial value. The hook returns the current state and an updater function just like `useState`.

When the app reloads, the hook will first look for a previously cached value. If one is found, it will be used as the initial value instead of the provided initial value.

```jsx
import { useLocalStorage } from "crooks";

const App = () => {
  const [state, setState] = useLocalStorage("LOCAL_STORAGE_KEY", initialValue);

  return <div>App</div>;
};
```

# useOnClickOutside

`useOnClickOutside` accepts a function that will be called when there's a click outside of a target element. The hook returns a ref, which you pass to the ref attribute of the element you want to target.

#### Basic Usage

```jsx
import { useOnClickOutside } from "crooks";

const App = () => {
  const handleClickOutside = () => {
    console.log("You clicked outside of the blue box");
  };

  const outsideRef = useOnClickOutside(handleClickOutside);

  return (
    <div>
      <div ref={outsideRef}> I'm a blue box </div>
    </div>
  );
};
```

```jsx
import { useState } from "react";
import { useOnClickOutside } from "crooks";

const App = () => {
  const [isDisabled, setIsDisabled] = useState(false);

  const disableOnOutside = () => setIsDisabled(true);

  const handleClickOutside = () => {
    console.log("You clicked outside of the blue box");
  };

  const outsideRef = useOnClickOutside(handleClickOutside, isDisabled);

  return (
    <div>
      <button onClick={disableOnOutside}>
        Stop listening for outside clicks
      </button>
      <div ref={outsideRef}> I'm a blue box </div>
    </div>
  );
};
```
