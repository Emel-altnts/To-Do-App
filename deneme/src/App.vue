<script setup>
import HelloWorld from './components/HelloWorld.vue'
import TheWelcome from './components/TheWelcome.vue'
</script>



<template>
  <div id="app" class= "app-container"> <!-- sayfada bolum olusturmak icin --> 

    <div class="task-box"> <!-- Görev yazmak için olan kutu -->
      <textarea v-model="newTask" placeholder="Add a new Task"></textarea> <!--  v-model textareadaki metni newTask'e bağlamak için (2 yönlü veri baglama) --> 
    </div>                                                                 <!--  placeholder dynamic güncelleme için (Add a new task degistiginde inputun placeholder'i da otomatik guncellenir.) --> 
    

    <div class="to-doListBox">  <!-- To-Do list'in bulunacagi kutu--> 
      <h3>To-Do List</h3>       <!-- listin basligi --> 
      <u1>
        
        <li v-for="(task,i) in tasks" :key="i"> <!-- görevlerin yapilip yapilmadigini kontrol etmek için for döngüsü --> 
          <span :class="{done:task.done}">{{task.i}}</span>
          <div class="button-container">
            <button @click="doneB(i)">✓</button> <!-- gorev yapildiysa üstünü cizen buton doneB fonksiyonu --> 
            <button @click="removeB(i)">X</button> <!-- gorevi kaldiran buton ve removeB fonksiyonu --> 
          </div>  
        </li>
      
      </u1>

    </div>


    <div>
      <button @click="addToList(i)">Add</button>  <!-- cevresi çizgili add butonu ve To-Do Liste eklemek için addToList fonksiyonu --> 
    </div>


  </div>



</template>




<script>
export default{
  data(){
    return{
      newTask: " ", 
      tasks:[ ],
    }; // newTask adında bos bir string (task-box için) ve tasks adında bos bir array (kontrol dongusunde kullanmak icin)

  },

  methods:{
    
    removeB(i){
      this.tasks.splice(i,1); // removeB methodu tasks dizisinden i indexindeki ogeyi kaldirir.
    },

    doneB(i){
      this.tasks[i].done = !this.tasks[i].done; // doneB tasks dizisindeki i indexinin gorev durumunu tersine cevirir. 
    },

    addToList(i) {
      if (this.newTask.trim() !==''){ // newTask boş değilse 
        this.tasks.push({text:this.newTask, done:false }); // newTask stringinde yazanı tasks arrayine pushla
        this.newTask= '';   // newTask strinini boşalt
      }
    },
  },
};

</script>




<style>
.app-container {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100vh ;
  gap: 100px ;
  background-color:#c1def6 ;
}

textarea{
  width: 150px;
  height:100px;
  resize: none;
  padding: 10px;
  border-radius: 4px;
  border: 1px solid #b455e0;
}

.task-box{
  display: flex;
  flex-direction: column;
  align-items: center ;
  gap: 10px;
  background-color: #c1a7f3 ;
  padding: 20px;
  border-radius: 8px;
  box-shadow:#b95ceb;
}

.to-doListBox{
  width: 250px;
  padding: 20px ;
  background-color: #c1a7f3;
  border-radius: 8px;
  box-shadow:#c166f3;
}

button{
  padding: 10px 20px;
  background-color: #f5bbe9;
  margin-top:-50px !important;
  color: #ef77eb;
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
  color: #dbc9da;
  transform:scale(1.05);
  transition: 0.4s;
}

h3{
  text-align: center;
}

u1{
  list-style-type: none;
  padding: 0;
}

li{
  align-items:center;
  display: flex;
  justify-content: space-between;
  margin: 10px ;
  padding: 5px; 
  background-color: #f2e7a9 ;
  border-radius: 4px;
}

.done{
  text-decoration:line-through;
}

.button-container{
  display: flex;
  gap: 5px;
}
</style>








