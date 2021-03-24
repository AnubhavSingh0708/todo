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
### if todos found create todos 
if todo list is detected then it makes the todo list else it removes the list and removes items from local storage using 
``` 
  localStorage.setItem('todoItems', JSON.stringify(todoItems));

  const list = document.querySelector('.js-todo-list');

  const item = document.querySelector(`[data-key='${todo.id}']`);

  if (todo.deleted) {

    item.remove();

    if (todoItems.length === 0) list.innerHTML = '';

    return

  }
```
in function `renderToDo(t)` in the previous code 
### and when todo item is created 
at first detecting if text input is submitted using 
```
const form = document.querySelector('.js-form');

form.addEventListener('submit', event => {

  event.preventDefault();

  const input = document.querySelector('.js-todo-input');

  const text = input.value.trim();

  if (text !== '') {

    addTodo(text);

    input.value = '';

    input.focus();

  }

});
```
and then on function addTodo(text); 
creating todo item and saving to local host using 
``` 
function addTodo(text) {

  const todo = {

    text,

    checked: false,

    id: Date.now(),

  };

  todoItems.push(todo);

  renderTodo(todo);

}
```
### marking todos done 
when todos are done click on them to mark done using 
javascript `addEventListener`to detect if it is clicked

```
const list = document.querySelector('.js-todo-list');

list.addEventListener('click', event => {

  if (event.target.classList.contains('js-tick')) {

    const itemKey = event.target.parentElement.dataset.key;

    toggleDone(itemKey);

  }
  ```
  and then marking todos done on function toggleDone(itemKey);
  ```
  function toggleDone(key) {

  const index = todoItems.findIndex(item => item.id === Number(key));

  todoItems[index].checked = !todoItems[index].checked;

  renderTodo(todoItems[index])

  localStorage.setItem('todoItems', JSON.stringify(todoItems));

}
  ```
  ### deleting todos 
  detecting using 
  ```
  if (event.target.classList.contains('js-delete-todo')) {

    const itemKey = event.target.parentElement.dataset.key;

    deleteTodo(itemKey);

  }

});
```
and then deleting using 
```
function deleteTodo(key) {

  const index = todoItems.findIndex(item => item.id === Number(key));

  const todo = {

    deleted: true,

    ...todoItems[index]

  }

  todo.deleted = true

  todoItems = todoItems.filter(item => item.id !== Number(key));

  renderTodo(todo);

}
```
