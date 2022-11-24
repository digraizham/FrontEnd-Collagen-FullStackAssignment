<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-buttons slot="start">
          <ion-button href="/tabs/page2">
            <img src="../../public/assets/svg/Vector.svg" alt="" />
          </ion-button>
        </ion-buttons>
        <ion-title>Registration Form</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content :fullscreen="true">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">Registration Form</ion-title>
        </ion-toolbar>
      </ion-header>
      <ion-list>
        <ion-item>
          <ion-label position="stacked">Nama Kolam</ion-label>
          <ion-input placeholder="Kolam 1" v-model="namakolam"></ion-input>
        </ion-item>
      </ion-list>
      <ion-list>
        <ion-item>
          <ion-label position="stacked">Lokasi Kolam</ion-label>
          <ion-input placeholder="Blok A" v-model="lokasikolam"></ion-input>
        </ion-item>
      </ion-list>
      <ion-list>
        <ion-item>
          <ion-label position="stacked">Jumlah Ikan</ion-label>
          <ion-input placeholder="200" v-model="jumlahikan"></ion-input>
        </ion-item>
      </ion-list>
      <ion-list>
        <ion-item>
          <ion-label position="stacked">Material Kolam</ion-label>
          <ion-select interface="action-sheet" v-model="materialkolam">
            <ion-select-option value="tanah">Tanah</ion-select-option>
            <ion-select-option value="beton">Beton</ion-select-option>
            <ion-select-option value="terpal">Terpal</ion-select-option>
          </ion-select>
        </ion-item>
      </ion-list>
      <ion-list>
        <ion-item>
          <ion-label position="stacked">Bentuk Kolam</ion-label>
          <ion-select interface="action-sheet" v-model="bentukkolam">
            <ion-select-option value="kotak">Kotak</ion-select-option>
            <ion-select-option value="bundar">Bundar</ion-select-option>
          </ion-select>
        </ion-item>
      </ion-list>

      <ion-button expand="block" @click="getFormValues()">Registrasi</ion-button>
    </ion-content>
  </ion-page>
</template>

<script lang="ts">
import { defineComponent, onMounted, ref } from "vue";
import {
  IonPage,
  IonHeader,
  IonToolbar,
  IonTitle,
  IonContent,
  IonButton,
  IonButtons,
  IonLabel,
  IonInput,
  IonSelect,
  IonSelectOption,
  IonItem,
  IonList,
} from "@ionic/vue";
import axios from "axios";
import { add } from "ionicons/icons";

export default defineComponent({
  name: "RegistrationPage",
  components: { IonHeader, IonToolbar, IonTitle, IonContent, IonPage, IonButton, IonButtons, IonLabel, IonInput, IonSelect, IonSelectOption },

  data() {
    return {
      namakolam: '',
      lokasikolam: '',
      jumlahikan: '',
      materialkolam: '',
      bentukkolam: '',
      
      
      material_options: [
        {key: 'tanah', value: 'Tanah'},
        {key: 'beton', value: 'Beton'},
        {key: 'terpal', value: 'Terpal'}
      ],
      shape_options: [
        {key: 'kotak', value: 'Kotak'},
        {key: 'bundar', value: 'Bundar'}
      ],
      getBackButtonText: () => {
        const win = window as any;
        const mode = win && win.Ionic && win.Ionic.mode;
        return mode === 'ios' ? 'Back' : '';
      }
    }
  },

  methods: {
    getFormValues() {
      // console.log(this.namakolam);
      // console.log(this.lokasikolam);
      // console.log(this.jumlahikan);
      // console.log(this.materialkolam);
      // console.log(this.bentukkolam);

      let pond = {
        "nama-kolam": this.namakolam,
        "lokasi-kolam": this.lokasikolam,
        "jumlah-ikan": this.jumlahikan,
        "material-kolam": this.materialkolam,
        "bentuk-kolam": this.bentukkolam,
      };
      console.log(pond);
      axios
              .post("http://127.0.0.1:5000/api/v1/registrasi", pond)
              .then((response) => {
                  console.log(response);
              })
              .catch((error) => {
                  console.log(error);
              });
    },
  },
  setup() {
    return {
      add
    };
  },
});
</script>

<style scoped>
ion-toolbar {
  display: flex;
  align-items: center;
}
ion-button {
  --background: #6c5ecf;
}
</style>
