# Map Equality

```ts
function deepEqual(a: Map<string, number>, b: Map<string, number>) {
  if (a.size !== b.size) return false;
  return Array.from(a.keys()).every((key) => a.get(key) === b.get(key));
}
```
