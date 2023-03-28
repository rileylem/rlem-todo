<script>
     let todoItem = '';
     let todoList = [];

     function add() {
          if (todoItem == ''){
               return;
          }
          todoList = [...todoList, {
               text: todoItem, 
               done: false
          }]
          todoItem= '';
     }

     function removeThis(index){
          todoList.splice(index, 1);
          todoList = todoList;
     }

     function clearDone(){
          todoList = todoList.filter(t => !t.done);
     }

     function clearAll(){
          todoList = [];
     }

</script>

<div class="content">

<form on:submit|preventDefault={add}>
     <input bind:value={todoItem} type="text" autofocus/>
     <button type="submit">Add</button>
</form>

<ul>
     {#each todoList as item, index}
          <li>
               <input type="checkbox" bind:checked={item.done}>
               <span class:done={item.done}>{item.text}</span>
               <span on:click={() => removeThis(index)} on:keypress={() => removeThis(index)} class="remove"></span>
          </li>
     {/each}
</ul>

<div class="clearbtn">
     <button class="clear" on:click={clearDone}><span class="trashBin"></span> Done Items</button>
     <button class="clear" on:click={clearAll}><span class="trashBin"></span> List</button>
</div>

</div>

<style>
     .content{
          background-color: antiquewhite;
          padding: 1em;
          margin-left: 20em;
          margin-right: 20em; 
     }
     ul{
          list-style: none;
     }
     .done{
          text-decoration: line-through;
          color: rgb(157, 198, 196);
     }
     form{
          width: 200px;
          margin: auto;
     }
     .trashBin{
          background: url('./images/bin.png');
          display: inline-block;
          height: 1rem;
          width: 1rem;
          background-size: 100% auto;
     }
     button{
          background-color: rgb(157, 198, 196);
          border-radius: 3rem;
          color: white;
          border-color: rgb(69, 122, 113);
          padding: 0.5em;
     }
     .remove{
          height: 1rem;
          width: 1rem;
          display: inline-block;
          background: url('./images/minus.png') ;
          background-size: 100% auto;
          cursor: pointer;
          margin: 0em 0em 0em 1em;
     }
     li{
          width: 235px;
          margin: auto;
          font-size: 1.5em;
          padding: 0.5em 0em 0em 0em;
     }
     .clearbtn{
          text-align: center;
          padding: 2em 0em 0em 0em;
     }
</style>