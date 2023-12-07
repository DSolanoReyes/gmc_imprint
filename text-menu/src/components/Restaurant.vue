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
        </v-card>
      </v-col>

      <!--for fields-->
      <v-col lg="6" md="6" sm="12">
        <v-card elevation="2">
          <v-form v-model="form" @submit.prevent="onSubmit">
            <v-container>
              <!--user input-->
              <RestaurantComponent
                v-model="restaurant"
                v-model:restaurant-name="restaurant"
                :rules="[rules.counter]"
                maxlength="16"
                counter
                variant="underlined"
                hint="No More Than 16 Characters"
                label="Your Restaurant Name Here"
                style="margin-bottom: 2%"
              />

              <v-spacer></v-spacer>

              <!--location select-->
              <v-select
                placeholder="Select Text Location"
                variant="outlined"
                label="Select Location"
                style="margin-bottom: 2%"
                :items="positionList"
                :item-props="positionProps"
                v-model="position"
              ></v-select>

              <v-spacer></v-spacer>

              <!--font select-->
              <v-select
                label="Select Font"
                placeholder="Select..."
                variant="outlined"
                style="margin-bottom: 2%"
                :items="fontList"
                v-model="font"
              ></v-select>

              <v-spacer></v-spacer>

              <!--menu select-->
              <v-select return-object
                label="Select Menu Color"
                placeholder="Select..."
                variant="outlined"
                :items="fontColors"
                :item-props="itemProps"
                v-model="selectedImage"
                @click="changeImage"
              ></v-select>
            </v-container>
          </v-form>
        </v-card>
      </v-col>
    </v-row>
  </v-container>

</template>

<script>
import RestaurantComponent from './RestaurantComponent.vue'
import blackgoldcorners from '/src/assets/BlackGoldCorners.webp'
import blacksilvercorners from '/src/assets/BlackSilverCorners.webp'
import burgundygoldcorners from '/src/assets/BurgundyGoldCorners.webp'
import burgundysilvercorners from '/src/assets/BurgundySilverCorners.webp'

export default {
  components: { RestaurantComponent },
  mounted() {
    this.selectedImage = {ID: "0", name: "Gold With Black", colour: "#AE9A37", src: blackgoldcorners}
    this.fontColors[2].src = burgundygoldcorners
    this.fontColors[3].src = burgundysilvercorners
    this.fontColors[0].src = blackgoldcorners
    this.fontColors[1].src = blacksilvercorners
    this.position = {name: "Center Top", location: "flex-start"}
  },

  data () {
    return {
      restaurant: 'Fancy Restaurant',
      font: "Calligraffitti",
      position:"",
      imageColor:"",
      fontColors: [{
        ID: "0", name: "Gold With Black", colour: "#AE9A37", src: blackgoldcorners
      },{
        ID: "1", name: "Silver With Black", colour: "#827C7C", src: blacksilvercorners
      },{
        ID: "2", name: "Gold With Burgundy", colour: "#AE9A37", src: burgundygoldcorners
      },{
        ID: "3", name: "Silver With Burgundy", colour: "#827C7C", src: burgundysilvercorners
      }],

      fontList: ["Calligraffitti", "Dancing Script", "Delius Swash Caps", "Homemade Apple", "Junge",
        "La Belle Aurore", "Patrick Hand", "Rochester", "Sue Ellen Francisco", "Waiting for the Sunshine"],
      positionList: [{
        name: "Center Top", location: "flex-start"
      },{
        name: "Center", location: "center"
      },{
        name: "Center Bottom", location: "flex-end"
      }],

      selectedImage: {src: blackgoldcorners},

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
      if (this.selectedImage.ID === 0){
        this.selectedImage = blackgoldcorners
      } else if (this.selectedImage.ID === 1){
        this.selectedImage = blacksilvercorners
      } else if (this.selectedImage.ID === 2){
        this.selectedImage = burgundygoldcorners
      } else if (this.selectedImage.ID === 3){
        this.selectedImage = burgundysilvercorners
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
  height: 75px;
  width: 325px;
  text-align: center;
  margin-top: 100px;
  margin-bottom: 100px;
}

@font-face {
  font-family: "Calligraffitti";
  src: url("@/assets/fonts/Calligraffitti-Regular.ttf");
}

@font-face {
  font-family: "Dancing Script";
  src: url("@/assets/fonts/DancingScript-Regular.ttf");
}

@font-face {
  font-family: "Delius Swash Caps";
  src: url("@/assets/fonts/DeliusSwashCaps-Regular.ttf");
}

@font-face {
  font-family: "Homemade Apple";
  src: url("@/assets/fonts/HomemadeApple-Regular.ttf");
}

@font-face {
  font-family: "Junge";
  src: url("@/assets/fonts/Junge-Regular.ttf");
}

@font-face {
  font-family: "La Belle Aurore";
  src: url("@/assets/fonts/LaBelleAurore-Regular.ttf");
}

@font-face {
  font-family: "Patrick Hand";
  src: url("@/assets/fonts/PatrickHand-Regular.ttf");
}

@font-face {
  font-family: "Rochester";
  src: url("@/assets/fonts/Rochester-Regular.ttf");
}

@font-face {
  font-family: "Sue Ellen Francisco";
  src: url("@/assets/fonts/SueEllenFrancisco-Regular.ttf");
}

@font-face {
  font-family: "Waiting for the Sunshine";
  src: url("@/assets/fonts/WaitingfortheSunrise-Regular.ttf");
}

</style>
