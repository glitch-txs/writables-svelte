# writables-svelte
Create multiple writables in one function call

```ts
import { writable, type Writable } from "svelte/store"

export function createWritables<W extends object>(store: W){

  type Writables = { [key in keyof W]?: Writable<W[key]> }

  let writables: Writables | undefined

  for (const state of Object.values(store)){
    const new_writable = writable<typeof state>(state)
    writables = { ...writables, [state]: new_writable }
  }

  return writables as Required<Writables>
}
```
