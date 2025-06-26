<script lang="ts">
	import { onMount } from "svelte";

	let activeSlide = 0;
	let interval: ReturnType<typeof setInterval> | undefined;

	const heroSlides = [
		{
			title: "Selamat Datang di Basketball Club",
			content:
				"Gabung bersama komunitas basket terbaik dan tingkatkan skillmu sekarang!",
			image_url:
				"https://images.unsplash.com/photo-1519766304817-4f37bda74a26?q=80&w=1920&auto=format&fit=crop",
			link_url: "#",
		},
		{
			title: "Jadilah Bagian dari Tim Impian",
			content: "Berlatih, bertanding, dan tumbuh bersama tim kami.",
			image_url:
				"https://images.unsplash.com/photo-1546519638-68e109498ffc?q=80&w=1920&auto=format&fit=crop",
			link_url: "#",
		},
		{
			title: "Turnamen Nasional 2025",
			content: "Siapkan dirimu! Pendaftaran tim segera dibuka.",
			image_url:
				"https://images.unsplash.com/photo-1504450758481-7338eba7524a?q=80&w=1169&auto=format&fit=crop",
			link_url: "#",
		},
	];

	onMount(() => {
		interval = setInterval(() => {
			activeSlide = (activeSlide + 1) % heroSlides.length;
		}, 6000);
		return () => clearInterval(interval);
	});
</script>

<svelte:head>
	<title>Beranda Basketball Club</title>
</svelte:head>

<!-- Hero Carousel with Navbar Inside -->
<section class="relative w-full h-screen overflow-hidden">
	<!-- Carousel Slides -->
	{#each heroSlides as slide, index}
		<div
			class="absolute inset-0 transition-opacity duration-1000 ease-in-out"
			style="opacity: {index === activeSlide ? 1 : 0}; z-index: {index ===
			activeSlide
				? 10
				: 0};"
		>
			<img
				src={slide.image_url}
				alt="Hero"
				class="w-full h-full object-cover"
			/>
			<div class="absolute inset-0 bg-black/60"></div>

			<!-- Navbar inside carousel -->
			<nav
				class="absolute top-0 left-0 w-full flex items-center justify-between px-6 md:px-10 py-4 z-20 bg-transparent"
			>
				<div class="text-2xl font-extrabold text-white drop-shadow">
					🏀 Basketball Club
				</div>
				<div class="space-x-4">
					<a href="/" class="text-white font-medium hover:underline"
						>Beranda</a
					>
					<a
						href="/login"
						class="bg-white text-blue-700 px-4 py-2 rounded-full font-semibold shadow hover:bg-gray-100 transition"
						>Login</a
					>
				</div>
			</nav>

			<!-- Hero Text -->
			<div
				class="absolute top-1/2 left-1/2 transform -translate-x-1/2 -translate-y-1/2 text-white z-20 text-center px-6 max-w-2xl"
			>
				<h1
					class="text-4xl md:text-6xl font-extrabold mb-4 drop-shadow"
				>
					{slide.title}
				</h1>
				<p class="text-lg md:text-2xl mb-6">{slide.content}</p>
				<div class="flex flex-col md:flex-row gap-4 justify-center">
					<a
						href={slide.link_url}
						class="bg-white text-blue-700 px-6 py-3 rounded-full font-bold text-lg shadow hover:bg-gray-100 transition"
						>Pelajari Lebih Lanjut</a
					>
					<a
						href="/membership"
						class="bg-yellow-400 text-gray-900 px-6 py-3 rounded-full font-bold text-lg shadow hover:bg-yellow-500 transition"
						>Daftar Membership</a
					>
				</div>
			</div>
		</div>
	{/each}
</section>

<!-- Section: Announcement -->
<section
	class="bg-gradient-to-r from-yellow-50 to-white border-l-4 border-yellow-500 p-8 md:p-12 rounded-xl shadow-md max-w-5xl mx-auto my-20 animate-fade-up"
>
	<h2 class="text-3xl font-bold text-yellow-700 mb-4">
		Pendaftaran Member Dibuka!
	</h2>
	<p class="text-gray-800 text-lg leading-relaxed">
		Daftarkan dirimu sebelum <strong>30 Juni</strong> dan dapatkan jersey gratis
		eksklusif dari klub kami.
	</p>
</section>

<!-- Section: Event Highlight -->
<section
	class="grid grid-cols-1 md:grid-cols-2 gap-12 items-center max-w-7xl mx-auto px-4 md:px-10 animate-fade-in-up"
>
	<img
		src="https://images.unsplash.com/photo-1520399636535-24741e71b160?q=80&w=1170&auto=format&fit=crop"
		alt="Event"
		class="rounded-xl shadow-xl w-full h-96 object-cover hover:scale-105 transition duration-700"
	/>
	<div class="space-y-4">
		<h3 class="text-4xl font-bold text-gray-900">Summer Tournament 2025</h3>
		<p class="text-gray-700 text-lg leading-relaxed">
			Turnamen basket terbesar tahun ini! Ayo daftar dan buktikan
			kemampuanmu di lapangan melawan tim terbaik dari seluruh Indonesia.
		</p>
		<a
			href="#"
			class="inline-block text-white bg-blue-600 px-6 py-3 rounded-full font-semibold hover:bg-blue-700 transition shadow"
			>Ikuti Event</a
		>
	</div>
</section>

<!-- Section: Newsletter -->
<section
	class="mt-24 bg-blue-50 py-16 px-6 md:px-20 text-center rounded-t-3xl shadow-inner"
>
	<h2 class="text-3xl md:text-4xl font-bold text-blue-800 mb-4">
		Tetap Terhubung
	</h2>
	<p class="text-gray-600 text-lg mb-8">
		Masukkan email dan nomor WhatsApp kamu untuk mendapatkan info event &
		promosi terbaru!
	</p>
	<form class="max-w-2xl mx-auto grid grid-cols-1 md:grid-cols-3 gap-4">
		<input
			type="email"
			placeholder="Email kamu"
			class="px-4 py-3 rounded-full border border-gray-300 focus:outline-none focus:ring-2 focus:ring-blue-500"
		/>
		<input
			type="text"
			placeholder="No WhatsApp"
			class="px-4 py-3 rounded-full border border-gray-300 focus:outline-none focus:ring-2 focus:ring-blue-500"
		/>
		<button
			type="submit"
			class="bg-blue-600 text-white font-bold px-6 py-3 rounded-full hover:bg-blue-700 transition"
			>Subscribe</button
		>
	</form>
</section>

<style>
	@keyframes fade-in-up {
		from {
			opacity: 0;
			transform: translateY(40px);
		}
		to {
			opacity: 1;
			transform: translateY(0);
		}
	}
	@keyframes fade-up {
		from {
			opacity: 0;
			transform: translateY(20px);
		}
		to {
			opacity: 1;
			transform: translateY(0);
		}
	}
	.animate-fade-up {
		animation: fade-up 1s ease-out forwards;
	}
	.animate-fade-in-up {
		animation: fade-in-up 1.5s ease-out forwards;
	}
</style>
