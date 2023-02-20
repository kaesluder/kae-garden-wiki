# filesearcher

I'm working on some learning projects, aka reimplementing stuff that could be done easier by piping a bunch of shell utilities together. A few lessons from DIY sewing:

1. Give it permission to look weird.
2. No, you're (probably) not going to reach the same level of speed and efficiency as a sweatshop with 300 years of technological automation.
3. Knowing how it works is priceless.

```JavaScript

import util from 'node:util'
import * as fsWalk from '@nodelib/fs.walk'

const ignoreDirs = ['.git', /node_modules/]

const ignore = function (entry, ignoreDirs) {
  for (let d in ignoreDirs) {
    if (entry.path.search(d) > 0) {
      return true
    }
  }
  return false
}

const runGlob = function (searchStr, path) {
  // todo ramda might make this easier
  const searchThis = (entry) => ignore(entry, ignoreDirs)
  const walk = util.promisify(fsWalk.walk)
  const filterPredicate = (entry) => entry.path.search(searchStr) > 0
  return walk(path ?? '.', { deepFilter: searchThis }).then((response) =>
    response.filter(filterPredicate)
  )
}

export { runGlob, ignore }
```

Lessons learned:

1. A large number of my files are ephemera from the development process, so having a way to exclude `.git`, `venv`, and `node_modules` will dramatically cut down the time. (As much as 90%.)
2. I spent way too much time trying to fit that for loop into a ramda expression.
3. I'm having much better luck working with vite compared to webpack/babel.

Things I need to learn:

1. The concepts under other people's boilerplate.
2. How to test async functionality in jest/vitest.
