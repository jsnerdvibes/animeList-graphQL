<script>

    let finalData = []

    async function FetchData() {
       const data = await fetch('https://graphql.anilist.co',{
        method:"POST",
        headers:{
            "Content-Type":"application/json",
        },
        body:JSON.stringify({
            query:`
        {
  Page {
    media {
      siteUrl
      title {
        english
        native
      }
      description
    }
  }
}`
        })

       })
       const res = await data.json()
       finalData = res.data.Page.media;

       console.log(res.data.Page.media)
    }

    FetchData()

</script>



<div class="flex flex-col justify-evenly heh-auto">
<div>
    <h1 class="text-3xl font-bold flex items-center justify-center m-2 h-16 bg-gray-800 text-white">Anime List</h1>
</div>
<div class="flex flex-wrap bg-yellow-700 py-2 md:justify-evenly">
    {#if finalData}
       
    {#each finalData as anime}
    <div class="flex flex-col w-auto text-xs p-2 bg-orange-200 m-2 border-2 border-black rounded-xl md:w-1/4 justify-evenly">
        <h2 class="font-bold text-sm mb-2">{anime.title.english===null?anime.title.native:anime.title.english}</h2>
        <p class="text-justify mb-2">{anime.description}</p>
        <a href={`${anime.siteUrl}`} class="justify-self-end">Click here for Site</a>
    </div>   
    {/each}

    {/if}
</div>
</div>