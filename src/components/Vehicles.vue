<template>
    <md-card :class="'md-primary'">

      <md-card-header>
        Add vehicles to your quote
      </md-card-header>


      <md-card-content>
        <md-chips v-model="vehicles[index]" v-for="(vehicle, index) in vehicles">
          {{vehicle.modelName}}
        </md-chips>

      <md-input-container>
        <label>Model Name</label>
        <md-input v-model="newModelName"></md-input>
      </md-input-container>

        <md-button @click="addVehicle">Add</md-button>
      </md-card-content>
    </md-card>

</template>
<script>
  export default {
    props: {
      value: Object,
    },
    data() {
      return {
        vehicles:[],
        newModelName
      }
    },
    watch: {
      value: {
          handler: function(){

              var me = this;

              $.ajax({
                url: "http://localhost:8080/dmv-service/owners/" + this.value.ssn + "/vehicles",
                success:   function(result){
                             me.vehicles = result;
                             alert('xxx')
                           },
              })

          },
          deep: true

      }

    },
    methods: {
      addVehicle: function(){
       // this.vehicles = [];
        this.vehicles.push({modelName: this.newModelName})

      }

    }
  }
</script>

<style scoped lang="scss" rel="stylesheet/scss">

</style>
