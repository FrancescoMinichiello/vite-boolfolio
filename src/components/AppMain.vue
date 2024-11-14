<script>

import axios from "axios";
export default{
    name: "AppMain",
    data(){
        return{
            projectList:[],
        }
    },
    methods:{
        getProjects(){
            axios.get('http://127.0.0.1:8000/api/projects')
                .then((response) => {
                   this.projectList = response.data.results
                })
                .catch(function (error) {
                    console.log(error);
                })
        }
    },
    created(){
       this.getProjects();
    }

}
</script>

<template>
<main class="container">
    <div class="row py-5">
        <div class="col-12 mb-3">
            <h2>
                Projects List:
            </h2>
        </div>
        <div class="col">
            <article class="card" v-for="singleProject in projectList" :key="singleProject.id">
                <div class="card-body">
                    <h1 class="card-title">
                        {{ singleProject.name }}
                    </h1>
                    <div class="card-subtitle" v-for="technology in singleProject.technologies" :key="technology.id">
                        <h3>
                          tecnologie usate:  {{ technology.name }}
                        </h3>
                    </div>
                    <div class="card-text">
                       <a :href="singleProject.link">Vai al progetto</a> 
                    </div>
                </div>
            </article>
        </div>
    </div>
</main>
</template>

<style>

</style>