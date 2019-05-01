<template>
  <v-container>
    <v-layout text-xs-center wrap>
      <v-flex mb-5 xs12>
        <h2 class="headline font-weight-bold mb-3">возможные ходы коня</h2>
        <v-layout justify-center>
          <v-card class="card" style="background:#444" width="370px">
            <!-- выводим элементы на которые будем тыкать -->
            <div v-for="(elem, index) in squares" :key='index' > 
            <v-btn
              class="square"
              v-for="(item, key) in elem" 
              :key="key"
              :style="{'background-color': item.color }"
              @click="showWays(item)"
            ></v-btn>
            </div>
              <!-- :style="{'background-color': item.checked == false ? '#fff' : item.color   }" -->

          </v-card>
        </v-layout>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
export default {
  data: () => ({
    squares: [], //массив объектов с "полями"
    clickWather: true
  }),
  mounted() {
    this.rerender();
     
  },
  methods: {
    showWays(item){
        this.rerender();
       
        let magicArray = [[-2, -1],[-1, -2],[1, 2],[2, 1],[-1, 2],[2, -1],[-2, 1],[1, -2]];
        let pointArr = item.id.split("");
        this.squares[+pointArr[0]][+pointArr[1]].color='blue';
         for (let i = 0; i < 8; i++) {
        try {
          if( +pointArr[1] + magicArray[i][1] >= 0 && +pointArr[1] + magicArray[i][1] <= 8){
            // console.log(`Точка[${+pointArr[0]}:${+pointArr[1]}] и Точка[${+magicArray[i][0]}:${+magicArray[i][1]}]`)
            this.squares[+pointArr[0]+magicArray[i][0]][+pointArr[1] + magicArray[i][1]].color= 'green'
          }
          // else{
          //   console.log('Случился meh')
          // }
        } catch (err) {
        console.log('Случился не успех')
        }

      }
   

    },
    rerender(){
        let squares = new Array();
    for (let i = 0; i < 8; i++) {
      squares[i] = []
       for (let j = 0; j < 8; j++) {
      if (i % 2 == 0 && j % 2 == 0 || i % 2 !== 0 && j % 2 !== 0 ){
       squares[i][j]={
          id: `${i}${j}`,
          checked: false,
          color: 'white'
        }
      }
      else {
         squares[i][j]={
            id: `${i}${j}`,
          checked: false,
          color: 'black'
        }
        
      }
     
    }
    }
    this.squares = squares;
    }
    
  },
  computed: {
    
  }
};
</script>

<style>
.disable-events {
  pointer-events: none;
}
.enable-events {
  pointer-events: auto;
}
.card {
  padding: 15px !important;
}
.square {
  width: 40px;
  height: 40px;
  min-width: 40px;
  border: none;
  border-radius: 0;
  margin: 0 !important;
  padding: 0 !important;
}
.white {
  background: white !important;
}
</style>
