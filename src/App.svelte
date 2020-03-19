<script>
	let newTask="";
	let taskArray = [{id:1, task:"första händelse", completed:false},
	{id:2, task:"andra händelse", completed:false}];


	function addTask(event){
		newTask = newTask.trim();
		alert(newTask);
		if (!newTask) return;

		const task = {
			task: newTask,
			completed: false,
			id: newTask.length-1,
		};

		taskArray = [task, ...taskArray];
		
		newTask = "";
	}



	function deleteTask(id){

		//Splice takes the given object out of the array
		  taskArray = taskArray.filter(item => item.id !== Number(id));

		

	}

	//Function used to mark which task has been completed with a checkbox
	function toggleComplete(id){

		const index = taskArray.findIndex(item => item.id === Number(id));
	 	taskArray[index].checked = !taskArray[index].completed;
		
	}







</script>


<main>
	<h1>TODO APP SVELTE</h1>
	
	<form id="taskForm" on:submit|preventDefault={addTask}>
		
		<input type="text" name="taskName" id="task" placeholder="task" bind:value={newTask}>
		<button on:click={addTask}>Add task</button>
	</form>



	<div id="todoList">
		{#each taskArray as task (task.id)}
			<div class="container">
				<h1 class="newTask">{task.task}</h1>
				<div class="buttons">
					<input id={task.id} type="checkbox" on:click={() => toggleComplete(task.id)}>
					<button class="delete-btn" on:click={() => deleteTask(task.id)}>-</button>
				</div>
			</div>
			<hr>
		{/each}
		
		

	</div>




</main>





<style>
*{
    margin: 0;
    padding: 0;
	list-style-type: none;
}

main{
    width: 700px;
    min-height: 800px;
    background-color: rgb(133, 157, 192);
    margin: auto;
    margin-top: 20px;
    padding: 10px;
    border-radius: 10px;
    border: solid 4px rgb(49, 49, 77);
    text-align: center;
}
#taskForm{
    padding-bottom: 10px;
    border-bottom:solid 3px rgb(49, 49, 77);
}
#task{
    width: 500px;
    padding: 2px;
    font-size: 16px;
}
h1{
    padding: 10px;
}

.container{
    display: flex;
    
} 

.buttons{
    flex: 1;

}
.newTask{
    flex: 3;
    max-width: 400px;


}


.delete-btn{
    background-color: red;
    border: solid 3px brown;
    color: white;
    font-size: 1rem;
    padding: 0px 4px 0px 4px;
    margin: 5px;
}



</style>