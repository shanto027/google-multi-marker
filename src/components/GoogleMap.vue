<template>
  <div>
    <br />
    <h1>Vue Js Add Multiple Markers on Google Maps</h1>

    <gmap-map :center="center" :zoom="12" style="width: 100%; height: 400px">
      <gmap-marker
        :key="index"
        v-for="(m, index) in markers"
        :position="m"
        :clickable="true"
        @click="openWindow"
      />
      <gmap-info-window
        @closeclick="window_open = false"
        :opened="window_open"
        :position="infowindow"
        :options="{
          pixelOffset: {
            width: 0,
            height: -35,
          },
        }"
      >
        Pump Information<br />
        Unique Identifier: 74Hj8562<br />
        Location : Anta<br />
        Installation date: 07 Dec 2021
      </gmap-info-window>
    </gmap-map>
  </div>
</template>
 
<script>
export default {
  name: "GoogleMap",
  data() {
    return {
      center: { lat: 45.508, lng: -73.587 },
      markers: [],
      currentPlace: null,
      info_marker: null,
      infowindow: { lat: 23.633841, lng: 89.066856 },
      window_open: false,
    };
  },

  mounted() {
    this.geolocate();
  },

  methods: {
    openWindow() {
      console.log(this);
      this.window_open = true;
    },

    setPlace(place) {
      this.currentPlace = place;
    },
    geolocate: function () {
      navigator.geolocation.getCurrentPosition((position) => {
        this.center = {
          lat: position.coords.latitude,
          lng: position.coords.longitude,
        };
      });

      this.markers = [
        {
          lat: 23.633841,
          lng: 89.066856,
          label: "Jhenaidah",
        },
        {
          lat: 24.40349,
          lng: 90.772301,
          label: "Kishoreganj",
        },
      ];
    },
  },
};
</script>


