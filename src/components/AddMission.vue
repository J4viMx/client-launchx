<template>
  <div class="submit-form">
    <div v-if="!submitted">
    <h3>Nuevo Mission Commander</h3>
      <div class="form-group">
        <label for="title">Nombre </label>
        <input
          type="text"
          class="form-control"
          id="title"
          required
          v-model="Mission.name"
          name="title"
        />
      </div>
      <div class="form-group">
        <label for="title">Username</label>
        <input
          type="text"
          class="form-control"
          id="username"
          required
          v-model="Mission.username"
          name="username"
        />
      </div>
      <div class="form-group">
        <label for="title">Main Stack</label>
        <input
          type="text"
          class="form-control"
          id="mainStack"
          required
          v-model="Mission.mainStack"
          name="mainStack"
        />
      </div>
      <button @click="saveMission" class="btn btn-success">Agregar</button>
    </div>
    <div v-else>
      <h4> Mission creado exitosamente. </h4>
      <button class="btn btn-success" @click="newMission">Add</button>
    </div>
  </div>
</template>

<script>
import MissionService from "../services/MissionService";
export default {
  name: "add-Mission",
  data() {
    return {
      Mission: {
        id: null,
        name: "",
        username: "",
        mainStack: ""
      },
      submitted: false
    };
  },
  methods: {
    saveMission() {
      var data = {
        name: this.Mission.name,
        username: this.Mission.username,
        mainStack: this.Mission.mainStack
      };
      MissionService.create(data)
        .then(response => {
          this.Mission.id = response.data.id;
          this.submitted = true;
        })
        .catch(e => {
          console.log(e);
        });
    },
    newMission() {
      this.submitted = false;
      this.Mission = {};
    }
  }
};
</script>
