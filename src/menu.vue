<template>
    <div class="menu bg-dark sticky-top " id="menu">
		<div class="container">
			<nav class="navbar navbar-expand-md navbar-dark">
				<!-- boutton du menu ou toggler/collapsible -->
				<button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#myNavbar">
					<span class="navbar-toggler-icon"></span>
				</button>
				<!-- lien du navbar qu'on met dans une div collapsible -->
				<div class="collapse navbar-collapse" id="myNavbar">
					<div class="navbar-nav"></div>
					<ul class="navbar-nav text-uppercase text-center">
						<li class="nav-item"><a href="index.html" class="nav-link active">Home</a></li>
						<li class="nav-item"><a href="#About" class="nav-link">Shop</a></li>
						<li class="nav-item"><a href="#team-member" class="nav-link">Team</a></li>
						<li class="nav-item"><a href="#" class="nav-link">Services</a></li>
						<li class="nav-item"><a href="#" class="nav-link">Portfolio</a></li>
						<li class="nav-item"><a href="#" class="nav-link">Contact</a></li>
					</ul>
				</div>
				<!-- logo ou brand -->
				<a href="" class="mr-auto navbar-brand text-uppercase font-weight-bold">Spirit8</a>
			</nav>
		</div>
	</div>

</template>

<script>
    export default {
        name:'myMenu'
    }
</script>