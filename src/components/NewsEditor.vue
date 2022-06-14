<template>
  <section>
    <div id="mainDiv">

      <div id="headerDiv">
       <span> <img id="logo" src="https://www.criticalmention.com/wp-content/uploads/Critical_Mention_Onclusive_transparent-600x403.png" /> </span>
       <div id="LogoName"> 
         <p>CRITICAL MENTION HOUSE</p>

       <p>OnClusive Family</p>
       <p>NewYork-Mumbai-London</p>

       </div>

      <div id="middleHeader">
      <p>CM NEWS FACTORY</p>
      <p>{{currentDate}}</p>

      </div>

        <div id="rightHeader">

      <div id="rightHeader1">
        <div>Telephone is here</div>
        <div id="rightHeader2">
          <div>$18.90</div>
          <div id="rightHeader3"></div>
          <div>Mumbai</div>

          
        </div>

      </div>

      <div id="leftHeader">
        <img  src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTeDqrH21_arwRDfvclattPBg7KT07OxXkN1g&usqp=CAU"/>
      </div>
      
      </div>
      
      </div>
      
      <div id="buttonDiv">
      
      <!-- <span > <button  :disabled="this.pageCount == '1'"
          @click="Pagination('first_page')">first Page</button> </span>
      
      <span :disabled="this.pageCount == '1'" @click="Pagination(-1)"> Previous </span>

      <span :disabled="this.pageCount == '5'" @click="Pagination(1)"> Next</span>

      <span   :disabled="this.pageCount == '5'"
          @click="Pagination('last_page')">  last Page</span> -->

     
     


      <div id="buttonDiv1">
        <button
          :disabled="this.pageCount == '1'"
          @click="Pagination('first_page')"
        >
          First Page
        </button>

        <button :disabled="this.pageCount == '1'" @click="Pagination(-1)">
         &Lt; Prev
        </button>
        <span>{{pageCount}}</span>
        <button :disabled="this.pageCount == '5'" @click="Pagination(1)">
          Next &Gt;
        </button>

        <button
          :disabled="this.pageCount == '5'"
          @click="Pagination('last_page')"
        >
          Last Page
        </button>
        </div>

       <span id="searchBar">   <input
          placeholder="Search Articles "
          v-model="inputValue"
          v-on:keyup.enter="enteredValue"
        />
        <button><img src="../assets/icons8-search-50.png"/></button>
        </span>
        <span>
        <select
          id="selectTagid"
          v-model="value"
          @change="Datesort"
          v-if="selectTag"
        >
          <option value="week1">Week 1</option>
          <option value="week2">Week 2</option>
          <option value="week3">Week 3</option>
          <option value="week4">Week 4</option>
        </select>
        </span>
      </div>

     <div id="newsDivs">
      <div id="newsDivleft">
        <h3>Top Daily News</h3>

        <div id="newsDivleft1">
      <NewsEditorUIVue
        v-for="(newdata, index) in Data"
        :key="index"
        :index="index"
        :title="newdata.title"
        :description="newdata.description"
        :content="newdata.content"
        :url="newdata.url"
        :author="newdata.author"
        :urlToImage="newdata.urlToImage"
      />
      </div>
      </div>
    
      <div id="newsDivright">
        <h3>OnClusive Family News</h3>
        <div id="newsDivright1">
        <h4 v-if="UsNews" >USA Top Headlines</h4>
        <h4 v-else>{{inputValue}} Top News</h4>

        <NewsUirightVue
             v-for="(newdataright, index) in Dataright"
        :key="index"
        :index="index"
        :title="newdataright.title"
        :description="newdataright.description"
        :content="newdataright.content"
        :url="newdataright.url"
        :author="newdataright.author"
        :urlToImage="newdataright.urlToImage"
        />
        </div>
      </div>
      </div>

      <!-- //dad div down -->
    </div>
  </section>
</template>

<script>
import axios from "axios";
import NewsEditorUIVue from "./NewsEditorUI.vue";
import NewsUirightVue from "./NewsUiright.vue";


