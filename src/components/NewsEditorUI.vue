<template>
<section>

 
  


    <div id="mainDiv">

  
    <div  id="subDiv"   >
    
    <div id="newsDiv">

  <div  @click="showFull" id="DataShow"> 


      <span> {{index+1}}) Title:- <p>{{title}} </p> </span>

      <span> Description:-  <p v-html="description"> </p></span>
 </div>
 <div v-if="showData" id="ifDiv">

      <span>Content:- <p v-html="content"></p></span>
      
       <p>Link:- <a :href='url' target="_blank"> <button>Go To Article</button></a></p>  

      <p v-if="author">Author name:-  {{author}}</p>
      <p v-else>Author name:- Anonymus Author</p>


 </div>
      

      </div>

      <div id="imageDiv" > 
        <img :src='urlToImage'/>
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
#mainDiv{
  
}
#subDiv{
    border: 1px solid black;
    padding: 20px;
    border-top: hidden;
    border-left: hidden;
    border-right: hidden;
}
#buttonDiv{
 margin-bottom: 10px;
}

#newsDiv{
text-align: left;
display: inline-block;
width: 500px;
margin-right: 5px;

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

#imageDiv{
vertical-align: top;
display: inline-block;
}

#imageDiv>img{

height: 150px;
width: 150px;
  transition: all .2s ease-in-out;
}
#imageDiv>img:hover{

height: 150px;
width: 150px;
transform: scale(1.5);
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
