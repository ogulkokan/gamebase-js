<template>
  <q-page padding>
    <p>Memory Game</p>

    <h3>Score:<span id="result"></span></h3>

    <div class="grid"> </div>
  </q-page>
</template>

<script>

export default {
  name: 'PageMemoryGame',
  data () {
    return {
      cardArray: [
        {
          name: 'fries',
          img: '../assets/Memory/fries.png'
        },
        {
          name: 'fries',
          img: '../assets/Memory/fries.png'
        },
        {
          name: 'cheeseburger',
          img: '../assets/Memory/cheeseburger.png'
        },
        {
          name: 'cheeseburger',
          img: '../assets/Memory/cheeseburger.png'
        },
        {
          name: 'hotdog',
          img: '../assets/Memory/hotdog.png'
        },
        {
          name: 'hotdog',
          img: '../assets/Memory/hotdog.png'
        },
        {
          name: 'ice-cream',
          img: '../assets/Memory/ice-cream.png'
        },
        {
          name: 'ice-cream',
          img: '../assets/Memory/ice-cream.png'
        },
        {
          name: 'milkshake',
          img: '../assets/Memory/milkshake.png'
        },
        {
          name: 'milkshake',
          img: '../assets/Memory/milkshake.png'
        },
        {
          name: 'pizza',
          img: '../assets/Memory/pizza.png'
        },
        {
          name: 'pizza',
          img: '../assets/Memory/pizza.png'
        }
      ],
      cardsChosen: [],
      cardsChosenId: [],
      cardsWon: []
    }
  },
  methods: {
    // create your board
    createBoard () {
      const grid = document.querySelector('.grid')
      this.cardArray.sort(() => 0.5 - Math.random())
      // const resultDisplay = document.querySelector('#result')
      for (let i = 0; i < this.cardArray.length; i++) {
        const card = document.createElement('img')
        const image = require('../assets/Memory/blank.png')
        card.setAttribute('src', image)
        card.setAttribute('data-id', i)
        // card.addEventListener('click', flipcard)
        grid.appendChild(card)
      }
    },
    // flip your card
    flipCard () {
      var cardId = this.getAttribute('data-id')
      this.cardsChosen.push(this.cardArray[cardId].name)
      this.cardsChosenId.push(cardId)
      // this.setAttribute('src', cardArray[cardId].img)
      if (this.cardsChosen.length === 2) {
        setTimeout(this.checkForMatch, 500)
      }
    },
    // check for matches
    checkForMatch () {
      const cards = document.querySelectorAll('img')
      const optionOneId = this.cardsChosenId[0]
      const optionTwoId = this.cardsChosenId[1]
      if (this.cardsChosen[0] === this.cardsChosen[1]) {
        alert('You found a match')
        // assign white png for match cards
        const whiteImage = require('../assets/Memory/white.png')
        cards[optionOneid].setAttribute('src', whiteImage)
        cards[optionTwoId].setAttribute('src', whiteImage)
        this.cardsWon.push(this.cardsChosen)
      } else {
        const blankImage = require('../assets/Memory/blank.png')
        cards[optionOneId].setAttribute('src', blankImage)
        cards[optionTwoId].setAttribute('src', blankImage)
        alert('Try Again')
      }
      this.cardsChosen = []
      this.cardsChosenId = []
      // resultDisplay.textContent = this.cardsWon.length
      if (this.cardsWon.length === this.cardsArray.length / 2) {
        console.log('congrats')
        // resultDisplay.textContent = 'Congrats'
      }
    }
  },
  mounted () {
    this.createBoard()
  }
}
</script>

<style scoped>
.grid {
  display: flex;
  flex-wrap: wrap;
  height: 300px;
  width: 400px;
}
</style>
