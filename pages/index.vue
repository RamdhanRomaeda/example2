<template>
  <div class="py-4">
    <div class="container">
      <div class="title border-bottom d-flex align-items-center justify-content-between py-2">
        <h5>Task</h5>
        <div class="kotak-kategori"  >
          <button  class="btn btn-secondary dropdown-toggle" type="button" data-bs-toggle="dropdown" aria-expanded="false" @click = "isDropdown=!isDropdown">
            Kategori
          </button>
          <ul class="list-kategori" v-if="isDropdown">
            <li @click = " searchKategori='Berat',isDropdown=!isDropdown " ><a href="#" >Berat</a></li>
            <li @click = " searchKategori='Sedang',isDropdown=!isDropdown"><a href="#" >Sedang</a></li>
            <li @click = "searchKategori='Ringan',isDropdown=!isDropdown"><a href="#" >Ringan</a></li>
          </ul>
        </div>
        <div class="d-flex align-items-center ms auto">        
          <input type="text" class="form-control" placeholder="Search" v-model="searchQuery">
          <div class="d-flex align-items-center justify-content-end w-100">
            <span class="me-2">View As</span>
            <button class="btn btn-outline-secondary py-1 px-3" @click="isGrid = !isGrid">
              {{ isGrid ? 'Grid' : 'List'}}
            </button>
          </div>
        </div>
      </div>
        <div class="list-task row">
          <CardItem
            v-for="(task, i) in resultQuery" 
            :key="i"
            :task="task" 
            :isGrid="isGrid"
           />
        </div>   
      <div class="py-2">
        <a v-if=!isCreating href="#" class="add-button"  @click="isCreating = !isCreating">Add Task</a>
        <div v-else class="add-card" >
          <div class="card mb-2">
            <div class="card-body d-flex flex-column p-0">
              <input type="text" placeholder="Title" class="form-control border-0 mb-2">
              <textarea placeholder="description" rows="10" class="form-control"></textarea>
            </div>
          </div>
          <div class="button-wrapper d-flex">
            <button class="btn btn-primary me-2">Save</button>
            <button class="btn btn-outline-secondary" @click="isCreating = !isCreating">Cancel</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import CardItem from "@/components/Card/CardItem.vue"
  export default{
    layout (context){
        return 'custom'
    },
    components:{
      CardItem
    },
    data(){      
      return{
        isDropdown:false,
        searchKategori:'',
        searchQuery : '',
        isCreating:false,
        isGrid:false,
        tasks:[
          {
            title: 'Task 1',
            description : 'ini deskripsi 1',
            isDone: false,
            kategori: 'Berat',
          },
          {
            title: 'Task 2',
            description : 'ini deskripsi 2',
            isDone: false,
            kategori: 'Sedang',
          },
          {
            title: 'Task 3',
            description : 'ini deskripsi 3',
            isDone: false,
            kategori: 'Ringan',
          },
          {
            title: 'Task 4',
            description : 'ini deskripsi 4',
            isDone: false,
            kategori: 'Berat',
          },
          {
            title: 'Task 5',
            description : 'ini deskripsi 5',
            isDone: false,
            kategori: 'Sedang',
          },
          {
            title: 'Task 6',
            description : 'ini deskripsi 6',
            isDone: false,
            kategori: 'Ringan',
          }
        ]
      }
    },
    computed:{
      resultQuery(){
        if(this.searchQuery){
          return this.tasks.filter((item)=>{
          return this.searchQuery.toLowerCase().split().every((v)=> item.title.toLowerCase().includes(v));
          });
        }else if(this.searchKategori === 'Berat'||this.searchKategori === 'Sedang' || this.searchKategori === 'Ringan'){
          console.log('berat')
          return this.tasks.filter((item)=>{
          return this.searchKategori.toLowerCase().split().every((v)=> item.kategori.toLowerCase().includes(v));
          }); 
        }else{
          console.log(this.tasks);
          return this.tasks
        }
        
      },
    }
  }
</script>
<style>
.list-kategori{
  display: flex;
  flex-direction: column;
  justify-content: space-evenly;
  align-items: center;
  margin-top: 10px;
  background-color: white;
  width: 170px;
  height: 100px;
  border: 0.5px solid rgb(192, 192, 192);
  border-radius:10px;
  color: white;
  position: absolute;
  box-sizing: border-box;
  overflow: hidden;
  padding: 0px;
}
.list-kategori li {
  line-height: 30px;
  display: block;
  width: 100%;
  height: 33px;
  list-style: none;
  text-align: center;
}
.list-kategori li a{
  text-decoration: none;
  color: gray;
}
.list-kategori li:hover{
  background-color: rgb(59, 163, 59);
}
.list-kategori li:hover a{
  color: white;
}

</style>


