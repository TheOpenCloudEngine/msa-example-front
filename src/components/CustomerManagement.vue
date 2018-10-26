<template>
  <div>
    <h1>Progressive Direct</h1>

    <customer v-model="customer" :is-new="isNew" @add="startMyQuote" @delete="deleteCustomer" @change="updateCustomer"></customer>
    <vehicles v-model="customer" v-if="!isNew"></vehicles>

  </div>
</template>

<script>
  export default {
    props: {},
    data() {
      return {
        customer: {
        },
        isNew : true
      }
    },
    created() {

    },
    watch: {},
    methods: {
      deleteCustomer(){
        $.ajax({
          url: this.customer._links.self.href,
          method: 'DELETE',
          contentType: "application/json",
          data: JSON.stringify(this.customer),
          success:
            function(result){
             alert('Successfully Deleted!');
           },
        })
      },
      updateCustomer(){
        $.ajax({
          url: this.customer._links.self.href,
          method: 'PATCH',
          contentType: "application/json",
          data: JSON.stringify(this.customer),
          success:
            function(result){
             alert('Successfully Updated!');
           },
        })
      },
       startMyQuote(){

          var self = this;

          $.ajax({
            url: "http://localhost:8080/customers",
            method: 'POST',
            contentType: "application/json",
            data: JSON.stringify(this.customer),
            success:
              function(result){
               alert('Successfully Added!');
                self.isNew = false;
                self.customer = result;
                self.customer = null;
                self.customer = result;
             },
          })
       },
    }
  }
</script>

<style scoped lang="scss" rel="stylesheet/scss">

</style>
