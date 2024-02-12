<template>
  <div>
    <div class="wrapper">
      <div class="hvhelu" v-for="character in characters" :key="character.id">
        <div class="containerCard">
          <div class="myimg">
            <img :src="character.image" />
          </div>
          <div class="myTextContainer">
            <div class="section">
              <h2>name {{ character.name }}</h2>
              <div>
                {{ character.status }}
                {{ character.species }}
              </div>
            </div>
            <div class="section">
              <div class="section">
                <div class="text-grey">Last known location:</div>
                <div class="text-white">
                  {{ character.location.name }}
                </div>
              </div>
              <div class="section">
                <div class="text-grey">First seen in:</div>
                <div class="text-white">
                  {{ character.origin.name }}
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    characters: {
      type: Array,
      required: true,
    },
  },
  computed: {
    iconsearch() {
      return point;
    },
  },
};
</script>

<style>
.wrapper {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 4.5rem 0px;
  background: rgb(39, 43, 51);
  min-height: calc(50vh - 60px);
  flex-wrap: wrap;
}
.hvhelu {
  display: flex;
  -webkit-box-pack: center;
  justify-content: center;
  -webkit-box-align: center;
  align-items: center;
  flex-wrap: wrap;
  max-width: 1920px;
}
.containerCard {
  width: 600px;
  height: 220px;
  display: flex;
  overflow: hidden;
  background: rgb(60, 62, 68);
  border-radius: 0.5rem;
  margin: 0.75rem;
  box-shadow: rgba(0, 0, 0, 0.1) 0px 4px 6px -1px,
    rgba(0, 0, 0, 0.06) 0px 2px 4px -1px;
}
.myimg {
  flex: 2 1 0%;
  width: 100%;
}

.myimg img {
  width: 100%;
  height: 100%;
  margin: 0px;
  opacity: 1;
  transition: opacity 0.5s ease 0s;
  object-position: center center;
  object-fit: cover;
}

.myTextContainer {
  flex: 3 1 0%;
  position: relative;
  padding: 0.75rem;
  color: rgb(255, 255, 255);
  display: flex;
  flex-direction: column;
}

.myTextContainer .section:first-child {
  -webkit-box-pack: start;
  justify-content: flex-start;
}
.myTextContainer .section {
  flex: 1 1 0%;
  display: flex;
  flex-direction: column;
  -webkit-box-pack: center;
  justify-content: center;
}
.myTextContainer h2 {
  font-size: 1.5rem;
}
.text-grey {
  color: rgb(158, 158, 158);
}
.text-white {
  color: rgb(245, 245, 245);
}
</style>
