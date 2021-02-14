<script lang="ts">
  import { v4 as uuid } from 'uuid';

  type Todo = {
    id: string;
    text: string;
    checked: boolean;
  };

  let todos: Todo[] = [];
  let text: string = '';

  const onAddClick = () => {
    if (!text) return;

    todos = [...todos, { id: uuid(), text, checked: false }];
    text = '';
  };

  const onDeleteClick = () => {
    todos = todos.filter((todo) => !todo.checked);
  };

  const onClearClick = () => {
    todos = [];
  };

  const onEnter = (event: KeyboardEvent) => {
    if (event.key === 'Enter') {
      onAddClick();
    }
  };
</script>

<div class="App">
  <section class="form">
    <input type="text" bind:value={text} on:keydown={onEnter} />
    <button on:click={onAddClick}>ADD</button>
  </section>

  <section class="menu">
    <button class="delete" on:click={onDeleteClick}>DELETE</button>
    <button class="clear" on:click={onClearClick}>CLEAR</button>
  </section>

  <ul class="list">
    {#each todos as todo}
      <li>
        <input id={todo.id} type="checkbox" bind:checked={todo.checked} />
        <label for={todo.id}>{todo.text}</label>
      </li>
    {/each}
  </ul>
</div>

<style>
  .App {
    width: 1280px;
    margin: 0 auto;
  }

  button {
    margin: 0;
    border: none;
    padding: 8px 16px;
    font-weight: bold;
    letter-spacing: 0.08em;
    border-radius: 4px;
    background: none;
    outline: none;
    cursor: pointer;
    text-transform: uppercase;
  }

  .form {
    display: flex;
    align-items: center;
    margin: 32px 0 8px;
  }

  .form input {
    flex: 1 1 0px;
    padding: 4px 8px;
    font-size: 16px;
    line-height: 1.2;
    border: none;
    border-bottom: 1px solid gray;
    outline: none;
  }

  .form button {
    margin-left: 8px;
    background-color: hsl(236, 100%, 90%);
    border: 2px solid hsl(236, 100%, 50%);
  }

  .form button:hover {
    background-color: hsl(236, 100%, 70%);
    color: hsl(0, 100%, 100%);
  }

  .menu button {
    background-color: hsl(0, 100%, 90%);
    border: 2px solid hsl(0, 100%, 50%);
  }

  .menu button:hover {
    background-color: hsl(0, 100%, 70%);
    color: white;
  }

  .menu .clear {
    background-color: hsl(46, 100%, 90%);
    border: 2px solid hsl(46, 100%, 50%);
  }

  .menu .clear:hover {
    background-color: hsl(46, 100%, 70%);
    color: white;
  }

  .list {
    list-style: none;
    margin: 4px 0 8px;
    padding: 0;
  }

  .list li {
    display: flex;
    align-items: center;
    padding: 16px 8px;
  }

  .list li + li {
    border-top: 1px solid gray;
  }

  .list li input {
    margin: 0 16px;
  }
</style>
