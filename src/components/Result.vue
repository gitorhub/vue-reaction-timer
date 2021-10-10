<template >
    <div class="result" v-if="score">
      <p>Your reaction time is: <strong>( {{score}} ms )</strong></p>  
      <p>You gained a <strong>{{rank}}</strong> rank</p>
    </div>
  
         <hr v-if="allRanks.length>0">

    <div class="all-scores" v-if="allRanks.length>0">
   
        <ul>
            <li v-for="(i, index) in allRanks" :key="index">
                <span>Score and Rank: {{i.score}}  - {{i.rank}} </span>
               
            </li>
            <li >
                <div class="btn btn--danger btn--delete" @click="deleteStorage">Delete Old Scores</div>
            </li>
        </ul>
        
    </div>
</template>
<script>
export default {
    props:["score"],
    data() {
        return {
            rank:"",
            allRanks:[]
        }
    },
    mounted() {
        if(this.score<200){
            this.rank="Golden"
        }else if(this.score<400){
            this.rank="Silver"
        }else if(this.score < 600){
            this.rank="Bronze"
        }else{
            this.rank="zero"
        }
         this.score?this.allRanks.push({
            score:this.score,
            rank:this.rank
        }):""
        this.score?localStorage.setItem("all-scores", JSON.stringify(this.allRanks)):""
    },
    created() {
        this.allRanks=JSON.parse(localStorage.getItem("all-scores")) || [];    
    },
    methods: {
        deleteStorage(){
            localStorage.clear();
            this.allRanks=[]
        }
    },
}
</script>

<style >
.all-scores{
    display: flex;
    justify-content: center;
    align-items: center;
}

    
</style>
