---
sidebar_position: 5
---

# Realtime Shared State

Realtimely provides `useRealtimeSharedState`, an evolution of React's `useState`.
It synchronizes the state of all users who are viewing the same URL.


```tsx
export default () => {
    
    const [slideState, setSlideState] = useRealtimeSharedState({
        pageNumber: 1,
        enableCursor: false,
        enableChat: false
    }, "slideState")

    const onClick = () => {
        slideState.pageNumber += 1
        setSlideState(slideState)
    }

    return (
        <div>
            <button onClick={onClick}>Next</button>
            <Slide pageNumber={slideState.pageNumber}>
        </div>
    )
}
```