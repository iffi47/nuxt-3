<template>
 <div>
  <pre>{{ data }}</pre>
 </div>
</template>
<script setup>
 const route = useRoute();
 const {data} = await useFetch("http://www.omdbapi.com/",{
  params:{
    i: route.params.id,
    apikey: "499650a"
  }
 },{
  pick:["Title", "Year", "Rated", "Released", "Runtime", "Genre", "Director", "Writer", "Actors", "Plot", "Language", "Country", "Awards", "Poster","Error"],
  key: `movie-${route.params.id}`,
 })
 if(data.value.Error==="Incorrect IMDb ID."){ 
      showError({
        statusCode: 404,
        statusMessage: "Movie Not Found"
      });
    }
//  const {data} = useAsyncData(`/movies/${route.params.id}`,() => {
//  return  $fetch(
//   `http://www.omdbapi.com/?i=${route.params.id}&apikey=499650a`
//  );
//  },
//  {
//   pick:["Title", "Year", "Rated", "Released", "Runtime", "Genre", "Director", "Writer", "Actors", "Plot", "Language", "Country", "Awards", "Poster"]
//  }
// );
 console.log(data);
</script>
