<template>
    <div class="container mt-5">
        <div class="row justify-content-center">
            <div class="col-md-12">
                <div class="card">
                    <div class="card-header">
                        <h3 class="card-title">User Table</h3>

                        <div class="card-tools">
                            <button class="btn btn-success" data-toggle="modal" data-target="#userAdd">
                                Add New
                                <i class="fas fa-user-plus fas-fw"></i>
                            </button>
                        </div>
                    </div>
                    <!-- /.card-header -->
                    <div class="card-body p-0">
                        <table class="table table-striped">
                            <tbody>
                                <tr>
                                    <th style="width: 10px">ID</th>
                                    <th>Name</th>
                                    <th>Email</th>
                                    <th>Type</th>
                                    <th>Register At</th>
                                    <th style="width: 40px">Modify</th>
                                </tr>
                                <tr v-for="user in users" :key="user.id">
                                    <td>{{user.id}}</td>
                                    <td>{{user.name}}</td>
                                    <td>{{user.email}}</td>
                                    <td>{{user.type | capText}}</td>
                                    <td>{{user.created_at | dateFrmt}}</td>
                                    <td>
                                        <a href="#">
                                            <span class="badge bg-primary">
                                                <i class="fa fa-edit"></i>
                                            </span>
                                        </a>
                                        <a href="#">
                                            <span class="badge bg-danger">
                                                <i class="fa fa-trash"></i>
                                            </span>
                                        </a>
                                    </td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                    <!-- /.card-body -->
                </div>
            </div>
        </div>
        <UserAdd />
    </div>
</template>

<script>
    import UserAdd from './UserAdd'
import { setTimeout } from 'timers';
    export default {
        name: "User",
        components: {
            UserAdd
        },
        data(){
            return{
                users: {}
            }
        },
        methods:{
            loadUsers(){
                axios.get("api/user").then((res)=>{
                    console.log("Res ==> ",res.data.data)
                    this.users = res.data.data;
                });
            },
        },
        created(){
            this.loadUsers();
        }
    }
</script>
