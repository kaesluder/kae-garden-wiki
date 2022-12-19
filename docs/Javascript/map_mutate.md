# JavaScript helpers for modifying lists 

JavaScript helpers for modifying lists for use with React. Both 
return a new list for triggering setState functions. 

```JavaScript
// Deletes items from task list matching id.
const deleteTaskById = function (taskList, id) {
  return taskList.filter((task) => task.id !== id);
};

// Changes list elements matching predicateFunc using mutatorFunc
const mapMutate = function (li, predicateFunc, mutatorFunc) {
  return li.map((element) => {
    if (predicateFunc(element)) {
      return mutatorFunc(element);
    } else {
      return element;
    }
  });
};
```