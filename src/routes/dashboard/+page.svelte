<script lang="ts">
    import {
        User,
        CalendarDays,
        Mail,
        MessageCircle,
        Activity,
        Bell,
        Settings,
        Users,
        Trophy,
        DollarSign,
        ArrowRight,
        BarChart2,
        Clock,
    } from "lucide-svelte";

    // --- Mock Data ---
    const userName = "Aji Setiaji";
    const userAvatarUrl = "https://i.pravatar.cc/150?img=8";

    // Summary Metrics
    const totalMembers = 1250;
    const totalEvents = 45;
    const newEmailSubscriptionsToday = 12;
    const newWhatsappSubscriptionsToday = 8;
    const totalRevenueThisMonth = 75000000; // IDR

    // Recent Activities (mock data)
    const recentActivities = [
        {
            id: 1,
            description: "Anggota baru 'Budi Santoso' bergabung.",
            time: "2 jam lalu",
            icon: User,
            color: "text-blue-500",
        },
        {
            id: 2,
            description: "Acara 'Turnamen Basket' ditambahkan.",
            time: "5 jam lalu",
            icon: CalendarDays,
            color: "text-purple-500",
        },
        {
            id: 3,
            description: "Pengaturan notifikasi diperbarui.",
            time: "1 hari lalu",
            icon: Bell,
            color: "text-orange-500",
        },
        {
            id: 4,
            description: "Pembayaran Rp 150.000 dari 'Siti Aminah' diterima.",
            time: "2 hari lalu",
            icon: DollarSign,
            color: "text-green-500",
        },
        {
            id: 5,
            description: "Tim 'Phoenix Flames' memperbarui profil.",
            time: "3 hari lalu",
            icon: Trophy,
            color: "text-yellow-500",
        },
    ];

    // Quick Links/Actions
    const quickLinks = [
        { name: "Lihat Profil", icon: User, href: "#" }, // Replace # with actual routes
        { name: "Daftar Anggota", icon: Users, href: "#" },
        { name: "Acara Mendatang", icon: CalendarDays, href: "#" },
        { name: "Pengaturan Akun", icon: Settings, href: "#" },
    ];

    // Utility function for currency formatting
    function formatCurrency(amount: number) {
        return new Intl.NumberFormat("id-ID", {
            style: "currency",
            currency: "IDR",
            minimumFractionDigits: 0,
        }).format(amount);
    }
</script>

