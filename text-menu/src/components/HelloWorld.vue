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
              <h1 id="menu-font">{{ restaurant }}</h1>
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

<!--              <v-text-field
                v-model="title"
                type="text"
                @input=""
                :rules="[rules.counter]"
                maxlength="16"
                counter
                label="Your Restaurant Name Here"
                variant="underlined"
                hint="No more than 16 Characters"
              ></v-text-field>-->



              <!--location select-->
<!--              <v-select
                label="Select Location"
                placeholder="Select..."
                variant="outlined"

              >
                <v-item>
                  water
                </v-item>
              </v-select>-->

              <v-select return-object

                placeholder="select..."
                variant="outlined"
                :items="positionList"
                v-model="selectedTextPosition"
              ></v-select>

<!--              <p id="menu-font">Relaxing in basins at the end of inlets terminates the endless tests from the box</p>-->
              <!--font select-->
              <v-select
                label="Select Font"
                placeholder="Select..."
                variant="outlined"
                :items="fontList"
                v-model="font"
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
      font: "arial",
      fontList: ["Arial", "Calibri", "Roboto", "Times New Roman"],
      selectedTextPosition: "center",
      positionList: ["center", "flex-start", "flex-end"],

      rules: {
        counter: value => value.length <= 16 || 'Max 16 Characters'
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
  background-image: url("../assets/blank black menu.png");
  height: 600px;
  width: 100%;
  background-size: contain;
  background-repeat: no-repeat;
  background-position: center;


  display: flex;
  justify-content: center;
  align-items: v-bind(selectedTextPosition);
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
