<template>
  <div class="wraper container">
    <h1 class="text-center">Car sharing project</h1>

    <ul class="car-list mt-5">
      <li 
        class="car-list__item"
        v-for="(car, i) in carList"
        :key="i"
      >
        <div class="car">
          <div class="car__aside">
            <div class="car__image">
              <img src="https://ikverkoopmijnauto.nl/wp-content/uploads/2019/10/5168/2020-toyota-camry-trd-first-drive-review-de-onwaarschijnlijkste-camry.jpg">
            </div>
          </div>
          <div class="car__body">
            <h2 class="car__name">{{car.name}}</h2>
            <p class="car__description">{{car.description}}</p>
            <p class="car__price">{{car.price}}$</p>
          </div>

          <div class="car__actions ml-auto">
            <button class="btn btn-warning text-white mr-2" @click="setCarToForm(car)">Редактировать</button>
            <button class="btn btn-danger" @click="deleteCar(car)">Удалить</button>
          </div>
        </div>
      </li>
    </ul>

    <h3>Добавить тачку</h3>
    <div class="add-car">
      <div class="form-group">
        <input type="text" class="form-control" placeholder="Enter car name" v-model="newCar.name"> 
      </div>

      <div class="form-group">
        <input type="text" class="form-control" placeholder="Enter car description"  v-model="newCar.description"> 
      </div>

      <div class="form-group">
        <input type="text" class="form-control" placeholder="Enter car price"  v-model="newCar.price"> 
      </div>

      <button v-if="!isEditing" class="btn btn-success" @click="addCar">Добавить</button>
      <button  v-if="isEditing" class="btn btn-warning text-white" @click="editCar">Редактировать</button>
    </div>

  </div>
</template>

<script>

export default {
  name: "Home",

  data() {
    return {
			isEditing: false,
			selectedCar: null,

      carList: [
        {
          id: 1,
          name: 'Toyota',
          description: 'Some text',
          price: 18500,
          image: null
        },
        {
          id: 2,
          name: 'ВАЗ 2109',
          description: 'Some text фор ваз',
          price: 500,
          image: null
        }
      ],

      newCar: {
        name: '',
        description: '',
        price: ''
      }
    }
  },

  methods: {
    addCar() {
			const newcar = JSON.parse(JSON.stringify(this.newCar))
      this.carList.push(newcar)
    },

    deleteCar(car) {
      const index = this.carList.findIndex(item => {
				return item.id === car.id
      })

      this.carList.splice(index, 1)
    },

    setCarToForm(car) {
			this.isEditing = true
			const cloneCar = JSON.parse(JSON.stringify(car))
			this.newCar = cloneCar
			this.selectedCar = cloneCar
    },

		editCar() {
			const index = this.carList.findIndex(item => {
				return item.id === this.selectedCar.id
      })

			const editedCarClone = JSON.parse(JSON.stringify(this.newCar))
			console.log('editedCarClone', editedCarClone)
			this.carList.splice(index, 1, editedCarClone)

			this.newCar = {
        name: '',
        description: '',
        price: ''
      }

			this.isEditing = false
		}
  },
};
</script>

<style scoped lang="scss">
.car-list {
  list-style: none;
  &__item {

  }
}

.car {
  display: flex;

  padding: 10px;
  box-shadow: 0px 0px 10px #ccc;
  margin: 0 auto 15px;
  // max-width: 700px;

  &__aside {}

  &__actions {
  }
  &__image {
    max-width: 200px;
  }
  &__body {
    padding: 0 15px;
  }
  &__name {
    font-size: 18px;
  }
  &__price {}
}

.add-car {
  max-width: 700px;
}
</style>
