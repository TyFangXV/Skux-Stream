<script>
  import {onMount} from 'svelte'
  import {fade, fly} from 'svelte/transition'
	let text = [
		{ text: 'style', id: 1, Image : "/images/lady-vibbin.svg", x:-200, y:0},
		{ text: 'Anywhere', id: 2, Image : "/images/lady-sitting-near-window.svg", y:200, x:0},
		{ text: 'no limitation', id: 3, Image : "/images/big-phone.svg", x:200, y:0}
	];
  let startingValue = 0;
  let visible = true; 
  onMount(async()=>{
    setInterval(() => {
      startingValue++;
      visible = !visible;
      if(startingValue === 3)
       {
        startingValue = 0;
       }
    }, 500);
  })


</script>
<div>
	<nav>
		<ul>
			<li><a href="/p/">Try it out</a></li>
			<li><a href="/p/">Request access</a></li>
			<li><a href="/p/">Preview</a></li>
			<li><a href="/p/">About</a></li>
		</ul>
	</nav>
	<p class="heading">Enjoy your music with</p>
  {#if visible}
    <span class="intros">
      <h1 in:fly="{{y: text[startingValue].y,x: text[startingValue].x, duration: 1000 }}" out:fade id={text[startingValue].id}>{text[startingValue].text}</h1>
      <img src={text[startingValue].Image} alt="img" in:fly="{{y: -text[startingValue].y,x: -text[startingValue].x, duration: 1000 }}" out:fade/>    
    </span>    
  {/if}

</div>

<style>
	nav ul {
		display: flex;
		margin: 20px 0px 0px 0px;
		justify-content: flex-end;
	}

	nav ul li {
		margin: 0px 2% 0px 2%;
		list-style: none;    
	}
  
	nav ul li:hover {
    opacity: 50%;
	}
  
  nav ul li a{
    font-family: var(--Ropa);
    font-size: x-large;
    cursor: pointer;
    color: white;
    text-decoration: none; 
  }

	.heading{
		position: absolute;
		top: 25%;
		left: 15%;
		transform: translate(-25%, -15%);
		font-size: xx-large;
		font-family: var(--LogoFont);
		color: white;
	}

  .intros{
    display: flex;
    justify-content: space-between;
  }

  .intros h1{
    margin-left: 10%;
    margin-top: 20%;
    font-size: 5rem;
    color: white;
    font-family: var(--Rokkit);
    font-weight: lighter;
  }

  .intros img{
    margin-right: 15%;
    margin-top: 5%;
    width: 500px;
    height: 500px;
  }
</style>
