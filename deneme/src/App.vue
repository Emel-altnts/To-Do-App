

<template>
  
  <div id="app" data-v-app>

    <div class="everything-box">

      <div id="app" class= "app-container"> <!-- sayfada bolum olusturmak icin --> 

      <div class="task-box"> <!-- Görev yazmak için olan kutu -->
        <textarea v-model= "newTask" placeholder= "Add a new Task"></textarea> <!--  v-model textareadaki metni newTask'e bağlamak için (2 yönlü veri baglama) --> 
      </div>                                                                 <!--  placeholder dynamic güncelleme için (Add a new task degistiginde inputun placeholder'i da otomatik guncellenir.) --> 
    

      <div class="to-doListBox">  <!-- To-Do list'in bulunacagi kutu--> 
        <h3>To-Do List</h3>       <!-- listin basligi --> 
      
        <ul>       
          <li v-for="(task,i) in tasks" :key="i"> <!-- görevlerin yapilip yapilmadigini kontrol etmek için for döngüsü --> 
            <span :class="{done: task.done}" >{{task.text}}</span>
            <div class="button-container">
              <button @click="doneB(i)">✓</button> <!-- gorev yapildiysa üstünü cizen buton doneB fonksiyonu --> 
              <button @click="removeB(i)">X</button> <!-- gorevi kaldiran buton ve removeB fonksiyonu --> 
            </div>  
          </li>
        </ul>

      </div>


      <div>
        <button @click="addToList()">Add</button>  <!-- cevresi çizgili add butonu ve To-Do Liste eklemek için addToList fonksiyonu --> 
      </div>


    </div>


    </div>

  </div>
  
</template>




<script>
export default{
  data(){
    return{
      newTask:"", 
      tasks:[],
    }; // newTask adında bos bir string (task-box için) ve tasks adında bos bir array (kontrol dongusunde kullanmak icin)

  },

  methods: {
    
    addToList() {
      if (this.newTask.trim() !== ''){ // newTask boş değilse 
        this.tasks.push({text: this.newTask, done: false }); // newTask stringinde yazanı tasks arrayine pushla
        this.newTask ='';   // newTask strinini boşalt
      }
    },
  
    removeB(i){
      this.tasks.splice(i,1); // removeB methodu tasks dizisinden i indexindeki ogeyi kaldirir.
    },

    doneB(i){
      this.tasks[i].done = !this.tasks[i].done; // doneB tasks dizisindeki i indexinin gorev durumunu tersine cevirir. 
    },
  },
};   


</script>




<style>
.app-container {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 50vh ;
  gap: 200px ;
  background-color:#a7d6dc ;
}

textarea{
  width: 150px;
  height:100px;
  resize: none;
  padding: 10px;
  border-radius: 4px;
  border: 1px #9257b6;
}


.everything-box{

  display: flex;
  flex-direction: column;
  align-items: center ;
  gap: 100px;
  background-color: #f4ad87 ;
  padding: 150px;
  border-radius: 8px;

}


.task-box{
  display: flex;
  flex-direction: column;
  align-items: center ;
  gap: 10px;
  background-color: #ed7aa0 ;
  padding: 20px;
  border-radius: 8px;
  box-shadow:#b95ceb;
}

.to-doListBox{
  width: 250px;
  padding: 20px ;
  background-color: #ed7aa0;
  border-radius: 8px;
  box-shadow:#7a3c9c;
}

button{
  padding: 10px 20px;
  background-color:#c381e2;
  color:  #d6b4f5;
  border: none;
  border-radius: 4px ;
  cursor: pointer ;
}

.task-box:hover{
  background-color: #ef77eb;
  transform:scale(1.05);
  transition: 0.4s; 
}

.to-doListBox:hover{
  background-color: #b95ceb;
  transform:scale(1.05);
  transition: 0.4s;
}

button:hover{
  background-color: #ef77eb;
  color: #d356cd;
  transform:scale(1.05);
  transition: 0.4s;
}

h3{
  text-align: center;
}

ul{
  list-style-type: none;
  padding: 0;
}

li{
  align-items:center;
  display: flex;
  justify-content: space-between;
  margin: 10px 0;
  border-radius: 4px;
  padding: 5px; 
  background-color: #86a8e7 ;
}

.done{
  text-decoration: line-through;
}

.button-container{
  display: flex;
  gap: 5px;
}

li button {
  padding: 5px;
  background-color: #e4db95 ;
  margin-left: 10px;
  color:#eca247;
  border: none;
  border-radius: 50% ;
  cursor: pointer ;
  font-weight: bold;

}

li button:hover{
  background-color: #95dbca;
  color: #5fc4aa ;
}

.task-text{
  color:orange;
}

</style>








