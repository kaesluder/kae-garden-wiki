# Using a comparator function for complex logic

Written for the [Ada js-adagrams project.](https://github.com/kaesluder/js-adagrams). 

The assignment involves writing functions for a Scrabble-like game. The game has four tiebreaker conditions:

1. The word with the highest score wins.
2. If two words are tied, pick a word that uses 10 characters.
3. If neither word has 10 characters, pick a word that's the shortest.
4. If all tiebreakers fail, pick the first submitted. 

Comparator functions/expressions in Javascript return negative, zero, or
positive to determine the order of two values in a list. We chain multiple
comparator expressions using or to create multi-category sorts. 

Not the most efficient way, will probably refactor later using a `max` algorithm
rather than a `sort` algorithm. 

```Javascript
const tenLetterTieBreaker = (a, b) => {
  /* the comparator function for sort needs to 
  return negative, positive, or zero. Assign 
  a fake score to a and b, if either or both are 
  10 characters in length. 
  
  Returns zero if:
  1. Both words are < 10 characters.
  2. Both words are 10 characters. */
  const aScore = a.length == 10 ? 100 : 0;
  const bScore = b.length == 10 ? 100 : 0;

  // bump the higher value to the front of
  // the list.
  return bScore - aScore;
};

export const highestScoreFrom = (words) => {
  const sortedWords = words.sort((a, b) => {
    return (
      // try to sort by score first.
      scoreWord(b) - scoreWord(a) ||
      // if scores are equal check the tenLetterTieBreaker.
      tenLetterTieBreaker(a, b) ||
      // if there's no 10 letter tiebreaker, favor the shortest.
      a.length - b.length
      // and if everything is equal, sort should be stable
      // (I'm grateful for that.)
    );
  });
  return { word: sortedWords[0], score: scoreWord(sortedWords[0]) };
};

```
