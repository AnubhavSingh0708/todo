# todo 
this is a simple localhost based todo web app
## how it works 
### finding todos 
at first when the site loads it requests the todos from local storage using 
```
document.addEventListener('DOMContentLoaded', () => {

  const ref = localStorage.getItem('todoItems');

  if (ref) {

    todoItems = JSON.parse(ref);

    todoItems.forEach(t => {

      renderTodo(t);

    });

  }

});
```
