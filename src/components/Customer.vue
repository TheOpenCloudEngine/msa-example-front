<template>
    <md-card :class="isNew ? 'md-primary' : ''">

      <md-card-header>
        Provide Policyholder Name and Address
      </md-card-header>


      <md-card-content v-if="!isNew">
        <md-input-container>
          <label>Name</label>
          <md-input v-model="value.firstName" ></md-input>
        </md-input-container>
        <md-input-container>
          <label>SSN</label>
          <md-input v-model="value.ssn"></md-input>
        </md-input-container>

        <md-button @click="update">Update</md-button>
        <md-button @click="remove">Delete</md-button>
      </md-card-content>
      <md-card-content v-else>
        <md-input-container>
          <label>Name</label>
          <md-input v-model="value.firstName"></md-input>
        </md-input-container>
        <md-input-container>
          <label>SSN</label>
          <md-input v-model="value.ssn"></md-input>
        </md-input-container>

        <md-button @click="add">Start My Quote</md-button>

      </md-card-content>
    </md-card>

</template>
<script>
  export default {
    props: {
      value: Object,
      editMode: false,
      isNew: false
    },
    data() {
      return {
      }
    },
    watch: {},
    methods: {
      update(){

        this.$emit('input', this.value);
        this.$emit('change', this.value);
      },
      remove(){

        this.$emit('input', this.value);
        this.$emit('delete', this.value);

        this.isNew = true;
      },

      add(){
         this.$emit('input', this.value);
         this.$emit('add', this.value);
      },

      jumpToClasses(){
        this.$emit('classes', this.value);
      }


    }
  }
</script>

<style scoped lang="scss" rel="stylesheet/scss">

</style>
