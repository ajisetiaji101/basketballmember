<script lang="ts">
	import { onMount } from "svelte";
	import { fade, scale } from "svelte/transition";
	import { cubicOut } from "svelte/easing";

	let activeSlide = 0;
	let interval: ReturnType<typeof setInterval> | undefined;

	import dharma from "$lib/images/dharma.jpeg";
	import reno from "$lib/images/reno.jpeg";
	import silvia from "$lib/images/silvia.jpg";

	const partners = [
		{
			name: "LeBron James",
			role: "Forward, Los Angeles Lakers",
			image: dharma,
			description:
				"One of the greatest basketball players of all time, known for his versatility, leadership, and multiple NBA championships.",
		},
		{
			name: "Stephen Curry",
			role: "Point Guard, Golden State Warriors",
			image: reno,
			description:
				"Revolutionized the game with his incredible shooting ability, holding multiple NBA records for three-pointers.",
		},
		{
			name: "Giannis Antetokounmpo",
			role: "Forward, Milwaukee Bucks",
			image: silvia,
			description:
				"Known as the 'Greek Freak', Giannis is a two-time NBA MVP and led the Bucks to an NBA championship in 2021.",
		},
	];

	let visible = partners.map(() => false);

	function inView(node: Element, index: number) {
		const observer = new IntersectionObserver(
			(entries) => {
				entries.forEach((entry) => {
					if (entry.isIntersecting) {
						visible[index] = true;
						observer.unobserve(node);
					}
				});
			},
			{ threshold: 0.1 },
		);
		observer.observe(node);

		return {
			destroy() {
				observer.unobserve(node);
			},
		};
	}

	function fadeScale(node: Element, { delay = 0, duration = 400 }) {
		return {
			delay,
			duration,
			css: (t: number) => {
				const eased = cubicOut(t);
				return `
                    opacity: ${eased};
                    transform: scale(${eased});
                `;
			},
		};
	}

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

<section class="relative w-full h-screen overflow-hidden font-sans">
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
			<div
				class="absolute inset-0 bg-gradient-to-t from-black/80 to-black/40"
			></div>

			<nav
				class="absolute top-0 left-0 w-full flex items-center justify-between px-6 md:px-12 py-5 z-20 bg-transparent"
			>
				<div class="text-3xl font-extrabold text-white drop-shadow-md">
					<span class="text-yellow-400">🏀</span> Basketball Club
				</div>
				<div class="space-x-6 flex items-center">
					<a
						href="/"
						class="text-white text-lg font-medium hover:text-yellow-300 transition duration-300"
						>Beranda</a
					>
					<a
						href="/login"
						class="bg-white text-blue-800 px-6 py-2 rounded-full font-semibold shadow-lg hover:bg-gray-200 transition duration-300 transform hover:scale-105"
						>Login</a
					>
				</div>
			</nav>

			<div
				class="absolute top-1/2 left-1/2 transform -translate-x-1/2 -translate-y-1/2 text-white z-20 text-center px-6 max-w-4xl w-full"
				in:fade={{ delay: 500, duration: 800 }}
			>
				<h1
					class="text-5xl md:text-7xl font-extrabold mb-5 drop-shadow-xl leading-tight"
				>
					{slide.title}
				</h1>
				<p class="text-xl md:text-3xl mb-10 font-light opacity-90">
					{slide.content}
				</p>
				<div class="flex flex-col md:flex-row gap-5 justify-center">
					<a
						href={slide.link_url}
						class="bg-gradient-to-r from-blue-600 to-blue-800 text-white px-10 py-4 rounded-full font-bold text-xl shadow-2xl hover:from-blue-700 hover:to-blue-900 transition duration-300 ease-in-out transform hover:-translate-y-1 hover:scale-105"
						>Pelajari Lebih Lanjut</a
					>
					<a
						href="/membership"
						class="bg-gradient-to-r from-yellow-400 to-orange-500 text-gray-900 px-10 py-4 rounded-full font-bold text-xl shadow-2xl hover:from-yellow-500 hover:to-orange-600 transition duration-300 ease-in-out transform hover:-translate-y-1 hover:scale-105"
						>Daftar Membership</a
					>
				</div>
			</div>
		</div>
	{/each}
