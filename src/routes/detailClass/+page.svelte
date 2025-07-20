<script lang="ts">
    // Define the type for a ClassOption (same as before)
    type ClassOption = {
        id: number;
        name: string;
        discount: number;
        price: number;
        originalPrice: number;
        image: string;
        description: string;
        // New fields for detail page
        fullDescription: string[]; // Array of paragraphs for more detail
        keyFeatures: string[]; // Bullet points for benefits/features
        schedule: string; // Example: "Every Monday & Wednesday, 7:00 PM - 9:00 PM"
        coach: {
            // Coach details
            name: string;
            bio: string;
            image: string;
        };
        galleryImages?: string[]; // Optional array of additional images
    };

    // This would ideally come from a data store or API based on a passed ID
    // For this example, we'll hardcode one class's details.
    // Ensure these image links are working placeholders or your own hosted images
    const classDetail: ClassOption = {
        id: 1,
        name: "Advanced Drills Squad",
        discount: 10,
        price: 150000,
        originalPrice: 165000,
        image: "https://images.ctfassets.net/xa93kvziwaye/MH0jddFJyXdc3MpfKF2OY/c7ba01415ea6d985da3e1b897b27184f/hero-image_nba-2k26s-cover-star-is-revealed.jpg?fm=webp&f=top&fit=fill&w=1124&h=506&q=50", // Main hero image for the class
        description:
            "Master complex techniques and elevate your game with intensive, high-level training.",
        fullDescription: [
            "Siap mendorong batas kemampuan Anda dan mendominasi lapangan? **Advanced Drills Squad** dirancang khusus untuk pemain serius yang ingin mencapai tingkat penguasaan tertinggi. Program ini fokus pada penyempurnaan teknik individu dan mengintegrasikannya ke dalam konsep tim yang lebih canggih.",
            "Sesi latihan kami berintensitas tinggi, mencakup segala hal mulai dari penguasaan bola yang presisi, mekanika tembakan yang dinamis, hingga skema pertahanan canggih dan pembuatan permainan ofensif. Dapatkan umpan balik yang personal dan latihan menantang yang mensimulasikan situasi permainan sesungguhnya. Bersiaplah untuk meningkatkan ketahanan mental dan kepemimpinan Anda di lapangan!",
        ],
        keyFeatures: [
            "Pelatihan Elit dari Pelatih Tingkat Profesional",
            "Latihan Intensitas Tinggi untuk Penguasaan Keterampilan",
            "Strategi Serangan & Pertahanan Tingkat Lanjut",
            "Analisis Performa yang Dipersonalisasi",
            "Latihan Game Kompetitif & Simulasi Pertandingan",
            "Fokus pada Ketangguhan Mental & Kepemimpinan",
        ],
        schedule: "Setiap Senin & Rabu, Pukul 19:00 - 21:00 WIB",
        coach: {
            name: "Coach Bima Perkasa",
            bio: "Coach Bima adalah legenda di kancah basket lokal, membawa lebih dari 15 tahun pengalaman bermain dan melatih profesional. Dikenal karena kecemerlangan taktisnya dan kemampuannya untuk mengembangkan bakat-bakat elit, dia berdedikasi untuk membuka potensi penuh setiap pemain.",
            image: "https://via.placeholder.com/150/00008b/ffffff?text=Coach+BP", // Placeholder for coach image
        },
        galleryImages: [
            "https://via.placeholder.com/800x600/34d399/ffffff?text=Sesi+Latihan+Intens",
            "https://via.placeholder.com/800x600/fbbf24/ffffff?text=Latihan+Tembakan+Presisi",
            "https://via.placeholder.com/800x600/60a5fa/ffffff?text=Diskusi+Taktik+Tim",
            "https://via.placeholder.com/800x600/c084fc/ffffff?text=Game+Simulasi",
        ],
    };

    // Function to handle the enrollment button click
    function handleEnroll() {
        alert(
            `Selamat! Anda akan mendaftar kelas ${classDetail.name}. Kami akan segera menghubungi Anda untuk detail pembayaran dan informasi selanjutnya.`,
        );
        // In a real application, this would redirect to a registration form or payment gateway.
    }
