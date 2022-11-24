<template>
  <ion-page>
    <ion-header :translucent="true">
      <ion-toolbar>
        <ion-title>Kolam</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content :fullscreen="true">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">Kolam</ion-title>
        </ion-toolbar>
      </ion-header>
      <div class="status">
        <ion-grid>

          <ion-row v-for="(pond, index) in ponds" v-bind:key="index">
            <ion-col>
              <div class="card-pond">
                <div class="header-pond">
                  <h3>{{pond.namakolam}}</h3>
                  <h6>{{pond.lokasikolam}}</h6>
                  <p :class="[ pond.isActive == 1 ? 'green' : 'red' ]">{{pond.status}}</p>
                </div>
                <div>
                  <div class="content-pond">
                    <img src="../../public/assets/svg/CalendarPlus.svg" alt="">
                    <p>{{ date(pond.build_at) }}</p>
                  </div>
                  <div class="content-pond">
                    <img src="../../public/assets/svg/Timesheet.svg" alt="">
                    <p>{{ findDay(pond.build_at) }} Hari</p>
                  </div>
                  <div class="content-pond">
                    <img src="../../public/assets/svg/WholeFish.svg" alt="">
                    <p>{{pond.jumlahikan}} Ekor</p>
                  </div>
                </div>
              </div>
            </ion-col>
          </ion-row>
  
        </ion-grid>
      </div>
    </ion-content>
    <ion-fab vertical="bottom" horizontal="end" slot="fixed" style="margin-right: 15px;">
      <ion-fab-button href="/registrationpage"><span style="font-size: 60px; font-weight:bolder">+</span></ion-fab-button>
    </ion-fab>
  </ion-page>
</template>

<script lang="ts">
import { IonContent, IonFab, IonFabButton, IonHeader, IonPage, IonTitle, IonToolbar } from "@ionic/vue";
import { defineComponent, onMounted, ref } from "vue";
import axios from 'axios';
import { add } from "ionicons/icons";

export default defineComponent({
  name: "PageSecond",
  components: {
    IonContent,
    IonHeader,
    IonPage,
    IonTitle,
    IonToolbar,
  },
  methods: {
    date(date: string) {
      const d = new Date(date);
      const month = d.getMonth() + 1;
      const day = d.getDate();
      const year = d.getFullYear();
      return `${day}-${month}-${year}`;
    },
    findDay(date: string) {
      const d = new Date(date);
      const diff = new Date().getTime() - d.getTime();
      return Math.floor(diff / (1000 * 60 * 60 * 24));
    },
  },
  setup() {
    const ponds = ref();
    let day;
    onMounted(async () => {
      const response = await axios.get('http://127.0.0.1:5000/api/v1/pondinfo')
      ponds.value = response.data
      console.log(response.data)
    });
    return {
      add, ponds
    }
  }
});
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Poppins&display=swap');
* {
  font-family: 'Poppins', sans-serif;
}
ion-content{
  --ion-background-color:#1F1D2B;
}
.section-title {
  margin-left: 12px;
  font-weight: bold;
  margin-top: 20px;
}
.kolam-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin: 20px 12px;
  font-weight: bold;
}
.kolam-header img {
  width: 30px;
}
.kolam-header img:nth-child(2) {
  filter: invert(100%);
}
.card-pond {
  background-color: #fff;
  color: #000;
  width: 100%;
  padding: 20px 15px;
  border-radius: 15px;
  margin-bottom: 20px;
}
.header-pond {
  display: flex;
  justify-content: space-between;
  font-weight: bold;
  align-items: center;
  border-bottom: 3px solid #333;
}
.header-pond h3 {
  font-weight: bold;
  font-size: 25px;
  width: 60%;
}
.header-pond p {
  padding: 10px 15px;
  border-radius: 5px;
  font-size: 18px;
  color: #fff;
}
.content-pond {
  display: flex;
  align-items: center;
  gap: 10px;
  margin-bottom: -20px;
}
.content-pond img {
  height: 30px;
}
.green {
  background-color: #1B7C1A;
}
.red {
  background-color: #952229;
}
.blue {
  background-color: #952229;
}

</style>