</section>

---

<section
	class="bg-gradient-to-br from-yellow-50 to-white border-l-8 border-yellow-500 p-10 md:p-16 rounded-2xl shadow-xl max-w-6xl mx-auto my-24 animate-fade-up relative overflow-hidden"
>
	<div
		class="absolute inset-0 bg-grid-pattern opacity-5 pointer-events-none"
	></div>
	<h2 class="text-4xl font-extrabold text-yellow-800 mb-6 drop-shadow-md">
		📢 Pendaftaran Member Dibuka!
	</h2>
	<p class="text-gray-900 text-xl leading-relaxed font-medium">
		Daftarkan dirimu sebelum
		<strong class="text-yellow-900 underline decoration-yellow-600"
			>30 Juni 2025</strong
		>
		dan dapatkan **jersey eksklusif gratis** dari klub kami. Jangan lewatkan
		kesempatan emas ini untuk menjadi bagian dari keluarga besar Basketball Club!
	</p>
</section>

---

<section class="my-32 px-6 md:px-10 max-w-7xl mx-auto text-center">
	<h2 class="text-5xl font-extrabold text-gray-900 mb-20">
		Meet Our Esteemed Partners
	</h2>

	<div class="grid grid-cols-1 md:grid-cols-3 gap-12">
		{#each partners as partner, index}
			<div
				use:inView={index}
				class="bg-gradient-to-br from-gray-800 to-gray-900 text-white rounded-3xl shadow-2xl p-10 transform transition-all duration-500 hover:scale-105 hover:shadow-3xl border-t-4 border-l-4 border-yellow-500 relative overflow-hidden group"
			>
				<div
					class="absolute inset-0 bg-dots-pattern opacity-5 group-hover:opacity-10 transition-opacity duration-300"
				></div>
				{#if visible[index]}
					<div
						in:fadeScale={{ delay: index * 180, duration: 700 }}
						class="text-center relative z-10"
					>
						<img
							src={partner.image}
							alt={partner.name}
							class="w-36 h-36 rounded-full mx-auto mb-7 object-cover border-5 border-yellow-400 shadow-xl transition-transform duration-300 group-hover:scale-105"
						/>
						<h3 class="text-3xl font-bold mb-2">
							{partner.name}
						</h3>
						<p
							class="text-lg font-semibold text-yellow-400 mb-4 tracking-wide"
						>
							{partner.role}
						</p>
						<p class="text-base leading-relaxed text-gray-300">
							{partner.description}
						</p>
					</div>
				{/if}
			</div>
		{/each}
	</div>
</section>

---

<section
	class="grid grid-cols-1 md:grid-cols-2 gap-20 items-center max-w-7xl mx-auto px-6 md:px-10 my-32 animate-fade-in-up"
>
	<div class="relative group">
		<img
			src="https://images.unsplash.com/photo-1520399636535-24741e71b160?q=80&w=1170&auto=format&fit=crop"
			alt="Summer Tournament 2025"
			class="rounded-3xl shadow-3xl w-full h-[450px] object-cover transform transition duration-700 ease-in-out group-hover:scale-102 group-hover:shadow-4xl"
		/>
		<div
			class="absolute inset-0 bg-blue-800 opacity-0 rounded-3xl group-hover:opacity-10 transition-opacity duration-300"
		></div>
	</div>
	<div class="space-y-8">
		<h3
			class="text-5xl md:text-6xl font-extrabold text-gray-900 leading-tight"
		>
			Summer Tournament <span class="text-blue-700">2025</span>
		</h3>
		<p class="text-gray-700 text-xl md:text-2xl leading-relaxed font-light">
			Bersiaplah untuk turnamen basket terbesar tahun ini! Ayo daftar dan
			buktikan kemampuanmu di lapangan melawan tim terbaik dari seluruh
			Indonesia. Ini adalah kesempatanmu untuk bersinar, bertemu atlet
			hebat, dan meraih kejayaan!
		</p>
		<a
			href="#"
			class="inline-block bg-gradient-to-r from-blue-700 to-blue-900 text-white px-12 py-5 rounded-full font-bold text-xl hover:from-blue-800 hover:to-blue-950 transition duration-300 shadow-xl transform hover:-translate-y-1 hover:scale-105 focus:outline-none focus:ring-4 focus:ring-blue-300"
			>Ikuti Event Sekarang</a
		>
	</div>
</section>

---

<section
	class="mt-32 bg-gradient-to-br from-blue-50 to-blue-100 py-20 px-6 md:px-20 text-center rounded-t-[4rem] shadow-2xl relative overflow-hidden"
>
	<div
		class="absolute inset-0 bg-abstract-pattern opacity-10 pointer-events-none"
	></div>
	<h2 class="text-4xl md:text-5xl font-extrabold text-blue-800 mb-6">
		Jangan Ketinggalan Info Terbaru!
	</h2>
	<p class="text-gray-700 text-xl mb-12 max-w-4xl mx-auto leading-relaxed">
		Daftarkan email dan nomor WhatsApp kamu untuk mendapatkan informasi
		terkini mengenai **event eksklusif, promosi spesial**, dan berita
		terbaru dari Basketball Club langsung ke genggamanmu!
	</p>
	<form
		class="max-w-4xl mx-auto grid grid-cols-1 md:grid-cols-3 gap-6 relative z-10"
	>
		<input
			type="email"
			placeholder="Email kamu"
			class="px-6 py-4 rounded-full border border-gray-300 focus:outline-none focus:ring-4 focus:ring-blue-300 transition duration-300 shadow-md text-lg"
			aria-label="Email Address"
		/>
		<input
			type="text"
			placeholder="Nomor WhatsApp"
			class="px-6 py-4 rounded-full border border-gray-300 focus:outline-none focus:ring-4 focus:ring-blue-300 transition duration-300 shadow-md text-lg"
			aria-label="WhatsApp Number"
		/>
		<button
			type="submit"
			class="bg-gradient-to-r from-blue-600 to-blue-800 text-white font-bold px-10 py-4 rounded-full hover:from-blue-700 hover:to-blue-900 transition duration-300 shadow-xl transform hover:-translate-y-1 focus:outline-none focus:ring-4 focus:ring-blue-300 text-xl"
		>
			Subscribe Sekarang
		</button>
	</form>
</section>

<style>
	@import url("https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600;700;800&display=swap");

	body {
		font-family: "Poppins", sans-serif;
	}

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

	.bg-grid-pattern {
		background-image: url("data:image/svg+xml,%3Csvg width='6' height='6' viewBox='0 0 6 6' xmlns='http://www.w3.org/2000/svg'%3E%3Cg fill='%239C92AC' fill-opacity='0.1' fill-rule='evenodd'%3E%3Cpath d='M0 0h3v3H0V0zm3 3h3v3H3V3z'/%3E%3C/g%3E%3C/svg%3E");
	}

	.bg-dots-pattern {
		background-image: url("data:image/svg+xml,%3Csvg width='10' height='10' viewBox='0 0 10 10' xmlns='http://www.w3.org/2000/svg'%3E%3Ccircle cx='5' cy='5' r='1' fill='%23FFF' fill-opacity='0.1'/%3E%3C/svg%3E");
	}

	.bg-abstract-pattern {
		background-image: url("data:image/svg+xml,%3Csvg width='40' height='40' viewBox='0 0 40 40' xmlns='http://www.w3.org/2000/svg'%3E%3Cg fill='%236B7280' fill-opacity='0.05' fill-rule='evenodd'%3E%3Cpath d='M0 0h20v20H0V0zm20 20h20v20H20V20z'/%3E%3C/g%3E%3C/svg%3E");
		background-size: 20px 20px;
	}
</style>
