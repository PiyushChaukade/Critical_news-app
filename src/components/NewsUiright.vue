<template>
<section>


    <div id="mainDiv">

  
    <div  id="subDiv"   >

        <div id="imageDiv" > 
        <img :src='urlToImage'/>
      </div>
    
    <div id="newsDiv">

  <div  @click="showFull" id="DataShow"> 


      <span> <p>{{title}} </p> </span>

 
 </div>
 <div v-if="showData" id="ifDiv">

      <!-- <span>Content:- <p>{{content}}</p></span> -->
           <span> Description:-  <p v-html="description">
       </p></span>

        <p>Link:- <a :href='url' target="_blank"> <button>Go To Article</button></a></p>  

      
       <!-- <p v-if="author">Author name:- {{author}}</p>

       <p v-else> Author name:- Anonymus Author</p> -->
     </div>
      

      </div>

    
  
     </div>


    </div>

</section>
</template>

<script>

export default {
    props:['index','title','description','content','url','author','urlToImage'],
data(){
   return {
    showData:false,
   }
},
methods:{
  showFull(){
    
  this.showData =! this.showData;

    
  },
  

},

}


</script>

<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Romanesco&display=swap" rel="stylesheet">
<link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:wght@300&display=swap" rel="stylesheet">


<style scoped>

#subDiv{
    border: 1px solid black;
    font-size: 14px;
    border-top: hidden;
    border-left: hidden;
    border-right: hidden;
}
#newsDiv{
text-align: left;
display: inline-block;
width: 70%;
padding: 6px 0px 10px 0px;
}

#imageDiv{
vertical-align: top;
display: inline-block;
margin-right: 2px;
padding: 20px 0px 0px 0px;

}

#imageDiv>img{

height: 60px;
width: 80px;
  transition: all .2s ease-in-out;

}
#imageDiv>img:hover{


transform: scale(1.2);
}
#imageDiv{
vertical-align: top;
display: inline-block;

}


#DataShow>span{
font-size: 16px;
font-family: 'Romanesco';
font-weight: bold;
}
#DataShow>span>p{
font-size: 14px;
font-weight: 100;


}

#ifDiv>span{
font-size: 16px;
font-family: 'Romanesco';
font-weight: bold;
}
#ifDiv>span>p{
font-size: 14px;
font-weight: 100;
}
#ifDiv>p{
font-size: 15px;
font-weight: 100;
font-family: 'Cormorant Garamond', serif;
}
#ifDiv>p>a>button{
padding: 5px;
background-color: #1eb4a9;
color: white;
border: hidden;
  transition: all .2s ease-in-out;

}
#ifDiv>p>a>button:hover{
transform: scale(1.1);

}


</style>