export default {
  components: {
   NewsEditorUIVue,
   NewsUirightVue
  },
  data() {
    return {
      Data: [],
      Dataright:[],
      count: 0,
      pageCount: 1,
      inputValue: "",
      value: "",
      showData: true,
      selectTag: false,
      currentDate:new Date().toDateString(),
      UsNews:true,
    };
  },
  methods: {
    Pagination(x) {
      console.log("im here")
      this.selectTag = false;
      if (x == "first_page") {
        this.pageCount = 1;
        axios
          .get(
            `https://newsapi.org/v2/everything?domains=wsj.com&page=${this.pageCount}&apiKey=4ad2a674dde14205b995173bd10abce4`
          )
          .then((res) => {
            this.Data = res.data.articles;
            //console.log('data',this.Data)
          });
      } else if (x == "last_page") {
        this.pageCount = 5;
        axios
          .get(
            `https://newsapi.org/v2/everything?domains=wsj.com&page=${this.pageCount}&apiKey=4ad2a674dde14205b995173bd10abce4`
          )
          .then((res) => {
            this.Data = res.data.articles;
            //console.log('data',this.Data)
          });
      } else {
        this.pageCount += x;
        axios
          .get(
            `https://newsapi.org/v2/everything?domains=wsj.com&page=${this.pageCount}&apiKey=4ad2a674dde14205b995173bd10abce4`
          )
          .then((res) => {
            this.Data = res.data.articles;
            //console.log('data',this.Data)
          });
        console.log(this.pageCount);
      }
    },
    Datesort() {
      console.log(this.value);
      if (this.value == "week4") {
        let Date1 = "2022-05-08";
        axios
          .get(
            `https://newsapi.org/v2/everything?q=${this.inputValue}&from=${Date1}&apiKey=4ad2a674dde14205b995173bd10abce4`
          )
          .then((res) => {
            this.Dataright = res.data.articles;
            //console.log('data',this.Data)
          });
      }
      if (this.value == "week3") {
        let Date1 = "2022-05-15";
        axios
          .get(
            `https://newsapi.org/v2/everything?q=${this.inputValue}&from=${Date1}&apiKey=4ad2a674dde14205b995173bd10abce4`
          )
          .then((res) => {
            this.Dataright = res.data.articles;
            //console.log('data',this.Data)
          });
      }
      if (this.value == "week2") {
        let Date1 = "2022-05-22";
        axios
          .get(
            `https://newsapi.org/v2/everything?q=${this.inputValue}&from=${Date1}&apiKey=4ad2a674dde14205b995173bd10abce4`
          )
          .then((res) => {
            this.Dataright = res.data.articles;
            //console.log('data',this.Data)
          });
      }
      if (this.value == "week1") {
        let Date1 = "2022-05-29";
        axios
          .get(
            `https://newsapi.org/v2/everything?q=${this.inputValue}&from=${Date1}&apiKey=4ad2a674dde14205b995173bd10abce4`
          )
          .then((res) => {
            this.Dataright = res.data.articles;
            //console.log('data',this.Data)
          });
      }
    },
    enteredValue() {
      this.selectTag = true;
      this.UsNews=false;
      console.log(this.inputValue);
      axios
        .get(
          `https://newsapi.org/v2/everything?q=${this.inputValue}&from=2022-05-12&apiKey=4ad2a674dde14205b995173bd10abce4`
        )
        .then((res) => {
          this.Dataright = res.data.articles;
          //console.log('data',this.Data)
        });
    },
  },
  computed: {},
  watch: {},
  created() {
    //  /530378679ab54f5692e6e04a9cc6a3b4 piyushchaukade21@gmail.com
    //3e5f6f481c53470294f159172b42824d
    //4ad2a674dde14205b995173bd10abce4

    axios
      .get(
        `https://newsapi.org/v2/everything?domains=wsj.com&page=${this.pageCount}&apiKey=4ad2a674dde14205b995173bd10abce4`
      )
      .then((res) => {
        this.Data = res.data.articles;
        //console.log('data',this.Data)
      });

    axios
      .get(
        `https://newsapi.org/v2/top-headlines?country=us&category=business&apiKey=530378679ab54f5692e6e04a9cc6a3b4`
      )
      .then((res) => {
        this.Dataright = res.data.articles;
        //console.log('data',this.Data)
      });
    //   for(var i=0; i<this.Data.length; i++){
    //       console.log(this.Data.author)
    //   }
  },
};
</script>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Joan&display=swap" rel="stylesheet">
<link href="https://fonts.googleapis.com/css2?family=Kanit:wght@100&display=swap" rel="stylesheet">
<link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&display=swap" rel="stylesheet">
<link href="https://fonts.googleapis.com/css2?family=Bree+Serif&display=swap" rel="stylesheet">
<link href="https://fonts.googleapis.com/css2?family=Bree+Serif&display=swap" rel="stylesheet">
<link href="https://fonts.googleapis.com/css2?family=Romanesco&display=swap" rel="stylesheet">



<style scoped>
#mainDiv {
  width: 90%;
  margin: auto;
 
 box-shadow: rgba(50, 50, 93, 0.25) 0px 50px 100px -20px, rgba(0, 0, 0, 0.3) 0px 30px 60px -30px, rgba(10, 37, 64, 0.35) 0px -2px 6px 0px inset;
}

#buttonDiv {
  margin: 10px 0px 10px 0px;
  display: flex;
  border: 1.5px solid grey;
    border-top: hidden;
  border-left: hidden;
  border-right: hidden;
  padding-bottom: 10px;
}
#buttonDiv1{
  border: 1.5px solid #1eb4a9;
   padding: 10px 10px 10px 13px ;
   height: 30px;
  display: flex;
