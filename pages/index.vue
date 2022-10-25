<template>
  <div data-app>
    <v-card class="mx-auto my-12 card__absolute" max-width="674">
      <v-card-title style="text-align: center;">
        <h5 style="text-align: center;">Portal Informasi Data Pelaku Usaha Ekonomi Kreatif</h5>
      </v-card-title>
      <v-autocomplete class="__select-modif" v-model="provinsiKd" :items="pelakuUsaha" item-text="nama"
        item-value="provinsiKd" dense chips small-chips @change="setActiveMap">
      </v-autocomplete>
    </v-card>

    <div id="map-wrap" style="height: 100vh;z-index: -1;">
      <client-only>
        <l-map :zoom=5 :center="[4.626344251568086, 114.79365521475563]">
          <l-tile-layer url="http://{s}.tile.osm.org/{z}/{x}/{y}.png"></l-tile-layer>
          <!-- <l-marker ref="popup" @add="openPopup" :lat-lng="[-3.784608312765171, 122.49534814876023]">
            <l-popup>
              <h3 style="text-align: center;">ProvKendari</h3>
              <p>Lorem ipsum dolor, sit amet consectetur adipisic</p>
            </l-popup>
          </l-marker> -->
          <div v-for="(item, index) in provinsi" :key="index">
            <div v-if="active">
              <div v-if="item.isActive">
                <l-marker ref="popup" @add="openPopup" :lat-lng="item.lokasi">
                  <l-popup class="popup d-flex justify-center">
                    <h3 style="text-align: center;">{{ item.nama }} </h3>

                    <p style="text-align: center;">
                      <span style="font-size: 21px;color: salmon;">{{ item.count }}</span> Pelaku Ekraf
                    </p>
                    <NuxtLink to="/pelaku-usaha" small
                      class="btn-modif v-btn v-btn--is-elevated v-btn--has-bg theme--light v-size--small">
                      Lihat Daftar Pelaku Ekraf
                    </NuxtLink>
                  </l-popup>
                </l-marker>
              </div>
              <div v-else>
                <l-marker :lat-lng="item.lokasi">
                  <l-popup class="popup">
                    <p style="text-align: center;font-size:21px">{{ item.nama }} </p>
                    <p style="text-align: center;">
                      <span style="font-size: 21px;color: salmon;">{{ item.count }}</span> Pelaku Ekraf
                    </p>
                  </l-popup>
                </l-marker>
              </div>
            </div>
          </div>
          <!-- <div v-for="(item, index) in provinsi" :key="index">
            <l-marker ref="popup" @add="openPopup" :lat-lng="[-3.784608312765171, 122.49534814876023]">
              <l-popup>
                <h3 style="text-align: center;">ProvKendari</h3>
                <p>Lorem ipsum dolor, sit amet consectetur adipisic</p>
              </l-popup>
            </l-marker>
          </div> -->
        </l-map>
      </client-only>
    </div>
  </div>

</template>
<style>
.group {
  display: flex;
  flex: 1;
  justify-content: space-around;
}

.map-popup {
  width: 600px;
}
</style>
<script>
import './index.css'
export default {
  name: 'IndexPage',
  methods: {
    setActiveMap: function () {
      this.active = false
      this.provinsi.forEach((pv) => {
        if (pv.kode === this.provinsiKd) {
          console.log("active bro", pv.kode, this.provinsiKd)
          pv.isActive = true;
          // console.log(this.provinsi)
        } else {
          pv.isActive = false;
        }
      })
      // this.active = true
      console.log(this.provinsi);
    },
    openPopup: function (event) {
      this.$nextTick(() => {
        event.target.openPopup();
      })
    },
  },
  updated() {
    this.active = true
  },
  mounted() {
    // console.log(this.provinsi);
    this.pelakuUsaha.forEach((pu) => {
      this.dataPelakuUsaha.push(pu)
    });
  },
  data: () => ({
    active: true,
    provinsiKd: null,
    dataPelakuUsaha: [],
    provinsi: [
      {
        nama: "kalimantan barat",
        kode: "01",
        lokasi: [-0.26474840622706436, 110.93113890218173],
        isActive: false,
        count: 50
      },

      {
        nama: "sulawesi selatan",
        kode: "02",
        lokasi: [0.5661557452089007, 123.07062631039902],
        isActive: false,
        count: 10
      },
      {
        nama: "jawa timur",
        lokasi: [-7.4228311805805545, 111.91314490446791],
        kode: "03",
        isActive: false,
        count: 100
      },
      {
        nama: "Medan",
        kode: "04",
        lokasi: [3.7159012715700945, 98.66627506176431],
        isActive: false,
        count: 50
      },
    ],
    pelakuUsaha: [
      {
        nama: "usaha kalbar",
        lokasi: [-0.26474840622706436, 110.93113890218173],
        provinsiKd: "01"
      },
      {
        nama: "usaha sulsel",
        lokasi: [0.5661557452089007, 123.07062631039902],
        provinsiKd: "02"
      },
      {
        nama: "usaha jatim",
        lokasi: [-7.4228311805805545, 111.91314490446791],
        provinsiKd: "03"
      }, {
        nama: "usaha medan",
        lokasi: [-7.4228311805805545, 111.91314490446791],
        provinsiKd: "04"
      },
      {
        nama: "usaha medan baru bro",
        lokasi: [-7.4228311805805545, 111.91314490446791],
        provinsiKd: "04"
      },
    ],
    values: null,
  }),
}
</script>
