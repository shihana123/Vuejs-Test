<template>
  <base-dialogue v-if="inputIsValid" title="Invalid Inputs" @close="theConfirmError">
    <template #default>
        <p>One of the input in empty</p>
    </template>
    <template #actions>
        <base-button @click="theConfirmError">Okay</base-button>
    </template>
  </base-dialogue>
  <base-card>
    <h3>Add Resource</h3>
    <form @submit.prevent="submitData">
        <div class="form-control">
            <label>Title</label>
            <input type="text" name="title" id="title" ref="inputTitle"/>
        </div>
        <div class="form-control">
            <label>Description</label>
            <textarea  name="description" id="description" ref="inputDesc"></textarea>
        </div>
        <div class="form-control">
            <label>link</label>
            <input type="url" name="link" id="link" ref="inputLink"/>
        </div>
        <div class="form-control">
           <base-button type="submit">Add Resource</base-button>
        </div>
    </form>
  </base-card>
</template>

<script>
  export default{
    inject:['addResource'],
    data(){
      return {
        inputIsValid : false,
      };
    },
    methods:{
      submitData(){
        const enteredTitle = this.$refs.inputTitle.value;
        const enteredDesc = this.$refs.inputDesc.value;
        const enteredLink = this.$refs.inputLink.value;

        if(enteredTitle.trim() === '' || enteredDesc.trim() === '' || enteredLink.trim() === ''){
          this.inputIsValid = true;
          return;
        }

        this.addResource(enteredTitle,enteredDesc,enteredLink);
      },
      theConfirmError(){
        this.inputIsValid = false;
      }
    }
  }
</script>
<style scoped>
label {
  font-weight: bold;
  display: block;
  margin-bottom: 0.5rem;
}

input,
textarea {
  display: block;
  width: 100%;
  font: inherit;
  padding: 0.15rem;
  border: 1px solid #ccc;
}

input:focus,
textarea:focus {
  outline: none;
  border-color: #3a0061;
  background-color: #f7ebff;
}

.form-control {
  margin: 1rem 0;
}
</style>