margin-left: 15%;
background-color: white;
border-radius: 25px;


}
#buttonDiv1>button{
height: 30px;
width: 80px;
border: none;
margin-right: 10px;
color: #1eb4a9;
background-color: white;
  transition: all .2s ease-in-out;
  font-weight: bold;
}
#buttonDiv1>button:hover{
transform: scale(1.1);
}

#buttonDiv1>span{
margin-right: 10px;
height: 25px;
width: 30px;
color: white;
background-color: #1eb4a9;
border-radius: 50%;
 padding: 6px 1px 0px 0px;
  transition: all .2s ease-in-out;
}
#buttonDiv1>span:hover{
transform: scale(1.1);
}
#buttonDiv>span>img{
  width: 30px;
  height: 30px;
}
#buttonDiv>span{
  cursor: pointer;
  margin-left: 10px;
}
#buttonDiv>span>button>img{
  width: 15px;
  height: 15px;
} 
#searchBar{
margin-left: 19% !important;
margin: 10px 0px 0px 0px;

}
#searchBar>input{

height: 20px;
padding-left: 15px;
}
#searchBar>button{
vertical-align:top;
height: 25px;
background-color: #1eb4a9;
border: none;

}
#selectTagid{
height: 25px;
vertical-align:top;
margin-top: 10px;
}
#headerDiv{
  width: 100%;
 height: fit-content;
 text-align: left;
  border: 1.5px solid grey;
  border-top: hidden;
  border-left: hidden;
  border-right: hidden;
display: flex;
}
#logo{
  width: 60px;
  height: 60px;
  border-radius: 50%;
  background-color: aqua;
  margin: 10px 10px 10px 10px;
box-shadow: rgba(50, 50, 93, 0.25) 0px 50px 100px -20px, rgba(0, 0, 0, 0.3) 0px 30px 60px -30px, rgba(10, 37, 64, 0.35) 0px -2px 6px 0px inset;
  transition: all .2s ease-in-out;

}
#logo:hover{
transform: scale(1.1);
}
#LogoName>p:nth-child(1){
  font-family: 'Joan', serif;
  word-spacing: -.1ch;
  
  font-size: 16px;
  font-weight: bold;

}
#LogoName>p:nth-child(2){
margin-top:  -10px;
  font-size: 14px;

}
#LogoName>p:nth-child(3){
margin-top:  -10px;
  font-size: 12px;
font-family: 'Kanit', sans-serif;
}
#middleHeader{
  border: 1.5px solid grey;
  height: 60px;
  width: 24%;
  margin: 15px 10px 10px 12%;
  border-right: none;
  border-left: none;
  text-align: center;
}
#middleHeader>p:nth-child(1){
font-family: 'Bebas Neue';
font-weight: bold;
letter-spacing: 1.5px;
 margin-top: 5px;


}
#middleHeader>p:nth-child(2){
 margin-top: -7px;
font-size: 14px;
}


#rightHeader{
  border: 1.5px solid grey;
  height: 60px;
  width: 22%;
  margin: 15px 10px 10px 9%;
  border-right: none;
  border-left: none;
  border-top: none;
  text-align: center;
  display: flex;
}
#rightHeader1{
display: block;
margin:8px 4px 4px 4px;
font-family: 'Bree Serif';
font-size: 16px;
font-weight: 600;
}
#rightHeader2{
display: flex;
margin:8px 0px 0px 0px;
font-size: 18px;
font-weight: 600;
}
#rightHeader3{
width: 1px;
background-color: grey;
margin: 0px 5px 0px 5px;
}
#leftHeader{
margin-left: 30px;
}
#leftHeader>img{
height: 60px;
width: 60px;
}

/*news div started--------------------------- */
#newsDivs{
  display: inline-block;
  margin-bottom: 20px;
}
#newsDivleft{
  display: inline-block;
vertical-align: top;
width: 65%;margin-right: 3%;

}

#newsDivleft1{
overflow: hidden;
  height: 600px;
width: 97.7%;
    border: 2px solid grey;
    border-radius: 5px;
}
#newsDivleft1:hover{
overflow: scroll;
height: 600px;
overflow-x: hidden;
width: 100%;

}

#newsDivright{
width: 30%;
display: inline-block;
vertical-align: top;
}
#newsDivright>h3{

  font-family: 'Bree Serif', serif;
  letter-spacing: 1.5px;
}
#newsDivright1{
overflow: hidden;
height: 600px;
width: 95%;
    border: 2px solid grey;
    border-radius: 5px;
}
#newsDivright1>h4{
font-family: 'Bebas Neue';
border: 1px solid grey;
  border-top: hidden;
    border-left: hidden;
    border-right: hidden;
    width: 150px;
    margin: auto;
    margin-top: 10px;
}
#newsDivright1:hover{
overflow: scroll;
height: 600px;
overflow-x: hidden;
width: 100%;

}

</style>
