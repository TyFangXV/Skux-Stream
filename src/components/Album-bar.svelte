<script>
	import { onMount } from 'svelte';
	export let _albums;
	export let title;
	 let Album = [];
	 let transitionSpeed = 350;



	 _albums.forEach((album) => {
		let newAlbum = Object.assign({}, album, { visible: true });
		Album.push(newAlbum);
	});

	const back = () => {
		const transitioningAlbum = Album[Album.length - 1];
		Album = [
			Album[Album.length - 1],
			...Album.slice(0, Album.length - 1)
		];
		setTimeout(() => {
			let AlbumToBeRemoved = Album.find(
				album => album.id === transitioningAlbum.id
			);
			AlbumToBeRemoved.visible = !AlbumToBeRemoved.visible;
			setTimeout(() => (AlbumToBeRemoved.visible = !AlbumToBeRemoved.visible)), 50;
		}, transitionSpeed);
	};
	const next = () => {
		const transitioningAlbum = Album[0];
		Album = [...Album.slice(1, Album.length), Album[0]];
		setTimeout(() => {
			let AlbumToBeRemoved = Album.find(
				album => album.id === transitioningAlbum.id
			);
			AlbumToBeRemoved.visible = true;
		}, transitionSpeed);
	};
</script>

<div class="album-bar">
	<!--headline-->
	<h1 class="album-name">{title}</h1>
	<div class="album-bar-view">
		{#each Album as album}
			<div class="album">
				<!--album overlay-->
				<div class="album-thumbnail-overlay">
					<!--buttons-->
					<div class="album-overlay-btn">
						<span class="material-icons options">more_vert</span>
						<span class="material-icons play">play_arrow</span>
					</div>
				</div>

				<!--Album Cover-->
				<img src={album.image} alt="album-pic" class="album-cover" />

				<h1 class="album-name">{album.name}</h1>
			</div>
		{/each}
		<span class="material-icons playlist-carousel-control-back" on:click={back}
			>navigate_before</span
		>
		<span class="material-icons playlist-carousel-control-next" on:click={next}>navigate_next</span>
	</div>
</div>

<style>
	:root {
		--Album-height: 200px;
		--Album-width: 420px;
	}

	.album-bar {
		margin-top: 2.5%;
		margin-left: 1%;
		padding-bottom: 5%;
	}

	.album-bar .album-name {
		text-align: left;
		font-family: var(--Ropa);
		font-weight: lighter;
		color: #ffffff83;
	}

	.album-bar .album-bar-view {
		display: flex;
		flex-direction: row;
	}

	.album-bar .album-bar-view .playlist-carousel-control-back {
		-webkit-user-select: none; /* Safari */        
		-moz-user-select: none; /* Firefox */
		-ms-user-select: none; /* IE10+/Edge */
		user-select: none; /* Standard */
		position: absolute;
		margin-top: 5%;
		left: 0;
		padding: 10px;
		background-color: whitesmoke;
		border-radius: 50%;
	}

	.album-bar .album-bar-view .playlist-carousel-control-next {
		-webkit-user-select: none; /* Safari */        
		-moz-user-select: none; /* Firefox */
		-ms-user-select: none; /* IE10+/Edge */
		user-select: none; /* Standard */
		position: absolute;
		margin-top: 5%; 
		right: 0;
		padding: 10px;
		background-color: whitesmoke;
		border-radius: 50%;
	}

	.album-bar .album-bar-view .album {
		margin-right: 35px;
	}

	.album-bar .album-bar-view .album .album-thumbnail-overlay {
		background: rgb(43, 35, 35);
		background: linear-gradient(
			180deg,
			rgba(43, 35, 35, 0) 0%,
			rgba(1, 0, 0, 0.804359243697479) 98%
		);
		width: var(--Album-width);
		height: var(--Album-height);
		position: absolute;
		border-radius: 10px;
		display: none;
		-webkit-user-select: none; /* Safari */        
		-moz-user-select: none; /* Firefox */
		-ms-user-select: none; /* IE10+/Edge */
		user-select: none; /* Standard */
	}

	.album-bar .album-bar-view .album:hover .album-thumbnail-overlay {
		display: block;
	}

	.album-bar .album-bar-view .album .album-thumbnail-overlay .album-overlay-btn {
		display: flex;
		width: var(--Album-width);
		justify-content: space-between;
		position: absolute;
		color: black;
	}

	.album-bar .album-bar-view .album .album-overlay-btn .material-icons {
		cursor: pointer;
		color: white;
		font-size: 2rem;
	}

	.album-bar .album-bar-view .album .album-cover {
		width: var(--Album-width);
		height: var(--Album-height);
		object-fit: cover;
		border-radius: 10px;
        object-fit: cover;
		-webkit-user-select: none; /* Safari */        
		-moz-user-select: none; /* Firefox */
		-ms-user-select: none; /* IE10+/Edge */
		user-select: none; /* Standard */
	}

	.album-bar .album-bar-view .album .album-name {
		font-family: 'Ropa Sans', sans-serif;
		color: whitesmoke;
		font-weight: lighter;
	}
</style>
