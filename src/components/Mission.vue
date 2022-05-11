<template>
<h4>Mission</h4>
  <div v-if="currentMission" class="edit-form">
    <form>
      <div class="form-group">
        <label for="title">Nombre</label>
        <input type="text" disabled class="form-control" id="title"
          v-model="currentMission.name"
        />
      </div>
      <div class="form-group">
        <label for="title">Username</label>
        <input type="text" disabled class="form-control" id="title"
          v-model="currentMission.username"
        />
      </div>
      <div class="form-group">
        <label for="title">Main Stack</label>
        <input type="text" class="form-control" id="title"
          v-model="currentMission.mainStack"
        />
      </div>
    </form>
    <button class="btn btn-danger mr-2" @click="deleteMission">
      Eliminar Mission
    </button>
    <button type="submit" class="btn btn-info mr-2" @click="updateMission">
      Actualizar
    </button>
    <p>{{ message }}</p>
  </div>
  <div v-else>
    <br />
    <p> Selecciona un Mission. </p>
  </div>
</template>
<script>
import MissionService from "../services/MissionService";
export default {
  name: "Mission",
  data() {
    return {
      currentMission: null,
      message: ''
    };
  },
  methods: {
    getMission(id) {
      MissionService.get(id)
        .then(response => {
          this.currentMission= response.data;
        })
        .catch(e => {
          console.log(e);
        });
    },
    deleteMission() {
      MissionService.delete(this.currentMission.id)
      .then(response => {
        console.log(response.data);
        this.$router.push({ name: "missionComander" });
      })
      .catch(e => {
          console.log(e);
      });
    },
    updateMission() {
      MissionService.update(this.currentMission.id, this.currentMission)
        .then(response => {
          console.log(response.data);
          this.message = 'Se actualizó correctamente';
        })
        .catch(e => {
          console.log(e);
        });
    }
  },
  mounted() {
    this.message = '';
    this.getMission(this.$route.params.id);
  }
};
</script>

<style>
.edit-form {
  max-width: 300px;
  margin: auto;
}
</style>
