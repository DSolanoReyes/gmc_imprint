<template>
  <v-container fluid="">
    <v-row>
      <!--for images-->
      <v-col lg="6" md="6" sm="12">
        <v-card elevation="1">
          <div id="image-frame" :style="{ backgroundImage: `url(${selectedImage.src})`}" style="margin: 0; padding: 0;)">
            <div id="image-frame-menu">
              <h1 type="text" id="menu-font" style="color: #827C7C" v-if="selectedImage.ID === '1' || selectedImage.ID === '3'">{{ restaurant }}</h1>
              <h1 type="text" id="menu-font" style="color: #AE9A37" v-else-if="selectedImage.ID === '0' || selectedImage.ID === '2'">{{ restaurant }}</h1>
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
                v-model="selectedImage"
                @click="changeImage"
              ></v-select>

              <h6>imagecolor.src</h6>
              {{imageColor.src}}

              <h6>imagecolor.id</h6>
              {{imageColor.ID}}

              <h6>selectedImage</h6>
              {{selectedImage}}

              <h6>selectedImage.src</h6>
              {{selectedImage.src}}

              <h6>selectedImage.ID</h6>
              {{selectedImage.ID}}

              <v-card-actions>
                <v-spacer></v-spacer>
                <v-btn
                  color="primary"
                  @click="">
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
    this.selectedImage = {ID: "0", name: "Gold With Black", colour: "#AE9A37", src: blankblack}
    this.fontColors[2].src = blankburgandy
    this.fontColors[3].src = blankburgandy
    this.fontColors[0].src = blankblack
    this.fontColors[1].src = blankblack
    this.position = {name: "Center Top", location: "flex-start"}
  },

  data () {
    return {
      restaurant: 'Fancy Restaurant',
      font: "Arial",
      position:"",
      imageColor:"",
      fontColors: [{
        ID: "0", name: "Gold With Black", colour: "#AE9A37", src: blankblack
      },{
        ID: "1", name: "Silver With Black", colour: "#827C7C", src: blankblack
      },{
        ID: "2", name: "Gold With Burgundy", colour: "#AE9A37", src: blankburgandy
      },{
        ID: "3", name: "Silver With Burgundy", colour: "#827C7C", src: blankburgandy
      }],

      fontList: ["Arial", "Calibri", "Roboto", "Times New Roman"],
      positionList: [{
        name: "Center Top", location: "flex-start"
      },{
        name: "Center", location: "center"
      },{
        name: "Center Bottom", location: "flex-end"
      }],
      selectedImage: {src: blankblack},
      rules: {
        counter: value => value.length <= 16 || 'Max 16 Characters'
      }
    }
  },
  methods: {
    itemProps (fontColors) {
      return {
        title: fontColors.name,
        src: fontColors.src,
        value: fontColors.ID
      }
    },
    changeImage (){
      if (this.selectedImage.ID === 0 || this.selectedImage.ID === 1){
        this.selectedImage = blankblack
      } else if (this.selectedImage.ID === 2 || this.selectedImage.ID === 3){
        this.selectedImage = blankburgandy
      }
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
  font-family: v-bind(font);
}

#image-frame{
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
