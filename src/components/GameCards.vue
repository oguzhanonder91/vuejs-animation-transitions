<template>
  <div class="game-area">
    <h1 class="title">Poğaça <span>Nerede</span><strong>?</strong></h1>
    <h4 class="description">Açık kartlardan birini seçtikten sonra kapalı karta tıklayınız.</h4>
    <div class="container">
      <transition-group name="rotate-all" class="card-container" appear>
        <Card
          :class="{'shadow' : selectedCard == card.id}"
          @click.native="selectedCard=card.id"
          v-for="card in cards"
          :card="card"
          :key="card.id">
        </Card>
      </transition-group>

    </div>
    <div class="container">
      <transition name = "rotate" mode="out-in">
        <component
          @click.native="showCard(answer)"
          :card ="answer"
          :is="activeCard">
        </component>
      </transition>
    </div>
  </div>
</template>

<script>
  import Card from './Card';
  import DefaultCard from './DefaultCard';

  export default {
    name: "GameCards",
    components: {Card, DefaultCard},
    data() {
      return {
        cards: [
          {id: 1, component: "Card", img: "/src/assets/card-1.jpg"},
          {id: 2, component: "Card", img: "/src/assets/card-2.jpg"},
          {id: 3, component: "Card", img: "/src/assets/card-3.jpg"},
          {id: 4, component: "Card", img: "/src/assets/card-4.jpg"},
          {id: 5, component: "Card", img: "/src/assets/card-5.jpg"}
        ],
        selectedCard: null,
        answer: {},
        activeCard: DefaultCard
      }
    },
    created() {
      let answer = Math.ceil(Math.random() * this.cards.length);
      this.answer = this.cards[answer - 1];
    },
    methods:{
      showCard(answer){
        if(this.selectedCard == null){
          alert("Bir Kart Seçiniz");
        }else{
          this.activeCard = answer.component;
          setTimeout(()=>{
            if(this.selectedCard == answer.id){
              this.$emit("activeComponent","Celebrate");
            }else{
              this.$emit("activeComponent","Fail");
            }
          },2000)
        }
      }
    }
  }
</script>

<style scoped>
  .container, .card-container {
    display: flex;
    justify-content: center;
    align-items: center;
    margin-top: 50px;
  }

  .title {
    text-align: center;
    color: rosybrown;
  }

  .title span {
    color: mediumpurple;
  }

  .title strong {
    color: darkred;
  }

  .description {
    text-align: center;
    color: grey;
  }

  .shadow {
    box-shadow: 10px 20px 60px #30969f !important;
    transition: box-shadow .5s;
  }

  /*Açık kartların animasyonları için transition classları*/
  /* İlk durumu from dan yaptığımız için enter  kullanmıyoruz. Herhangi bir component ekrandan deactived olmadığı için leave kullanmıyoruz.*/


  .rotate-all-enter {
  }

  .rotate-all-enter-active {
    /* Animation */
    animation: rotate-all ease-in-out 2s forwards;
  }

  .rotate-all-leave {
  }

  .rotate-all-active {
  }

  @keyframes rotate-all {
    from {
      transform: rotateY(0);
    }
    to {
      transform: rotateY(1080deg);
    }
  }


  /*Kapalı kartların animasyonları için transition classları*/
  .rotate-enter {
  }

  .rotate-enter-active {
    /* Animation */
    animation: rotate-in ease-in-out 1s forwards;
  }

  .rotate-leave {

  }

  .rotate-leave-active {
    animation: rotate-out ease-in-out 1s forwards;

  }

  @keyframes rotate-in {
    from {
      transform: rotateY(90deg);
    }
    to {
      transform: rotateY(0deg);
    }
  }

  @keyframes rotate-out {
    from {
      transform: rotateY(0deg);
    }
    to {
      transform: rotateY(90deg);
    }
  }

</style>
