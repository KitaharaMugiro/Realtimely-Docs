---
sidebar_position: 3
---

# Realtime Cursor
![demo](/img/realtime-cursor.gif)

## Example
Call `useRealtimeCursor` on the element that covers the full screen in your React app.
Pass the return value `onMouseMove` to the element's onMouseMove event and call the` renderCursors` method in the HTML anywhere.

```tsx title="App.tsx"
import React from 'react';
import { useRealtimeCursor } from "realtimely"

function App() {

  const { onMouseMove, renderCursors } = useRealtimeCursor()

  return (
    <div className="App" onMouseMove={onMouseMove}>
      {renderCursors()}
    </div>
  );
}

export default App
```