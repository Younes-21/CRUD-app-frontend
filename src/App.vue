<template>
    <div>
    <div>
              <!-- <ul>
        <li v-for="(val, key) in brands" :key="key">
        {{ key }} : {{ val }}
        </li>
        </ul>--></div>

    

   <center> <h1> BrandList </h1></center>
  <center><div>        <button @click="toggleModal" class="btn btn-success" style="border: #00608d;border-radius: 5px;height: 40px;">Create brand</button>
</div></center> 
<br />
<div v-if="showcreatebrand"><CreateBrand v-bind:showcreatebrand="showcreatebrand" v-bind:toggleModal="toggleModal" /></div>
<div v-if="showupdatebrand"><UpdateBrand v-bind:showupdatebrand="showupdatebrand" v-bind:brandtoedit="brandtoedit" v-bind:toggleModalUpdate="toggleModalUpdate" /></div>
    <table border="1px" class="table table-striped">
       <thead>
       <tr>
            <td>Id brand</td>
            <td>Brand name</td>
            <td>Description</td>
            <td>Image</td>
            <td>Actions</td>
        </tr>
        </thead>
        <tbody>
        <tr v-for="item in brands" :key="item.Id_brand">
            <td>{{item.Id_brand}}</td>
            <td>{{item.Name_brand}}</td>
            <td>{{item.Description_brand}}</td>
            <td>{{item.Image_brand}}</td>
            <td>
                <button @click="getoneBrand(item)" class="btn btn-warning">
                    Update
                </button>  
                &nbsp;
                <button class="btn btn-danger" @click="Delete(item)">
                    Delete
                </button>
            </td>

        </tr>
        </tbody>
    </table>

    
    </div>
</template>

<script>
import axios from "axios";
import CreateBrand from "./components/Modals/CreateBrand.vue";
import UpdateBrand from "./components/Modals/UpdateBrand.vue";
export default {
    data() {
        return {
            brands: [],
            brand: {},
            showcreatebrand : false,
            showupdatebrand : false,
             brandtoedit : [
               /* 'Id_brand': 2,
                'Name_brand' : 'test',
                'Description_brand':'same',
                'Image_brand' :'testttt'       */   ],
             
        }
    },
   
    methods: {
        toggleModal: function(){
  this.showcreatebrand = !this.showcreatebrand;
},
 toggleModalUpdate: function(){
  this.showupdatebrand = !this.showupdatebrand;
},
              async Delete(item) {
            console.log(item.Id_brand);
            var response = await fetch("http://localhost:61917/api/test/delete/" + item.Id_brand, {
                method: "delete",
                headers: {
                    "Content-Type": "application/json"
                },
                body: JSON.stringify(this.brand)
            });
            this.brands.push(await response.json());
            window.location.reload(false);
        },
          // Get brand data by id to edit it
 async getoneBrand(item){
   console.log(item.Id_brand);
   var response = await fetch("http://localhost:61917/api/test/" + item.Id_brand);
     /* console.log("rrrr111",response);*/
    //   console.log("rrrr",await response.json());
    // if(response.status == 200){
        this.brandtoedit = await response.json();
    // }

   
  /* console.log('0000',this.brandtoedit);*/
   this.toggleModalUpdate();
},
     async getBrand() {
        axios
            .get("http://localhost:61917/api/test/")
            .then(result => {
            this.brands = result.data;
        });
    },
    },
    components: { CreateBrand , UpdateBrand},
    created() {
        this.getBrand();  
                    }
}
</script>