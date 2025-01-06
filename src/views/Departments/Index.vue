<script setup>
import {ref, onMounted} from 'vue'
import { confirmation } from '@/function';
import { useAuthStore } from '@/stores/auth';

const authStore = useAuthStore();
axios.defaults.headers.common['Authorization'] = 'Bearer '+ authStore.authToken
onMounted(() => {getDepartments()})

const departments = ref([])
const load = ref(false)

const getDepartments = async () => {
    await axios.get('api/departments').then(
        response =>  departments.value = response.data.data );
    load.value = true;  
}

const deleteDepartments = (id, name) => {
  confirmation(name,'api/departments/'+id,'/departments')
}


</script>

<template>
    <div class="row">
      <div class="col-md-4 offset-md-4">
        <div class="d-grid col-10 mx-auto">
          <router-link :to="{name: 'create'}" class="btn btn-dark">
            <i class="fa-solid fa-circle-plus"></i> Add
          </router-link>
        </div>
      </div>
    </div>
    <div class="row mt-3">
      <div class="col-md-6 offset-md-3">
        <div class="card border border-white text-center" v-if="!load">
          <div class="card-body">
            <img src="/loading.gif" class="img-fluid">
          </div>
        </div>
        <div class="table-responsive" v-else>
          <table class="table table-bordered table-hover">
            <thead>
              <tr>
                <th>#</th>
                <th>DEPARTMENT</th>
                <th></th>
              </tr>
            </thead>
            <tbody class="table-group-divider">
                <tr v-for="dep, i in departments" :key="dep.id">
                  <td>{{ (i+1) }}</td>
                  <td>{{ dep.name }}</td>
                  <td>
                    <router-link :to="{name: 'edit', params:{id: dep.id}}" class="btn btn-warning">
                      <i class="fa-solid fa-edit"></i>
                    </router-link>
                  </td>
                  <td>
                    <button class="btn btn-danger" @click="deleteDepartments(dep.id, dep.name)">
                      <i class="fa-solid fa-trash"></i>
                    </button>
                  </td>
                </tr>
            </tbody>
          </table>
        </div>
      </div>
    </div>
</template>