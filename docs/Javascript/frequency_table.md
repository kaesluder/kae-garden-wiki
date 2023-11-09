# Frequency Table

```ts
function freqMap(s: string): Map<string, number> {
  return s.split('').reduce((freq: Map<string, number>, c: string) => {
    freq.set(c, freq.has(c) ? freq.get(c) + 1 : 1);
    return freq;
  }, new Map<string, number>());
}
```
