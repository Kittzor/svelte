<script>
  import { onMount } from 'svelte';
  let todos = [];
  let newTodo = '';

  onMount(async () => {
    const res = await fetch('http://localhost:3000/todos');
    todos = await res.json();
  });

  function addTodo() {
    if (newTodo.trim()) {
      todos = [...todos, newTodo];
      newTodo = '';
    }
  }
</script>

<input bind:value={newTodo} placeholder="Lägg till todo" />
<button on:click={addTodo}>Lägg till</button>

<ul>
  {#each todos as todo, i}
    <li>{todo}</li>
  {/each}
</ul>

<style>
  input {
    padding: 0.5rem;
    border-radius: 4px;
  }

  button {
    background-color: #007acc;
    color: white;
    border: none;
    padding: 0.5rem 1rem;
    border-radius: 4px;
    cursor: pointer;
  }

  button:hover {
    background-color: #005fa3;
  }
</style>

