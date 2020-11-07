<template>
  <div class="calender">
    <h1>Vue Calender</h1>
    <h3>{{currentMonthName}} {{currentYear}}</h3>
    <div class="wrapper">
        <section class="days">
          <div v-for="day in days" :key="day">{{day}}</div>
        </section>
        <section class="date">
          <p v-for="num in firstDay()" :key="num"></p>
          <p v-for="num in totalDaysInMonth(currentYear,currentMonth)" :key="num" :class="currentDateClass(num)">
            <span v-if="!colorCurrentDate">{{num}}</span><span v-if="colorCurrentDate" :class="{grey:true}">{{num}}</span>
          </p>
        </section>
        <section>
          <button @click="prev">Prev</button>
          <button @click="next">Next</button>
        </section>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Index',
  data(){
    return{
      days:['Sun','Mon','Tue','Wed','Thu','Fri','Sat'],
      currentMonth:new Date().getMonth(),
      currentYear: new Date().getFullYear(),
      currentDate: new Date().getUTCDate(),
      calenderFullDate:'',
      currentFullDate:'',
      colorCurrentDate:''
    }
  },
  methods:{
    totalDaysInMonth(){
      // console.log(new Date(this.currentYear,this.currentMonth+1 ,0).getDate());
      return new Date(this.currentYear,this.currentMonth+1 ,0).getDate()
    },
    firstDay(){
      // console.log(new Date(this.currentYear, this.currentMonth, 1).getDay());
      return new Date(this.currentYear, this.currentMonth, 1).getDay()
    },
    next(){
      if(this.currentMonth == 11){
        this.currentYear++
        this.currentMonth = -1
      
      }
      this.currentMonth++
      console.log(this.currentMonth);

    },
    prev(){
      if(this.currentMonth == 0){
        this.currentYear--
        this.currentMonth = 12
      }
      this.currentMonth--
      console.log(this.currentMonth);
    },
    currentDateClass(num){
      this.calenderFullDate =  new Date(this.currentYear, this.currentMonth, num).toDateString()
      this.currentFullDate = new Date().toDateString()
      return this.colorCurrentDate = this.calenderFullDate === this.currentFullDate
    }
    
  },
  computed:{
     currentMonthName(){
      return new Date(this.currentYear, this.currentMonth).toLocaleString('default', { month: 'long' })
    }
  }
  

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.calender{
  width: 600px;
  margin: 0 auto;
}

.wrapper{
  width: 400px;
  margin: 0 auto;
  margin-top: 30px;
}


.days{
  display: flex;
}

.days div{
  width: 14.28%;
  font-weight: bold;
}

.date{
  display: flex;
  flex-wrap: wrap;
}

.date p{
  width: 14.24%;
}

button{
  margin: 10px;
  padding: 5px 15px;
}

.grey{
  background-color: rgb(7, 206, 40);
  font-size: 12px;
  padding: 10px 14px;
  border-radius: 50%;
}

</style>
