
<style>
  * 
  {
    color : white;
  }

</style>

<script>
  const data = [
    {title:"winch.link",description:"Un outil permettant de contacter directement les entreprises et ses employés sur les offres d'emploi",link:"https://winch.link"},
    {title:"wirenotes",description:"La plateforme de partage de notes la plus utilisée en Belgique francophone",link:"https://wirenotes.eu"},
    {title:"edmaster",description:"masterclasses pour les étudiants sur leurs cours",link:"https://edmaster.me"},
  ]

</script>

<h2>Développement web</h2>
<div>Fort de plus de 7 ans d'expérience de développement web, full stack, laravel, sveltekit</div>

<h3>Portfolio</h3>

<div class="Portfolio">
  {#each data as {title,link}}
    <a href={link} target="_blank" rel="noreferrer">
      {title}
    </a>
  {/each}
</div>