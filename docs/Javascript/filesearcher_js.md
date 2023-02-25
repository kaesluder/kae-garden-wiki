# filesearcher

I'm working on some learning projects, aka reimplementing stuff that could be done easier by piping a bunch of shell utilities together. A few lessons from DIY sewing:

1. Give it permission to look weird.
2. No, you're (probably) not going to reach the same level of speed and efficiency as a sweatshop with 300 years of technological automation.
3. Knowing how it works is priceless.

```JavaScript

import util from 'node:util'
import * as fsWalk from '@nodelib/fs.walk'

// https://www.npmjs.com/package/@nodelib/fs.walk

const errorFilter = (error) => error.code === 'EACCES' || 'EPERM'

const ignoreDirs = [/[.]git[/]/, /[/]node_modules[/]/]

/**
 * Filter predicate to determine if a directory should be
 * ignored or not.
 * @param {fsWalk.Entry} entry Entry to match against.
 * @param {Regexp[]} ignoreDirs List of RegExps to match directories to ignore.
 * @returns {Boolean}
 */
const ignore = function (entry, ignoreDirs) {
  for (let i in ignoreDirs) {
    let dr = new RegExp(ignoreDirs[i])
    if (dr.test(entry.path)) {
      return true
    }
  }
  return false
}

/**
 * Run a search query and return a list of matching fsWalk entries.
 * @param {String} searchStr Regexp or string to match against target path.
 * @param {String} path Source path from which to start searching.
 * @param {String[]} ignoreDirs List matching dirs to ignore.
 * @returns
 */
const runGlob = function (searchStr, path, ignoreDirs) {
  // todo ramda might make this easier
  const searchThis = (entry) => {
    if (ignore(entry, ignoreDirs)) {
      return false
    } else {
      return true
    }
  }
  const searchReg = new RegExp(searchStr)

  // Transform a function that uses a callback into one that returns a promise.
  const walk = util.promisify(fsWalk.walk)
  return walk(path ?? '.', { deepFilter: searchThis, errorFilter: errorFilter }).then((response) =>
    response.filter((entry) => searchReg.test(entry.path))
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

EDIT: Updated to fix some string-matching and logic errors.
