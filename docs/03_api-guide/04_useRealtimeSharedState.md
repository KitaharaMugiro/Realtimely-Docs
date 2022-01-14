---
sidebar_position: 4
---

# useRealtimeSharedState

This method can be used like React's `useState` to send the state change to the server and share the state with all users viewing the same URL.

```tsx
const [state, setState] = useRealtimeSharedState({color: "red", number:3}, "slideState") 
```

The first argument of `useRealtimeSharedState` is the default value, and the second argument is the actionId.
The actionId can be any string, as long as it is unique within the same URL.

This method returns an array with one variable and one function as a pair.
As with `useState`, the first return value stores the state, and the second is used to update the state.

The URL and actionId are paired and the value is sent to the server for management.

## On first render
Get the latest value from the server the first time it is rendered. If it cannot be obtained, the default value is used.

## When value is updated
When there is an update, the latest value is delivered to all users viewing the same URL.