</script>

<div class="font-sans antialiased text-gray-800 bg-gray-100 min-h-screen">
    <header class="bg-blue-800 text-white p-4 shadow-md sticky top-0 z-50">
        <div class="container mx-auto flex justify-between items-center">
            <a
                href="/"
                class="text-2xl font-bold hover:text-yellow-400 transition duration-300"
            >
                Hardwood Heroes Academy
            </a>
            <nav>
                <a
                    href="/#class-selection"
                    class="ml-4 px-4 py-2 rounded-lg hover:bg-blue-700 transition duration-300"
                >
                    Kembali ke Pilihan Kelas
                </a>
            </nav>
        </div>
    </header>

    <main class="container mx-auto px-4 py-12">
        <section class="bg-white rounded-3xl shadow-xl overflow-hidden mb-12">
            <div class="relative">
                <img
                    src={classDetail.image}
                    alt={classDetail.name}
                    class="w-full h-96 md:h-[500px] object-cover object-center animate-fade-in-img"
                />
                <div
                    class="absolute inset-0 bg-gradient-to-t from-black/80 to-transparent flex items-end p-8 md:p-12"
                >
                    <div class="text-white">
                        <h1
                            class="text-5xl md:text-6xl font-extrabold mb-3 leading-tight animate-slide-in-up"
                        >
                            {classDetail.name}
                        </h1>
                        <p
                            class="text-xl md:text-2xl text-blue-100 animate-slide-in-up delay-100"
                        >
                            {classDetail.description}
                        </p>
                    </div>
                </div>
                <div
                    class="absolute top-6 right-6 bg-gradient-to-r from-red-600 to-pink-500
                           text-white text-xl md:text-2xl font-bold px-6 py-2.5 rounded-full shadow-lg
                           transform -rotate-6 z-10 animate-fade-in-delay-300"
                >
                    <i class="fas fa-tag mr-2"></i> Hemat {classDetail.discount}%!
                </div>
            </div>

            <div class="p-8 lg:p-12 grid grid-cols-1 lg:grid-cols-3 gap-10">
                <div class="lg:col-span-2">
                    <h2
                        class="text-3xl md:text-4xl font-extrabold text-gray-900 mb-6 border-b-4 border-blue-500 pb-2"
                    >
                        Tentang Kelas Ini
                    </h2>
                    {#each classDetail.fullDescription as paragraph}
                        <p class="text-lg text-gray-700 mb-5 leading-relaxed">
                            {@html paragraph}
                        </p>
                    {/each}

                    <h3
                        class="text-2xl md:text-3xl font-extrabold text-gray-900 mb-5 mt-10"
                    >
                        Apa yang Akan Anda Pelajari:
                    </h3>
                    <ul
                        class="grid grid-cols-1 md:grid-cols-2 gap-x-6 gap-y-3 list-none text-lg text-gray-700"
                    >
                        {#each classDetail.keyFeatures as feature}
                            <li class="flex items-start">
                                <svg
                                    xmlns="http://www.w3.org/2000/svg"
                                    class="h-7 w-7 text-blue-600 mr-3 flex-shrink-0 mt-1"
                                    fill="none"
                                    viewBox="0 0 24 24"
                                    stroke="currentColor"
                                >
                                    <path
                                        stroke-linecap="round"
                                        stroke-linejoin="round"
                                        stroke-width="2"
                                        d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z"
                                    />
                                </svg>
                                {feature}
                            </li>
                        {/each}
                    </ul>

                    {#if classDetail.galleryImages && classDetail.galleryImages.length > 0}
                        <h3
                            class="text-2xl md:text-3xl font-extrabold text-gray-900 mb-6 mt-12 border-b-4 border-blue-500 pb-2"
                        >
                            Galeri Kelas
                        </h3>
                        <div class="grid grid-cols-1 sm:grid-cols-2 gap-6">
                            {#each classDetail.galleryImages as img}
                                <div
                                    class="bg-gray-200 rounded-lg overflow-hidden shadow-md group"
                                >
                                    <img
                                        src={img}
                                        alt="Class Gallery"
                                        class="w-full h-64 object-cover transform group-hover:scale-105 transition-transform duration-300 ease-out"
                                    />
                                </div>
                            {/each}
                        </div>
                    {/if}
                </div>

                <aside
                    class="lg:col-span-1 bg-blue-50 p-8 rounded-3xl shadow-xl border border-blue-200 h-fit sticky top-28 animate-slide-in-right"
                >
                    <h3 class="text-3xl font-extrabold text-blue-800 mb-6">
                        Detail Pendaftaran
                    </h3>

                    <div class="mb-6 pb-4 border-b border-blue-200">
                        <p class="text-xl text-gray-700 font-semibold mb-2">
                            Harga Investasi:
                        </p>
                        <div class="flex items-baseline mb-2">
                            <span
                                class="text-5xl md:text-6xl font-extrabold text-blue-700 leading-none"
                            >
                                Rp{classDetail.price.toLocaleString("id-ID")}
                            </span>
                            {#if classDetail.discount > 0}
                                <span
                                    class="text-lg text-gray-500 line-through ml-3"
                                >
                                    Rp{classDetail.originalPrice.toLocaleString(
                                        "id-ID",
                                    )}
                                </span>
                            {/if}
                        </div>
                        {#if classDetail.discount > 0}
                            <p class="text-base text-red-600 font-bold mt-2">
                                Anda menghemat sebesar Rp{(
                                    classDetail.originalPrice -
                                    classDetail.price
                                ).toLocaleString("id-ID")}! Manfaatkan penawaran
                                spesial ini!
                            </p>
                        {/if}
                    </div>

                    <div class="mb-6 pb-4 border-b border-blue-200">
                        <p class="text-xl text-gray-700 font-semibold mb-2">
                            Jadwal Kelas Eksklusif:
                        </p>
                        <p
                            class="text-2xl font-bold text-blue-600 flex items-center"
                        >
                            <svg
                                xmlns="http://www.w3.org/2000/svg"
                                class="h-7 w-7 mr-3 text-blue-500"
                                fill="none"
                                viewBox="0 0 24 24"
                                stroke="currentColor"
                            >
                                <path
                                    stroke-linecap="round"
                                    stroke-linejoin="round"
                                    stroke-width="2"
                                    d="M8 7V3m8 4V3m-9 8h10M5 21h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v12a2 2 0 002 2z"
                                />
                            </svg>
                            {classDetail.schedule}
                        </p>
                    </div>

                    <div
                        class="mb-8 p-5 bg-white rounded-xl shadow-inner border border-gray-200"
                    >
                        <p class="text-xl text-gray-800 font-semibold mb-3">
                            Temui Pelatih Anda:
                        </p>
                        <div class="flex items-center mb-4">
                            <img
                                src={classDetail.coach.image}
                                alt={classDetail.coach.name}
                                class="w-24 h-24 rounded-full object-cover mr-5 ring-4 ring-blue-400 border-2 border-white shadow-md"
                            />
                            <div>
                                <h4 class="text-2xl font-bold text-gray-900">
                                    {classDetail.coach.name}
                                </h4>
                                <p class="text-base text-gray-600 mt-1">
                                    {classDetail.coach.bio}
                                </p>
                            </div>
                        </div>
                    </div>

                    <button
                        on:click={handleEnroll}
                        class="w-full bg-blue-600 hover:bg-blue-700 text-white font-bold py-5 px-8 rounded-xl
                               text-2xl transition duration-300 transform hover:scale-105 shadow-xl
                               flex items-center justify-center animate-bounce-btn"
                    >
                        <svg
                            xmlns="http://www.w3.org/2000/svg"
                            class="h-9 w-9 mr-4"
                            fill="none"
                            viewBox="0 0 24 24"
                            stroke="currentColor"
                        >
                            <path
                                stroke-linecap="round"
                                stroke-linejoin="round"
                                stroke-width="2"
                                d="M18 9v3m0 0v3m0-3h3m-3 0h-3m-6-3h2m-2 0h-2m2 0V9m0 3v3m0-3a2 2 0 110-4 2 2 0 010 4zm0 0V9a2 2 0 100 4zm0 0h2a2 2 0 100 4h-2zm0 0v2a2 2 0 100-4zM6 18a2 2 0 100-4 2 2 0 000 4z"
                            />
                        </svg>
                        Daftar Sekarang Juga!
                    </button>
                    <p class="text-center text-gray-600 text-sm mt-4 italic">
                        Amankan posisi Anda sebelum terlambat. Kuota terbatas!
                    </p>
                </aside>
            </div>
        </section>
    </main>

    <footer class="bg-gray-900 text-gray-400 py-10 text-center">
        <div class="container mx-auto px-6">
            <p class="mb-4">
                &copy; 2025 Hardwood Heroes Academy. All rights reserved.
            </p>
            <div
                class="flex flex-col sm:flex-row justify-center space-y-2 sm:space-y-0 sm:space-x-8 text-sm"
            >
                <a
                    href="#"
                    class="hover:text-white transition-colors duration-200"
                    >Kebijakan Privasi</a
                >
                <a
                    href="#"
                    class="hover:text-white transition-colors duration-200"
                    >Syarat & Ketentuan</a
                >
                <a
                    href="#"
                    class="hover:text-white transition-colors duration-200"
                    >Hubungi Kami</a
                >
            </div>
        </div>
    </footer>
</div>

<style>
    /* Ensure you link Font Awesome for icons, e.g., in your main HTML file's <head> */
    /* <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.3/css/all.min.css" integrity="sha512-..." crossorigin="anonymous" referrerpolicy="no-referrer" /> */

    @keyframes fadeInImg {
        from {
            opacity: 0;
            transform: translateY(20px);
        }
        to {
            opacity: 1;
            transform: translateY(0);
        }
    }

    @keyframes slideInUp {
        from {
            opacity: 0;
            transform: translateY(40px);
        }
        to {
            opacity: 1;
            transform: translateY(0);
        }
    }

    @keyframes slideInRight {
        from {
            opacity: 0;
            transform: translateX(50px);
        }
        to {
            opacity: 1;
            transform: translateX(0);
        }
    }

    @keyframes fadeInDelay {
        0% {
            opacity: 0;
        }
        50% {
            opacity: 0;
        } /* Delay */
        100% {
            opacity: 1;
        }
    }

    @keyframes bounceBtn {
        0%,
        100% {
            transform: translateY(0) scale(1);
        }
        50% {
            transform: translateY(-5px) scale(1.02);
        }
    }

    .animate-fade-in-img {
        animation: fadeInImg 1s ease-out forwards;
    }
    .animate-slide-in-up {
        animation: slideInUp 1s ease-out forwards;
    }
    .animate-slide-in-up.delay-100 {
        animation-delay: 0.1s;
    } /* Small delay for text */
    .animate-fade-in-delay-300 {
        animation: fadeInDelay 1.5s ease-out forwards;
        animation-delay: 0.3s;
    } /* Longer delay for badge */
    .animate-slide-in-right {
        animation: slideInRight 0.8s ease-out forwards;
    }
    .animate-bounce-btn {
        animation: bounceBtn 1.8s infinite ease-in-out;
    }
</style>
