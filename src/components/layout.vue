<template>
  <div>
    <div class="hero">
      <div class="hero__content">
        <h1>Localizzatore Incendi</h1>
        <h3>Cerca un giorno specifico per sapere dove ci sono stati incendi</h3>
      </div>
      <div>
        <img src="../assets/fire-bg.jpg" class="img-back" alt="Fire Image">
      </div>
    </div>
    <Map></Map>
  </div>
</template>

<script>
import Map from '../components/map.vue'

export default {
  name: 'Layout',
  components: {
    Map
  }
}
</script>

<style>
.hero{
  position: relative;
}

.hero__content{
  color: #fff;
  width: 100%;
  height: 300px;
  position: absolute;
  text-align: center;
  background: linear-gradient(180deg, rgba(0,0,0,0.1) 25%, rgba(0,0,0,1) 100%);
}

.hero__content h1{
  font-size: 45px;
  position: absolute;
  left: 50%;
  transform: translateX(-50%);
  bottom: 10%;
}

.hero__content h3{
  font-size: 20px;
  position: absolute;
  left: 50%;
  transform: translateX(-50%);
  bottom: 5%;
}

.img-back{
  object-fit: cover;
  width:100%;
  height: 300px;
  overflow: hidden;
}
</style>
