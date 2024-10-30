<script>
    let tasks = [];
    let newTask = '';

    // Function to add a new task
    function addTask() {
        if (newTask.trim() !== '') {
            tasks = [...tasks, { text: newTask, completed: false }];
            newTask = '';
        }
    }

    // Function to remove a task
    function removeTask(index) {
        tasks = tasks.filter((_, i) => i !== index);
    }

    // Function to toggle task completion
    function toggleTask(index) {
        tasks = tasks.map((task, i) => {
            if (i === index) {
                return { ...task, completed: !task.completed };
            }
            return task;
        });
    }
</script>

<style>
	main {
		max-width: 400px;
		margin: 50px auto;
		padding: 20px;
		box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
		border-radius: 8px;
		background-color: #f9f9f9;
	}
 
	input[type="text"] {
		width: calc(100% - 60px);
		padding: 8px;
		margin-right: 10px;
	}
 
	button {
		padding: 8px;
		cursor: pointer;
	}
 
	ul {
		list-style-type: none;
		padding: 0;
	}
 
	li {
		display: flex;
		align-items: center;
		margin: 10px 0;
	}
 
	.completed {
		text-decoration: line-through;
		color: grey;
	}
 </style>
 

<main>
    <h1>To-Do List</h1>
    <input type="text" bind:value={newTask} placeholder="Add a new task..." />
    <button on:click={addTask}>Add Task</button>

    <ul>
        {#each tasks as task, index}
            <li>
                <input type="checkbox" checked={task.completed} on:change={() => toggleTask(index)} />
                <span class:completed={task.completed}>{task.text}</span>
                <button on:click={() => removeTask(index)}>Remove</button>
            </li>
        {/each}
    </ul>
</main>
