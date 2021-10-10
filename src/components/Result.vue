<template >
    <div class="result" v-if="score">
      <p>Your reaction time is: <strong>( {{score}} ms )</strong></p>  
      <p>You gained a <strong>{{rank}}</strong> rank</p>
    </div>
    <div class="all-scores">
        <ul>
            <li v-for="(i, index) in allRanks" :key="index">
                <span>Score and Rank: {{i.score}}  {{i.rank}} </span>
               
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
        this.allRanks.push({
            score:this.score,
            rank:this.rank
        })
        this.score?localStorage.setItem("all-scores", JSON.stringify(this.allRanks)):""
    },
    created() {
        this.allRanks=JSON.parse(localStorage.getItem("all-scores")) || [];    
    },
}
</script>
