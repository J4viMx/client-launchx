<template>
  <div class="list row">
    <div class="col-md-6">
      <h4> MissionCommanders</h4>
      <ul class="list-group">
        <li class="list-group-item"
          :class="{ active: index == currentIndex }"
          v-for="(mission, index) in missions"
          :key="index"
          @click="setActiveMission(mission, index)"
        >
          {{ mission.username }}
        </li>

      </ul>
    </div>
    <div class="col-md-6">
      <div v-if="currentMission">
        <h4>Mission Commander</h4>
        <div>
          <br><label><strong>Nombre:</strong></label> {{ currentMission.name}}
          <br><label><strong>Username:</strong></label> {{ currentMission.username}}
          <br><label><strong>Main Stack:</strong></label> {{ currentMission.mainStack}}
        </div>
        <router-link :to="'/mission/' + currentMission.id" class="btn btn-info"> Editar</router-link>
      </div>
      <div v-else>
        <br />
        <p> Selecciona un mission commander.</p>
      </div>
    </div>
  </div>
</template>
<script>

import MissionService from "../services/MissionService";

export default {
  name: "mission-list",
  data() {
    return {
      tutorials: [],
      missions: [],
      currentTutorial: null,
      currentMission: null,
      currentIndex: -1,
      title: "",
      missionId: ""
    };
  },
  methods: {
    getAllMission(){
      MissionService.getAll()
        .then(response => {
          this.missions = response.data;
        })
        .catch(e => {
          console.log(e);
        });
    },
    setActiveMission(mission, index) {
      this.currentMission= mission;
      this.currentIndex = mission? index : -1;
    }
  },
  mounted() {
    this.getAllMission();
  }
};
</script>
