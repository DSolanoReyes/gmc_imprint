<template>
  <v-container fluid="">
    <v-row>
      <!--for images-->
      <v-col lg="6" md="6" sm="12">
        <v-card elevation="1">
<!--          <v-img-->
<!--          src="../assets/blank black menu.png">-->
<!--          </v-img>-->
          <div id="image-frame" style="margin: 0; padding: 0">
            <div id="image-frame-menu">
              <h1 type="text" id="menu-font" >{{ restaurant }}</h1>
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

              <!--location select-->
              <v-select return-object
                placeholder="Select Text Location"
                variant="outlined"
                :items="positionList"
                :item-props="positionProps"
                v-model="positionList.value"
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

export default {
  components: { RestaurantComponent },
  data () {
    return {
      restaurant: '',
      font: "Arial",
      fontColors: [{
        ID: "0", name: "Gold With Black", colour: "#AE9A37", src: "../assets/blank black menu.png"
      },{
        ID: "1", name: "Silver With Black", colour: "#827C7C", src: ""
      },{
        ID: "2", name: "Gold With Burgundy", colour: "#AE9A37", src: "../assets/blank burgandy menu.jpg"
      },{
        ID: "3", name: "Silver With Burgundy", colour: "#827C7C", src: ""
      }],

      fontList: ["Arial", "Calibri", "Roboto", "Times New Roman"],

      positionList: [{
        name: "Center Top", location: "flex-start"
      },{
        name: "Center", location: "center"
      },{
        name: "Center Bottom", location: "flex-end"
      }],

      rules: {
        counter: value => value.length <= 16 || 'Max 16 Characters'
      }
    }
  },
  methods: {
    itemProps (fontColors) {
      return {
        title: fontColors.name,
      }
    },
    positionProps (positionList) {
      return {
        title: positionList.name,
        value: positionList.location
      }
    },
  },
  computed: {
    cssProps() {
      return{
        'color': this.fontColors.colour
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
  background-image: url("../assets/blank black menu.png");
  height: 600px;
  width: 100%;
  background-size: contain;
  background-repeat: no-repeat;
  background-position: center;


  display: flex;
  justify-content: center;
  align-items: v-bind(positionList);
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
