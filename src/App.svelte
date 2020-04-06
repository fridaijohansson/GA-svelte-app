<!-- SCRIPT -->
<script>
//Creating a fake database with "taskArray" and declaring the variable "newTask"
let newTask="";
let taskArray = [{id:1, task:"First task", completed:false}, {id:2, task:"Second task", completed:false}];

//addTask recives an event which initiate a new task 
function addTask(event){

	//Trims off any space before and after the object
	newTask = newTask.trim();

	//If it's not a new task then the function return nothing
	if (!newTask) return;

	//This puts ""newTask" and more infrmation into a new variable
	const task = {
		task: newTask,
		completed: false,
		id: Date.now(),
	};

	//Adds the new object to the beginning of the array and redefines "newTask"
	taskArray = [task, ...taskArray];
	newTask = "";
}

function deleteTask(id){
	//Splice takes the given object out of the array based on the object's id
	taskArray = taskArray.filter(item => item.id !== Number(id));
}

//Function used to mark which task has been completed with a checkbox
function toggleComplete(id){

	const index = taskArray.findIndex(item => item.id === Number(id));
	taskArray[index].checked = !taskArray[index].completed;
}

</script>

<!-- HTML -->
<main>

	<h1>TODO APP SVELTE</h1>
	
	<!-- preventDefault is called when the form is submitted to run the function "addTask", 
	"addTask" recieves an event, submit, from preventDefault -->
	<form id="taskForm" on:submit|preventDefault={addTask}>
		
		<!-- bind:value allows the value of "newTask" to be changed by the users input -->
		<input type="text" name="taskName" id="task" placeholder="task" bind:value={newTask}>
		<input type="submit" value="Add Task">
	</form>

	<!-- In this div an each-block displays/renders the fake database everytime a new task is added. 
	When displaying the task in the div a delete button and a checkbox is added to edit the todo list-->
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

<!-- STYLE -->
<style>
*{
    margin: 0;
    padding: 0;
	list-style-type: none;
}

main{
    width: 700px;
    min-height: 400px;
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