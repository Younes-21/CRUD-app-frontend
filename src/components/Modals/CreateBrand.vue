<template>
<div class="bloc-modale">
    <div class="overlay" v-on:click="toggleModal"></div>
<div  class="modale card">
<div class="btn-modale btn btn-danger" v-on:click="toggleModal" >X</div>
    <div class="container">
        <div style="width:400px"><h4 >Create brand form</h4></div> 
         <form @submit.prevent="CreateBrand">
      <div class="form-group row" style="width:200px ">
    
    <label>Brand name</label>
<input type="text" class="form-control col-3 mx-2" placeholder="Brand name" v-model="brand.Name_brand">
<label>Description</label>
<input type="text" class="form-control col-3 mx-2" placeholder="Description" v-model="brand.Description_brand">
<label>Image</label>
<input type="text" class="form-control col-3 mx-2" placeholder="Image" v-model="brand.Image_brand" >
</div>
<br />

<button class="btn btn-success" style="width: 90px;">Submit</button>
</form>
&nbsp;&nbsp;
<button type="button" class="btn btn-danger submit-btn" style="border-radius: 8px;margin-left:30%; margin-top: -4.25rem;  width: 90px;" @click="toggleModal">Cancel</button>

        </div>
</div>
</div>
</template>
<script>
export default {
data(){
    return {
brand : {},
brands :[]
    }
},
props:['showcreatebrand','toggleModal'],
methods : {
 async CreateBrand(){
    console.log('submitted');
  var response = await fetch("http://localhost:61917/api/test/insert/"+this.brand.Name_brand+"/"+this.brand.Description_brand+"/"+this.brand.Image_brand, {
    method: 'post',
    headers: {
      'Content-Type':'application/json'
    },
    body: JSON.stringify(this.brand)
  });
  this.brands.push(await response.json());
  window.location.reload(false);
},
},
}
</script>
<style scoped>
.bloc-modale{
    position: fixed;
    top:0;
    bottom:0;
    left:0;
    right:0;
    display: flex;
    justify-content: center;
    align-items: center;
    
}
.overlay{
    background: rgba(0,0,0,0.5);
    position: fixed;
    top:0;
    bottom:0;
    left:0;
    right:0;
}
.modale{
    background: #f1f1f1;
    color: #333;
    padding: 50px;
    position: fixed;
    top: 10% ;
    left:39%;
    width:400px;
    margin-left: -3rem;
}
.btn-modale {
    position: absolute;
    top:10px;
    right:10px;
}
</style>