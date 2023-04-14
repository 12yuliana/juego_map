
<template>
    
      <div class="medio">
        <img class="img" ref="map" id="map" src="../assets/treasuremap.png" alt="">
      </div>
      <div  ref="distance" id="distance"></div>

  </template>
    <style scoped>  
  
    .medio{
        background-color: rgba(238, 228, 228, 0.459);
        height: 70vh;
        display: flex;
    }
    .img{
        margin: auto;
     
    }


    
    </style>
  
  <script>
  export default {
      name:"juegO",
    data() {
      return {
        target: {
          x: 0,
          y: 0,
        },
        clicks: 0,
      };
    },
    mounted() {
      const WIDTH = 400;
      const HEIGHT = 400;
  
      this.target.x = this.getRandonNumber(WIDTH);
      this.target.y = this.getRandonNumber(HEIGHT);
  
      this.$refs.map.addEventListener('click', (e) => {
        this.clicks++;
        let distance = this.getDistancia(e, this.target);
        let distanceHint = this.getDistanciaHint(distance);
        this.$refs.distance.innerHTML = `<h1>${distanceHint}</h1>`;
        if (distance < 20) {
          alert(`¡Has encontrado el tesoro en ${this.clicks} clicks!`);
          location.reload();
        }
      });
    },
    methods: {
      getRandonNumber(size) {
        return Math.floor(Math.random() * size);
      },
      getDistancia(e, target) {
        let diffX = e.offsetX - target.x;
        let diffY = e.offsetY - target.y;
        return Math.sqrt(diffX * diffX + diffY * diffY);
      },
      getDistanciaHint(distance) {
        if (distance < 30) {
          return 'Muy caliente';
        } else if (distance < 40) {
          return 'Punto caliente';
        } else if (distance < 60) {
          return 'Caliente';
        } else if (distance < 100) {
          return 'Tibio';
        } else if (distance < 180) {
          return 'Frio';
        } else if (distance < 360) {
          return 'Realmente frio';
        } else {
          return 'Congelado';
        }
      },
    },
  };
  </script>
  
  <!-- Add "scoped" attribute to limit CSS to this component only -->

  