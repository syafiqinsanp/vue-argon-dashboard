<template>
  <div class="card" id="top">
    <div class="card-header pb-0">
      <h3>Get User</h3>
    </div>
    <div class="card-body px-0 pt-0 pb-2">
      <div class="table-responsive p-4">
        <table class="table align-items-center text-center">
          <thead>
            <tr>
              <th class="text-uppercase font-weight-bolder opacity-7">Avatar</th>
              <th class="text-uppercase font-weight-bolder opacity-7">Name</th>
              <th class="text-uppercase font-weight-bolder opacity-7">Email</th>
              <th class="text-uppercase font-weight-bolder opacity-7">Action</th>
            </tr>
          </thead>
          <tbody v-if="get && get.length">
            <tr v-for="get of get">
              <td>
                <img :src=get.avatar class="avatar avatar-xl" />
              </td>
              <td>
                <h5 class="font-weight-bold mb-0">{{get.first_name}} {{get.last_name}}</h5>
              </td>
              <td>
                <h5 class="font-weight-bold mb-0">{{get.email}}</h5>
              </td>
              <td>
                <button @click="deleteUser" class="btn btn-danger mt-3">Delete</button>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
  <div class="mt-4 card mx-4" id="top">
    <div class="card-header pb-0">
      <h3>Post User</h3>
    </div>
    <div class="card-body px-3 pt-0 pb-2">
      <div class="mb-3">
        <label
          for="Name"
          class="form-label fs-5 text-uppercase font-weight-bolder opacity-7"
          >Name</label
        >
        <input type="text" class="form-control" id="Name" v-model="name" />
      </div>
      <div class="mb-3">
        <label
          for="Job"
          class="form-label fs-5 text-uppercase font-weight-bolder opacity-7"
          >Job</label
        >
        <input type="text" class="form-control" id="Job" v-model="job" />
      </div>
      <button @click="post()" class="btn btn-primary">Simpan</button>
      <div id="name"></div>
      <div id="job"></div>
    </div>
  </div>

  <div class="mt-4 card mx-4" id="top">
      <div class="card-header pb-0 mb-3">
        <h3>Put User</h3>
      </div>
      <div class="card-body px-3 pt-0 pb-2">
        <div class="mb-3">
          <label
            for="name"
            class="form-label fs-5 text-uppercase font-weight-bolder opacity-7"
            >Name</label
          >
          <input type="text" class="form-control" id="name" v-model="name" />
        </div>
        <div class="mb-3">
          <label
            for="job"
            class="form-label fs-5 text-uppercase font-weight-bolder opacity-7"
            >Job</label
          >
          <input type="text" class="form-control" id="job" v-model="job" />
        </div>
        <button @click="update()" class="btn btn-primary">Submit</button>
        <div id="name"></div>
        <div id="job"></div>
      </div>
    </div>
    
    <div class="mt-4 card mx-4" id="top">
    <div class="card-header pb-0">
      <h3>Delete User</h3>
    </div>
    <div class="card-body px-3 pt-0 pb-2">
      <button @click="deleteUser" class="btn btn-primary mt-3">Delete</button>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  name: "authors-table",
  data() {
    return {
      get: []
    }
  },
  created() {
    axios.get('https://reqres.in/api/users')
      .then(response => {
        this.get = response.data.data
      })
  },
  methods: {
      async deleteUser() {
          let x = window.confirm("You want to delete the user?");
          if (x) {
              const user = await axios.delete(
                  "https://reqres.in/api/users/2"
              );
              console.log(user);
              alert("User deleted!");
          }
      },
     post() {
      axios
        .post("https://reqres.in/api/users", {
          name: this.name,
          job: this.job,
        })
        .then((response) => {})
        .catch((e) => {
          this.errors.push(e);
        });

      document.getElementById("name").innerHTML =
        '<div class="fs-4">Name : ' + this.name + "</div>";
      document.getElementById("job").innerHTML =
        '<div class="fs-4">Job : ' + this.job + "</div>";
    },
    async update() {
        try {
          const user = await axios.put(
            "https://reqres.in/api/users/2",
            {
              name: this.name,
              job: this.job,
            });
            console.log(user);
            alert("User updated!");
            } catch (e) {
              console.log(e);
            }
        },
    async deleteUser() {
      let x = window.confirm("You want to delete the user?");

      if (x) {
        const user = await axios.delete("https://reqres.in/api/users/2");

        console.log(user);
        alert("User deleted!");
      }
    },
        },
}
</script> 
