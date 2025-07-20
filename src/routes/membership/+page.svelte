<script lang="ts">
    import { fade, slide } from "svelte/transition";
    import { cubicOut } from "svelte/easing";

    // Team members data (dummy images for demonstration)
    import player1 from "$lib/images/dharma.jpeg"; // Replace with actual player images
    import player2 from "$lib/images/reno.jpeg";
    import player3 from "$lib/images/silvia.jpg";

    const teamMembers = [
        { name: "Andi Wijaya", role: "Kapten Tim", image: player1 },
        { name: "Budi Santoso", role: "Point Guard", image: player2 },
        { name: "Citra Dewi", role: "Shooting Guard", image: player3 },
    ];

    // Intersection Observer for animations
    let showTeam = false;
    let showActivities = false;

    function inView(node: Element, targetVar: "showTeam" | "showActivities") {
        const observer = new IntersectionObserver(
            (entries) => {
                entries.forEach((entry) => {
                    if (entry.isIntersecting) {
                        if (targetVar === "showTeam") showTeam = true;
                        if (targetVar === "showActivities")
                            showActivities = true;
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
</script>

<svelte:head>
    <title>Membership | Basketball Club</title>
</svelte:head>

<section
    class="relative bg-center bg-cover text-white py-32 px-6 text-center overflow-hidden"
    style="background-image: url('https://images.unsplash.com/photo-1627627256672-027a4613d028?q=80&w=1174&auto=format&fit=crop'); background-size: cover; background-position: center;"
>
    <div
        class="absolute inset-0 bg-gradient-to-t from-black/80 to-black/40"
    ></div>
    <div class="relative z-10 max-w-4xl mx-auto">
        <h1 class="text-5xl md:text-6xl font-extrabold mb-6 drop-shadow-lg">
            Gabung sebagai Member Resmi
        </h1>
        <p class="text-xl md:text-2xl max-w-3xl mx-auto opacity-90 font-light">
            Dapatkan akses eksklusif ke **pelatihan intensif, event spesial,
            merchandise terbaru**, dan menjadi bagian dari komunitas basket
            terbaik se-Indonesia.
        </p>
    </div>
</section>

---

<section class="py-24 px-6 md:px-16 max-w-7xl mx-auto font-sans">
    <h2 class="text-4xl md:text-5xl font-bold text-center mb-16 text-gray-900">
        Pilih Paket Membership Anda
    </h2>
    <div class="grid grid-cols-1 md:grid-cols-3 gap-12">
        <div
            class="bg-white rounded-2xl shadow-xl p-8 border border-blue-200 hover:border-blue-500 transform hover:-translate-y-2 transition-all duration-300 relative overflow-hidden group"
        >
            <div
                class="absolute top-0 left-0 w-full h-2 bg-blue-500 rounded-t-2xl"
            ></div>
            <h3 class="text-3xl font-bold text-blue-700 mb-4">Basic</h3>
            <p class="text-gray-600 mb-6 text-lg">
                Cocok untuk pemula yang ingin mulai membangun dasar kemampuan
                dan rutin berlatih.
            </p>
            <ul class="space-y-3 text-gray-800 mb-8 text-base">
                <li class="flex items-center">
                    <span class="text-green-500 mr-2 text-xl">✔</span> Akses latihan
                    mingguan (2x)
                </li>
                <li class="flex items-center">
                    <span class="text-green-500 mr-2 text-xl">✔</span> Grup WhatsApp
                    komunitas & diskusi
                </li>
                <li class="flex items-center opacity-70">
                    <span class="text-red-500 mr-2 text-xl">✖</span> Tiket event
                    gratis
                </li>
                <li class="flex items-center opacity-70">
                    <span class="text-red-500 mr-2 text-xl">✖</span> Prioritas pendaftaran
                    turnamen
                </li>
            </ul>
            <div class="text-4xl font-extrabold text-gray-900 mb-8">
                Rp150.000<span class="text-xl font-medium text-gray-500"
                    >/bulan</span
                >
            </div>
            <a
                href="#form"
                class="block bg-blue-600 text-white text-center py-4 rounded-full font-bold text-lg shadow-lg hover:bg-blue-700 transition transform hover:scale-105"
                >Daftar Basic</a
            >
        </div>

        <div
            class="bg-white rounded-2xl shadow-2xl p-8 border-4 border-yellow-500 transform scale-105 relative overflow-hidden animate-pulse-border"
        >
            <div
                class="absolute -top-4 left-1/2 -translate-x-1/2 bg-yellow-500 text-white text-sm font-bold px-5 py-2 rounded-b-lg shadow-md"
            >
                Paling Populer
            </div>
            <h3 class="text-3xl font-bold text-yellow-700 mb-4 mt-4">Pro</h3>
            <p class="text-gray-700 mb-6 text-lg">
                Pilihan terbaik untuk atlet serius yang ingin akses penuh,
                pengembangan skill, dan peluang bertanding.
            </p>
            <ul class="space-y-3 text-gray-800 mb-8 text-base">
                <li class="flex items-center">
                    <span class="text-green-500 mr-2 text-xl">✔</span> Akses latihan
                    harian (4x)
                </li>
                <li class="flex items-center">
                    <span class="text-green-500 mr-2 text-xl">✔</span> Jersey eksklusif
                    klub gratis
                </li>
                <li class="flex items-center">
                    <span class="text-green-500 mr-2 text-xl">✔</span> Tiket 2 event
                    gratis per tahun
                </li>
                <li class="flex items-center">
                    <span class="text-green-500 mr-2 text-xl">✔</span> Prioritas
                    pendaftaran turnamen
                </li>
            </ul>
            <div class="text-4xl font-extrabold text-gray-900 mb-8">
                Rp300.000<span class="text-xl font-medium text-gray-500"
                    >/bulan</span
                >
            </div>
            <a
                href="#form"
                class="block bg-yellow-500 text-gray-900 text-center py-4 rounded-full font-bold text-lg shadow-lg hover:bg-yellow-600 transition transform hover:scale-105"
                >Daftar Pro</a
            >
        </div>

        <div
            class="bg-white rounded-2xl shadow-xl p-8 border border-blue-200 hover:border-blue-500 transform hover:-translate-y-2 transition-all duration-300 relative overflow-hidden group"
        >
            <div
                class="absolute top-0 left-0 w-full h-2 bg-blue-500 rounded-t-2xl"
            ></div>
            <h3 class="text-3xl font-bold text-blue-700 mb-4">Elite</h3>
            <p class="text-gray-600 mb-6 text-lg">
                Untuk member yang memiliki ambisi tampil di tingkat nasional &
                internasional.
            </p>
            <ul class="space-y-3 text-gray-800 mb-8 text-base">
                <li class="flex items-center">
                    <span class="text-green-500 mr-2 text-xl">✔</span> Semua fitur
                    Paket Pro
                </li>
                <li class="flex items-center">
                    <span class="text-green-500 mr-2 text-xl">✔</span> Konsultasi
                    personal dengan pelatih kepala
                </li>
                <li class="flex items-center">
                    <span class="text-green-500 mr-2 text-xl">✔</span> Undangan
                    turnamen eksklusif & scouting
                </li>
                <li class="flex items-center">
                    <span class="text-green-500 mr-2 text-xl">✔</span> Prioritas
                    utama pendaftaran turnamen
                </li>
            </ul>
            <div class="text-4xl font-extrabold text-gray-900 mb-8">
                Rp500.000<span class="text-xl font-medium text-gray-500"
                    >/bulan</span
                >
            </div>
            <a
                href="#form"
                class="block bg-blue-600 text-white text-center py-4 rounded-full font-bold text-lg shadow-lg hover:bg-blue-700 transition transform hover:scale-105"
                >Daftar Elite</a
            >
        </div>
    </div>
</section>

---

<section
    class="py-24 px-6 md:px-16 max-w-7xl mx-auto bg-gray-50 rounded-3xl shadow-inner mt-20"
    use:inView={"showTeam"}
>
    <h2
        class="text-4xl md:text-5xl font-extrabold text-center mb-16 text-gray-900"
    >
        Kenali Tim Kami
    </h2>
    <div class="flex flex-wrap justify-center gap-10">
        {#if showTeam}
            {#each teamMembers as member, i}
                <div
                    class="w-full sm:w-1/2 md:w-1/3 lg:w-1/4 bg-white rounded-2xl shadow-lg p-6 text-center transform transition-all duration-500 hover:scale-105 hover:shadow-xl"
                    in:fade={{ delay: i * 150, duration: 800 }}
                >
                    <img
                        src={member.image}
                        alt={member.name}
                        class="w-36 h-36 rounded-full mx-auto object-cover mb-4 border-4 border-blue-500 shadow-md"
                    />
                    <h3 class="text-2xl font-bold text-gray-900 mb-1">
                        {member.name}
                    </h3>
                    <p class="text-blue-600 font-semibold">{member.role}</p>
                </div>
            {/each}
        {/if}
    </div>
    <div class="text-center mt-12">
        <p class="text-xl text-gray-700 mb-4">
            Total Anggota Aktif: <strong class="text-blue-700">150+</strong>
        </p>
        <p class="text-xl text-gray-700">
            Tim Nasional: <strong class="text-blue-700"
                >2 Tim Putra, 1 Tim Putri</strong
            >
        </p>
    </div>
</section>

---

<section class="py-24 px-6 md:px-16 max-w-7xl mx-auto">
    <h2
        class="text-4xl md:text-5xl font-extrabold text-center mb-16 text-gray-900"
    >
        Prestasi Gemilang Kami
    </h2>
    <div class="grid grid-cols-1 md:grid-cols-2 gap-12 items-center">
        <div class="space-y-8">
            <div class="flex items-start bg-blue-50 p-6 rounded-xl shadow-md">
                <span class="text-blue-600 text-4xl mr-4">🏆</span>
                <div>
                    <h3 class="text-2xl font-bold text-gray-900 mb-2">
                        Juara Nasional Liga Basket (2023, 2024)
                    </h3>
                    <p class="text-gray-700">
                        Tim putra kami berhasil mempertahankan gelar juara liga
                        basket nasional dua tahun berturut-turut!
                    </p>
                </div>
            </div>
            <div class="flex items-start bg-yellow-50 p-6 rounded-xl shadow-md">
                <span class="text-yellow-600 text-4xl mr-4">🏅</span>
                <div>
                    <h3 class="text-2xl font-bold text-gray-900 mb-2">
                        Pemain Terbaik Tahun Ini (MVP)
                    </h3>
                    <p class="text-gray-700">
                        Salah satu bintang kami, Budi Santoso, meraih
                        penghargaan MVP liga di musim terakhir.
                    </p>
                </div>
            </div>
            <div class="flex items-start bg-green-50 p-6 rounded-xl shadow-md">
                <span class="text-green-600 text-4xl mr-4">🌟</span>
                <div>
                    <h3 class="text-2xl font-bold text-gray-900 mb-2">
                        Tim Putri Finalis Turnamen Internasional
                    </h3>
                    <p class="text-gray-700">
                        Tim putri kami menunjukkan performa luar biasa hingga
                        mencapai babak final di turnamen tingkat Asia.
                    </p>
                </div>
            </div>
        </div>
        <div class="relative group">
            <img
                src="https://images.unsplash.com/photo-1546519638-68e109498ffc?q=80&w=1920&auto=format&fit=crop"
                alt="Prestasi Tim"
                class="rounded-2xl shadow-2xl w-full h-[400px] object-cover border-4 border-blue-500 transform transition duration-500 hover:scale-102 hover:shadow-3xl"
            />
            <div
                class="absolute inset-0 bg-blue-800 opacity-0 rounded-2xl group-hover:opacity-10 transition-opacity duration-300"
            ></div>
        </div>
    </div>
</section>

---

<section
    class="py-24 px-6 md:px-16 max-w-7xl mx-auto bg-blue-50 rounded-3xl shadow-inner mt-20"
    use:inView={"showActivities"}
>
    <h2
        class="text-4xl md:text-5xl font-extrabold text-center mb-16 text-gray-900"
    >
        Aktivitas Klub Kami
    </h2>
    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-10">
        {#if showActivities}
            <div
                class="bg-white rounded-2xl shadow-lg p-6 text-center transform transition-all duration-500 hover:scale-105 hover:shadow-xl"
                in:fade={{ delay: 100, duration: 800 }}
            >
                <img
                    src="https://image.kemenpora.go.id/images/content/2022/09/19/2571/19Ketua-DPR-Harap-Turnamen-Bola-Basket-Antar-Perguruan-Tinggi-se-Indonesia-Bangkitkan-Prestasi-dan-Semangat-Berolahragash.jpeg"
                    alt="Latihan Rutin"
                    class="w-full h-48 object-cover rounded-xl mb-4 shadow-md"
                />
                <h3 class="text-2xl font-bold text-gray-900 mb-2">
                    Latihan Rutin
                </h3>
                <p class="text-gray-700">
                    Sesi latihan intensif dan terstruktur setiap minggu di
                    fasilitas terbaik.
                </p>
            </div>
            <div
                class="bg-white rounded-2xl shadow-lg p-6 text-center transform transition-all duration-500 hover:scale-105 hover:shadow-xl"
                in:fade={{ delay: 300, duration: 800 }}
            >
                <img
                    src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSkhONjGH0J9ksgr9sYYIOGQOJkXfzJOeQqzA&s"
                    alt="Turnamen Internal"
                    class="w-full h-48 object-cover rounded-xl mb-4 shadow-md"
                />
                <h3 class="text-2xl font-bold text-gray-900 mb-2">
                    Turnamen Internal
                </h3>
                <p class="text-gray-700">
                    Ajang kompetisi seru antar anggota untuk mengasah kemampuan
                    dan sportivitas.
                </p>
            </div>
            <div
                class="bg-white rounded-2xl shadow-lg p-6 text-center transform transition-all duration-500 hover:scale-105 hover:shadow-xl"
                in:fade={{ delay: 500, duration: 800 }}
            >
                <img
                    src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRrZwS_sxbdWJ8KTLiJ53bdvvhggcdqsSFoNw&s"
                    alt="Gathering Komunitas"
                    class="w-full h-48 object-cover rounded-xl mb-4 shadow-md"
                />
                <h3 class="text-2xl font-bold text-gray-900 mb-2">
                    Gathering Komunitas
                </h3>
                <p class="text-gray-700">
                    Acara santai untuk mempererat tali persaudaraan dan berbagi
                    pengalaman di luar lapangan.
                </p>
            </div>
        {/if}
    </div>
</section>

---

<section id="form" class="bg-gray-800 py-24 px-6 md:px-16 mt-20 font-sans">
    <h2 class="text-4xl md:text-5xl font-bold text-center mb-12 text-white">
        Daftarkan Dirimu Sekarang!
    </h2>
    <p class="text-lg text-gray-300 text-center mb-10 max-w-2xl mx-auto">
        Isi formulir di bawah ini untuk memulai perjalananmu bersama Basketball
        Club. Tim kami akan segera menghubungimu!
    </p>
    <form
        class="max-w-2xl mx-auto bg-white p-10 rounded-2xl shadow-2xl space-y-8"
        in:slide={{ duration: 700, easing: cubicOut }}
    >
        <div>
            <label for="fullName" class="block font-semibold mb-3 text-gray-800"
                >Nama Lengkap <span class="text-red-500">*</span></label
            >
            <input
                type="text"
                id="fullName"
                name="fullName"
                required
                class="w-full px-5 py-3 border border-gray-300 rounded-lg focus:outline-none focus:ring-4 focus:ring-blue-200 transition duration-200 text-lg"
                placeholder="Masukkan nama lengkap Anda"
            />
        </div>
        <div>
            <label for="email" class="block font-semibold mb-3 text-gray-800"
                >Email <span class="text-red-500">*</span></label
            >
            <input
                type="email"
                id="email"
                name="email"
                required
                class="w-full px-5 py-3 border border-gray-300 rounded-lg focus:outline-none focus:ring-4 focus:ring-blue-200 transition duration-200 text-lg"
                placeholder="email@example.com"
            />
        </div>
        <div>
            <label for="whatsapp" class="block font-semibold mb-3 text-gray-800"
                >No WhatsApp <span class="text-red-500">*</span></label
            >
            <input
                type="text"
                id="whatsapp"
                name="whatsapp"
                required
                class="w-full px-5 py-3 border border-gray-300 rounded-lg focus:outline-none focus:ring-4 focus:ring-blue-200 transition duration-200 text-lg"
                placeholder="Contoh: 081234567890"
            />
        </div>
        <div>
            <label
                for="membershipPlan"
                class="block font-semibold mb-3 text-gray-800"
                >Paket Pilihan <span class="text-red-500">*</span></label
            >
            <select
                id="membershipPlan"
                name="membershipPlan"
                required
                class="w-full px-5 py-3 border border-gray-300 rounded-lg focus:outline-none focus:ring-4 focus:ring-blue-200 transition duration-200 bg-white text-lg appearance-none cursor-pointer"
            >
                <option value="" disabled selected
                    >-- Pilih Paket Anda --</option
                >
                <option value="Basic">Basic - Rp150.000/bulan</option>
                <option value="Pro">Pro - Rp300.000/bulan</option>
                <option value="Elite">Elite - Rp500.000/bulan</option>
            </select>
        </div>
        <button
            type="submit"
            class="w-full bg-blue-600 text-white py-4 rounded-full font-bold text-xl shadow-lg hover:bg-blue-700 transition transform hover:scale-105 focus:outline-none focus:ring-4 focus:ring-blue-300"
            >Kirim Pendaftaran</button
        >
    </form>
</section>

<style>
    @import url("https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600;700;800&display=swap");

    /* Apply Poppins font globally */
    body {
        font-family: "Poppins", sans-serif;
    }

    /* Custom animation for popular package border pulse */
    @keyframes pulse-border {
        0% {
            border-color: #fcd34d; /* yellow-300 */
            box-shadow: 0 0 0 0 rgba(252, 211, 77, 0.7);
        }
        50% {
            border-color: #f59e0b; /* yellow-500 */
            box-shadow: 0 0 0 10px rgba(245, 158, 11, 0);
        }
        100% {
            border-color: #fcd34d; /* yellow-300 */
            box-shadow: 0 0 0 0 rgba(252, 211, 77, 0.7);
        }
    }

    .animate-pulse-border {
        animation: pulse-border 2s infinite ease-in-out;
    }

    /* Custom styles for select arrow */
    select {
        -webkit-appearance: none;
        -moz-appearance: none;
        appearance: none;
        background-image: url("data:image/svg+xml;charset=US-ASCII,%3Csvg xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22 width%3D%22292.4%22 height%3D%22292.4%22 viewBox%3D%220 0 292.4 292.4%22%3E%3Cpath fill%3D%22%236B7280%22 d%3D%22M287 69.4a17.6 17.6 0 0 0-25.3 0L146.2 189.9 30.7 69.4a17.6 17.6 0 0 0-25.3 0c-6.8 6.8-6.8 17.7 0 24.5l130.4 129.9c3.4 3.4 8 5.2 12.6 5.2s9.2-1.8 12.6-5.2l130.4-129.9c6.9-6.8 6.9-17.7.1-24.5z%22%2F%3E%3C%2Fsvg%3E");
        background-repeat: no-repeat;
        background-position: right 1rem center;
        background-size: 1em;
        padding-right: 3rem; /* Make space for the custom arrow */
    }
</style>
