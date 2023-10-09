<template>
  <v-container fluid="">
    <v-row>
      <!--for images-->
      <v-col lg="6">
        <v-card elevation="1">
<!--          <v-img-->
<!--          src="../assets/blank black menu.png">-->
<!--          </v-img>-->
          <div id="image-frame" style="margin: 0; padding: 0">
            <div id="image-frame-menu">
              <p>testing</p>
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
      <v-col lg="6">
        <v-card elevation="2">
          <v-form v-model="form" @submit.prevent="onSubmit">
            <v-container>
              <!--user name input-->
              <v-text-field
                v-model="restaurantText"
                type="text"
                label="Your Restaurant Name Here"
                variant="underlined"
                hint="No more than 16 Characters">
              </v-text-field>



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

              <v-select
                label="select thing"
                placeholder="select..."
                variant="outlined"
                v-model="selectedTextPosition"
                :items="positions"
                item-text="textName"
                return-object filled>
              </v-select>

              <!--font select-->
              <v-select
                label="Select Font"
                placeholder="Select..."
                variant="outlined"
                :items="fontList"
                v-model="font"
              ></v-select>
              <p id="menu-font">Relaxing in basins at the end of inlets terminates the endless tests from the box</p>

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

export default {
  data () {
    return {
      font: "arial",
      fontList: ["Arial", "Calibri", "Roboto", "Times New Roman"],
      selectedTextPosition: {
        textName: 'Top',
        textValue: 'flex-start'
      },
      positions: [{
        textName: 'Top',
        textValue: 'flex-start',
      },{
        textName: 'Middle',
        textValue: 'center',
      },{
        textName: 'Bottom',
        textValue: 'flex-end'
      }]
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
