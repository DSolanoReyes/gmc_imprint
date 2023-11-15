<template>
  <v-container fluid="">
    <v-row>
      <!--for images-->
      <v-col lg="6" md="6" sm="12">
        <v-card elevation="1">
          <div id="image-frame" :style="{ backgroundImage: `url(${selectedImage})` }"  style="margin: 0; padding: 0;)">
            <div id="image-frame-menu">
              <h1 type="text" id="menu-font" style="color: #827C7C" v-if="fontColors.id === 1 || 3">{{ restaurant }}</h1>
              <h1 type="text" id="menu-font" style="color: #AE9A37" v-else-if="fontColors.id === 0 || 2">{{ restaurant }}</h1>
            </div>
          </div>

          <v-divider></v-divider>

          <!--bottom buttons for images-->
          <v-card-actions>
            <v-btn
              align="left"
              prepend-icon="mdi-arrow-left">
              Previous
            </v-btn>
            <v-spacer></v-spacer>
            <v-btn
              align="right"
              append-icon="mdi-arrow-right">
              Next
            </v-btn>
          </v-card-actions>
        </v-card>
      </v-col>

      <!--for fields-->
      <v-col lg="6" md="6" sm="12">
        <v-card elevation="2">
          <v-form v-model="form" @submit.prevent="onSubmit">
            <v-container>
              <!--user name input-->
              <RestaurantComponent
                v-model="restaurant"
                v-model:restaurant-name="restaurant"
                :rules="[rules.counter]"
                maxlength="16"
                counter
                variant="underlined"
                hint="No More Than 16 Characters"
                label="Your Restaurant Name Here"
              />

              {{position}}

              <!--location select-->
              <v-select
                placeholder="Select Text Location"
                variant="outlined"
                label="Select Location"
                :items="positionList"
                :item-props="positionProps"
                v-model="position"
              ></v-select>

              <!--font select-->
              <v-select
                label="Select Font"
                placeholder="Select..."
                variant="outlined"
                :items="fontList"
                v-model="font"
              ></v-select>

              <v-select return-object
                label="Select Menu Color"
                placeholder="Select..."
                variant="outlined"
                :items="fontColors"
                :item-props="itemProps"
                v-model="imageColor"
              ></v-select>


              <v-card-actions>
                <v-spacer></v-spacer>
                <v-btn
                  color="primary"
                  @click="submit">
                  Submit
                </v-btn>
              </v-card-actions>
            </v-container>
          </v-form>
        </v-card>
      </v-col>
    </v-row>
  </v-container>

</template>

<script>
import {right} from "core-js/internals/array-reduce";
import RestaurantComponent from './RestaurantComponent.vue'
import blankblack from '/src/assets/blankblackmenu.png'
import blankburgandy from '/src/assets/blankburgandymenu.jpg'
export default {
  components: { RestaurantComponent },
  mounted() {
    this.selectedImage = this.blankblack
  },

  data () {
    return {
      restaurant: '',
      font: "Arial",
      position:"",
      imageColor:"",
      fontColors: [{
        ID: "0", name: "Gold With Black", colour: "#AE9A37", src: "../assets/blankblackmenu.png"
      },{
        ID: "1", name: "Silver With Black", colour: "#827C7C", src: "../assets/blankblackmenu.png"
      },{
        ID: "2", name: "Gold With Burgundy", colour: "#AE9A37", src: "../assets/blankburgandymenu.jpg"
      },{
        ID: "3", name: "Silver With Burgundy", colour: "#827C7C", src: "../assets/blankburgandymenu.jpg"
      }],

      fontList: ["Arial", "Calibri", "Roboto", "Times New Roman"],

      positionList: [{
        name: "Center Top", location: "flex-start"
      },{
        name: "Center", location: "center"
      },{
        name: "Center Bottom", location: "flex-end"
      }],
      blankblack,
      blankburgandy,
      selectedImage:null,
      rules: {
        counter: value => value.length <= 16 || 'Max 16 Characters'
      }
    }
  },
  methods: {
    itemProps (fontColors) {
      return {
        title: fontColors.name,
        value: fontColors.ID
      }
    },
    ChangeImage(){

    },
    positionProps (positionList) {
      return {
        title: positionList.name,
        value: positionList.location
      }
    }
  }

}
</script>

<style>
#menu-font{
  /*background-color: var(--bg-hover-color);*/
  font-family: v-bind(font);
}

#image-frame{
  //background-image: url("../assets/blankburgandymenu.jpg");
  height: 600px;
  width: 100%;
  background-size: contain;
  background-repeat: no-repeat;
  background-position: center;
  background-image: v-bind(selectedImage);


  display: flex;
  justify-content: center;
  align-items: v-bind(position);
}

#image-frame-menu{
  background-color: red;
  height: 75px;
  width: 325px;
  text-align: center;
  margin-top: 100px;
  margin-bottom: 100px;
}
</style>
