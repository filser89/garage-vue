<template>
  <div id="app">
    <div class="app">
      <div class="garage">
        <div
          class="garage-image"
          style="
            background: linear-gradient(
                rgba(255, 255, 255, 0.5),
                rgba(255, 255, 255, 0.4)
              ),
              url('images/garage.jpg');
          "
        >
          <div class="garage-logo">
            <img src="images/white_logo_red_circle.png" alt="" />
          </div>
        </div>
        <div class="garage-info">
          <h3 class="text-center">Le Wagon</h3>
          <div class="garage-description">
            Our garage is the best. Reasonable price, always on time, we are the
            awesome (and fictionnal).
          </div>
          <div class="text-center">
            <form class="car-form" id="new-car" @submit.prevent="addCar()">
              <input
                id="brand"
                type="text"
                class="form-control"
                placeholder="Ferrari"
              />
              <input
                id="model"
                type="text"
                class="form-control"
                placeholder="308 GTS"
              />
              <input
                id="plate"
                type="text"
                class="form-control"
                placeholder="56E-478"
              />
              <input
                id="owner"
                type="text"
                class="form-control"
                placeholder="Thomas Magnum"
              />
              <input type="submit" class="btn btn-cta" value="Add a Car" />
            </form>
          </div>
        </div>
      </div>
      <div class="cars-list">
        <!-- NOTE: The team designer left you this template for a car. Enjoy! -->

        <div class="car" v-for="(car, index) in cars" v-bind:key="car.id">
          <div class="car-image">
            <img :src="srcLinks[index]" />
          </div>
          <div class="car-info">
            <h4>{{ car.brand }} {{ car.model }}</h4>
            <p><strong>Owner:</strong> {{ car.owner }}</p>
            <p><strong>Plate:</strong> {{ car.plate }}</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      cars: [],
    };
  },
  methods: {
    addCar() {
      fetch("https://wagon-garage-api.herokuapp.com/777/cars", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({
          brand: "PEUGEOT",
          model: "106",
          owner: "ssaunier",
          plate: "123AZ56",
        }),
      })
        .then((response) => response.json())
        .then(() => {
          this.getCars();
        });
    },
    getCars() {
      fetch("https://wagon-garage-api.herokuapp.com/777/cars")
        .then((response) => response.json())
        .then((data) => {
          this.cars = data;
          console.log(this.cars);
        });
    },
  },
  mounted() {
    this.getCars();
  },
  computed: {
    srcLinks() {
      return this.cars.map(
        (car) => `http://loremflickr.com/280/280/${car.brand} ${car.model}`
      );
    },
  },
};
</script>
// fetch garage api add car to the garage

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.app {
  display: flex;
  height: 100vh;
}
.garage {
  width: 25%;
  background-color: white;
}
.garage-image {
  background-repeat: no-repeat;
  height: 200px;
  display: flex;
  align-items: flex-end;
  justify-content: center;
}
.garage-logo {
  width: 100px;
  border-radius: 50%;
  border: 2px solid white;
  margin-bottom: -50px;
}
.garage-logo img {
  width: 100%;
}
.garage-info {
  margin-top: 60px;
}
.garage-info .btn-cta {
  background-color: transparent;
  border: 1px solid black;
  color: black;
  font-weight: bold;
  letter-spacing: 2px;
  padding: 10px;
  border-radius: 3px;
}
.garage-info .btn-cta:hover {
  background-color: black;
  color: white;
}
.garage-description {
  padding: 30px;
  color: gray;
}
.cars-list {
  width: 75%;
  background-color: lightgray;
  padding: 20px;
  overflow: scroll;
}
.car {
  display: flex;
  background-color: white;
  margin-bottom: 10px;
  opacity: 0.9;
}
.car:hover {
  opacity: 1;
}
.car-image {
  width: 140px;
}
.car-image img {
  width: 100%;
}
.car-info {
  padding: 10px;
}
.car-form {
  padding: 0px 20px;
}
.car-form input {
  margin-bottom: 5px;
}
.car-body {
  display: flex;
  justify-content: space-between;
  width: calc(100% - 150px);
}
.car-plate {
  border: 1px solid black;
  padding: 10px;
  text-align: center;
}
.car-destroy {
  align-self: flex-end;
}
</style>
