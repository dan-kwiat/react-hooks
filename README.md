# React Hooks

## `useServerSentEvents`

```tsx
import useServerSentEvents from "hooks/useServerSentEvents"

interface QueryParams {
  prompt: string
}

export default function MyComponent() {
  const { openStream, closeStream } = useServerSentEvents<QueryParams>({
    baseUrl: "/api/converse-edge",
    config: {
      withCredentials: false,
    },
    onData: (data) => {
      try {
        console.log(JSON.parse(data))
      } catch (e) {
        console.error(`Failed to parse data`)
      }
    },
    onOpen: () => {
      console.log(`Stream opened`)
    },
    onClose: () => {
      console.log(`Stream closed`)
    },
    onError: () => {
      console.error(`Stream error`)
    },
  })

  function onClick() {
    const evtSource = openStream({
      query: {
        prompt: `Why is the sky blue?`,
      },
    })
    // Call `closeStream(evtSource)` to abort
  }

  return (
    <div>
      <button onClick={onClick}>Open Stream</button>
    </div>
  )
}
```