<section class="min-h-screenpy-16 px-4 sm:px-6 lg:px-8">
    <div class="max-w-7xl mx-auto">
        <!-- Dashboard Header -->
        <header
            class="mb-12 flex flex-col sm:flex-row items-center justify-between gap-6"
        >
            <div class="flex items-center gap-4 text-center sm:text-left">
                <img
                    src={userAvatarUrl}
                    alt="Foto Profil Pengguna"
                    class="w-20 h-20 rounded-full border-4 border-indigo-400 shadow-md object-cover"
                />
                <div>
                    <h1
                        class="text-4xl font-extrabold text-gray-900 leading-tight"
                    >
                        Halo, {userName}!
                    </h1>
                    <p class="text-lg text-gray-700">
                        Selamat datang kembali di dashboard Anda.
                    </p>
                </div>
            </div>
            <button
                class="bg-indigo-600 hover:bg-indigo-700 text-white font-semibold py-3 px-6 rounded-xl transition-colors duration-200 shadow-md flex items-center gap-2"
                on:click={() => alert("Tombol Aksi Cepat diklik!")}
            >
                <Activity class="w-5 h-5" /> Aksi Cepat
            </button>
        </header>

        <!-- Summary Metrics Grid -->
        <div
            class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 xl:grid-cols-5 gap-6 mb-12"
        >
            <div
                class="bg-white p-6 rounded-2xl shadow-lg flex flex-col items-center justify-center text-center transform hover:scale-105 transition-transform duration-300"
            >
                <Users class="w-10 h-10 text-blue-500 mb-3" />
                <p class="text-sm text-gray-500 font-medium">Total Anggota</p>
                <p class="text-3xl font-bold text-gray-900">{totalMembers}</p>
            </div>
            <div
                class="bg-white p-6 rounded-2xl shadow-lg flex flex-col items-center justify-center text-center transform hover:scale-105 transition-transform duration-300"
            >
                <CalendarDays class="w-10 h-10 text-purple-500 mb-3" />
                <p class="text-sm text-gray-500 font-medium">Acara Mendatang</p>
                <p class="text-3xl font-bold text-gray-900">{totalEvents}</p>
            </div>
            <div
                class="bg-white p-6 rounded-2xl shadow-lg flex flex-col items-center justify-center text-center transform hover:scale-105 transition-transform duration-300"
            >
                <Mail class="w-10 h-10 text-indigo-500 mb-3" />
                <p class="text-sm text-gray-500 font-medium">
                    Langganan Email (Hari Ini)
                </p>
                <p class="text-3xl font-bold text-gray-900">
                    {newEmailSubscriptionsToday}
                </p>
            </div>
            <div
                class="bg-white p-6 rounded-2xl shadow-lg flex flex-col items-center justify-center text-center transform hover:scale-105 transition-transform duration-300"
            >
                <MessageCircle class="w-10 h-10 text-green-500 mb-3" />
                <p class="text-sm text-gray-500 font-medium">
                    Langganan WA (Hari Ini)
                </p>
                <p class="text-3xl font-bold text-gray-900">
                    {newWhatsappSubscriptionsToday}
                </p>
            </div>
            <div
                class="bg-white p-6 rounded-2xl shadow-lg flex flex-col items-center justify-center text-center transform hover:scale-105 transition-transform duration-300"
            >
                <DollarSign class="w-10 h-10 text-emerald-500 mb-3" />
                <p class="text-sm text-gray-500 font-medium">
                    Pendapatan Bulan Ini
                </p>
                <p class="text-3xl font-bold text-gray-900">
                    {formatCurrency(totalRevenueThisMonth)}
                </p>
            </div>
        </div>

        <!-- Main Content Grid (Recent Activity & Quick Links) -->
        <div class="grid grid-cols-1 lg:grid-cols-3 gap-8">
            <!-- Recent Activity Card -->
            <div class="lg:col-span-2 bg-white rounded-3xl shadow-xl p-8">
                <h2
                    class="text-3xl font-bold text-gray-800 mb-6 flex items-center gap-3"
                >
                    <Activity class="w-8 h-8 text-red-500" /> Aktivitas Terbaru
                </h2>
                <div class="space-y-4">
                    {#each recentActivities as activity (activity.id)}
                        <div
                            class="flex items-start gap-4 p-4 rounded-lg hover:bg-gray-50 transition-colors duration-200"
                        >
                            <svelte:component
                                this={activity.icon}
                                class={`w-6 h-6 ${activity.color} flex-shrink-0 mt-1`}
                            />
                            <div class="flex-1">
                                <p class="text-gray-800 font-medium text-lg">
                                    {activity.description}
                                </p>
                                <p
                                    class="text-sm text-gray-500 flex items-center gap-1 mt-1"
                                >
                                    <Clock class="w-4 h-4" />
                                    {activity.time}
                                </p>
                            </div>
                        </div>
                    {/each}
                </div>
                <button
                    class="mt-8 w-full bg-gray-100 hover:bg-gray-200 text-gray-700 font-semibold py-3 rounded-lg transition-colors duration-200 flex items-center justify-center gap-2"
                    on:click={() => alert("Lihat Semua Aktivitas diklik!")}
                >
                    Lihat Semua Aktivitas <ArrowRight class="w-4 h-4" />
                </button>
            </div>

            <!-- Quick Links Card -->
            <div class="bg-white rounded-3xl shadow-xl p-8">
                <h2
                    class="text-3xl font-bold text-gray-800 mb-6 flex items-center gap-3"
                >
                    <Bell class="w-8 h-8 text-teal-500" /> Tautan Cepat
                </h2>
                <div class="space-y-4">
                    {#each quickLinks as link}
                        <a
                            href={link.href}
                            class="flex items-center gap-4 p-4 rounded-lg bg-gray-50 hover:bg-gray-100 transition-colors duration-200 group"
                        >
                            <svelte:component
                                this={link.icon}
                                class="w-6 h-6 text-indigo-600 group-hover:text-indigo-800 transition-colors duration-200"
                            />
                            <span
                                class="text-lg font-medium text-gray-800 group-hover:text-gray-900 transition-colors duration-200 flex-1"
                                >{link.name}</span
                            >
                            <ArrowRight
                                class="w-5 h-5 text-gray-500 group-hover:translate-x-1 transition-transform duration-200"
                            />
                        </a>
                    {/each}
                </div>
            </div>
        </div>

        <!-- Optional: Placeholder for a Chart/Graph -->
        <div class="mt-12 bg-white rounded-3xl shadow-xl p-8">
            <h2
                class="text-3xl font-bold text-gray-800 mb-6 flex items-center gap-3"
            >
                <BarChart2 class="w-8 h-8 text-cyan-500" /> Statistik Pertumbuhan
            </h2>
            <div
                class="h-64 bg-gray-100 rounded-lg flex items-center justify-center text-gray-500 text-lg"
            >
                Grafik akan ditampilkan di sini (misalnya, pertumbuhan anggota,
                tren pendapatan)
            </div>
        </div>
    </div>
</section>
