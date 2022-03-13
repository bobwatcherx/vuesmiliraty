<script >
  import stringSimilarity from "string-similarity"
  export default{
    data(){
      return{
        skor:0,
        postsoal:[
        {
          "soal":"Dimanakah Ibu kota Indonesia",
          "jawaban":"jakarta",
          "nilai":20,
          "answer":"",
          "acur":""
        },
        {
          "soal":"siapa presiden pertama ?",
          "jawaban":"sukarno",
          "nilai":20,
          "answer":"",
          "acur":""

        },
        {
          "soal":"jumlah propinsi di Indonesia",
          "jawaban":"34",
          "nilai":20,
          "answer":"",
          "acur":""

        }
        ]
      }
    },
    methods:{
      sendpost(){

        let soal = this.postsoal.forEach((p)=>{
         var similarity = stringSimilarity.compareTwoStrings(p.jawaban, p.answer);
         console.log(JSON.stringify(similarity))
         if(similarity  > 0.8 && similarity <= 1){
          this.skor = this.skor + p.nilai
          p.acur = similarity
         }
        })
      },
      reset(){
        this.skor = 0
        this.postsoal.forEach((p)=>{
          p.answer = "";
        })
      }
    }
  }
</script>
<template>
  <div >
    <h1>skor :{{skor}}</h1>
    <div v-for="(p,index) in postsoal">
      <span key="index"
      class="soal"
      >
        <h2>{{index}}. {{p.soal}}</h2>
       Jawab: <textarea
        v-model="p.answer"
         name=""/>
         <h3>{{p.acur}}</h3>
      </span>
    </div>
    <button @click="sendpost">Kirim Jawaban</button>
    <button @click="reset"
    style="background-color: red;color: white;"
    >Reset</button>
  </div>
</template>

<style >
  .soal{
    font-weight: bold;
    font-size: 50;
  }
</style>