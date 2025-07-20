<script lang="ts">
    import { Users, UserRound, Trophy, Calendar, Search } from "lucide-svelte"; // Removed Basketball, added other relevant icons

    // --- Mock Data ---
    // In a real application, this data would come from your backend API
    const generateTeams = (count: number) => {
        const teams = [];
        const teamNames = [
            "Phoenix Flames",
            "Thunderbolts",
            "Oceanic Waves",
            "Mountain Lions",
            "Desert Scorpions",
            "City Hawks",
            "River Dragons",
            "Starlight Knights",
            "Crimson Raptors",
            "Emerald Guardians",
            "Blaze Bisons",
            "Arctic Wolves",
            "Iron Giants",
            "Shadow Serpents",
            "Cosmic Comets",
            "Vortex Vipers",
            "Golden Grizzlies",
            "Silver Streaks",
            "Dark Matter",
            "Nebula Nomads",
        ];
        const coachNames = [
            "Coach Budi",
            "Coach Siti",
            "Coach Adi",
            "Coach Maya",
            "Coach Rio",
            "Coach Lina",
            "Coach Doni",
            "Coach Sari",
        ];
        const logoPlaceholders = [
            "https://placehold.co/120x120/8b5cf6/ffffff?text=Team+A",
            "https://placehold.co/120x120/10b981/ffffff?text=Team+B",
            "https://placehold.co/120x120/ef4444/ffffff?text=Team+C",
            "https://placehold.co/120x120/3b82f6/ffffff?text=Team+D",
            "https://placehold.co/120x120/f97316/ffffff?text=Team+E",
            "https://placehold.co/120x120/6b7280/ffffff?text=Team+F",
        ];

        for (let i = 1; i <= count; i++) {
            teams.push({
                id: i,
                name:
                    teamNames[i % teamNames.length] +
                    (i > teamNames.length
                        ? ` ${Math.floor(i / teamNames.length)}`
                        : ""), // Add suffix for more teams
                logoUrl: logoPlaceholders[i % logoPlaceholders.length],
                coach: coachNames[i % coachNames.length],
                playersCount: 12 + Math.floor(Math.random() * 3), // 12-14 players
                wins: Math.floor(Math.random() * 15),
                losses: Math.floor(Math.random() * 10),
                establishedYear: 2000 + Math.floor(Math.random() * 20), // 2000-2019
            });
        }
        return teams;
    };

    let allTeams = generateTeams(25); // Generate 25 mock teams
    let searchTerm = "";

    // --- Reactive Filtering ---
    $: filteredTeams = allTeams.filter((team) => {
        const lowerCaseSearchTerm = searchTerm.toLowerCase();
        return (
            team.name.toLowerCase().includes(lowerCaseSearchTerm) ||
            team.coach.toLowerCase().includes(lowerCaseSearchTerm)
        );
    });

    // --- Computed Total Teams ---
    $: totalTeams = allTeams.length;
</script>

<section class="min-h-screen py-16 px-4 sm:px-6 lg:px-8">
    <div class="max-w-7xl mx-auto">
        <header class="text-center mb-12">
            <h1
                class="text-5xl font-extrabold text-gray-900 mb-4 tracking-tight flex items-center justify-center gap-3"
            >
                <!-- Custom Basketball SVG Icon -->
                <svg
                    width="48"
                    height="48"
                    viewBox="0 0 24 24"
                    fill="none"
                    stroke="currentColor"
                    stroke-width="1.5"
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    class="text-indigo-600 animate-bounce-slow"
                >
                    <circle cx="12" cy="12" r="10" />
                    <path d="M12 2a10 10 0 0 0 0 20" />
                    <path d="M2 12h20" />
                    <path d="M12 2a10 10 0 0 1 8 4" />
                    <path d="M4 6a10 10 0 0 1 8 4" />
                    <path d="M12 22a10 10 0 0 1 8-4" />
                    <path d="M4 18a10 10 0 0 1 8-4" />
                </svg>
                Daftar Tim Basket
            </h1>
            <p class="text-lg text-gray-700 max-w-2xl mx-auto mb-8">
                Temukan informasi lengkap tentang tim-tim basket yang berlaga di
                liga kami.
            </p>

            <!-- Summary Card -->
            <div
                class="inline-flex items-center bg-white p-4 rounded-2xl shadow-lg"
            >
                <Users class="w-7 h-7 text-indigo-500 mr-3" />
                <div>
                    <p class="text-sm text-gray-500 font-medium">Total Tim</p>
                    <p class="text-2xl font-bold text-indigo-700">
                        {totalTeams}
                    </p>
                </div>
            </div>
        </header>

        <!-- Search Bar -->
        <div
            class="mb-10 max-w-lg mx-auto relative shadow-md rounded-full overflow-hidden"
        >
            <input
                type="text"
                placeholder="Cari nama tim atau pelatih..."
                class="w-full py-3 pl-12 pr-4 text-lg border-2 border-indigo-200 rounded-full focus:outline-none focus:border-indigo-500 transition-all duration-200"
                bind:value={searchTerm}
            />
            <Search
                class="absolute left-4 top-1/2 -translate-y-1/2 text-gray-400 w-6 h-6"
            />
        </div>

        <!-- Team List Grid -->
        {#if filteredTeams.length > 0}
            <div
                class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-8"
            >
                {#each filteredTeams as team (team.id)}
                    <!-- Changed <div> to <a> tag for proper clickability -->
                    <!-- Placeholder URL -->
                    <a
                        href={`/teams/${team.id}`}
                        class="group bg-white rounded-2xl shadow-xl
                        hover:shadow-2xl transition-all duration-300 ease-in-out
                        transform hover:-translate-y-2 overflow-hidden block
                        relative"
                        aria-label={`Profil tim ${team.name}`}
                    >
                        <!-- Team Logo -->
                        <div
                            class="relative pt-6 pb-2 px-4 flex justify-center"
                        >
                            <img
                                src={team.logoUrl}
                                alt={`Logo ${team.name}`}
                                class="w-28 h-28 rounded-full object-cover border-4 border-indigo-300 group-hover:border-indigo-500 transition-colors duration-300 shadow-md"
                                loading="lazy"
                                on:error={(e) => {
                                    const img =
                                        e.currentTarget as HTMLImageElement;
                                    img.onerror = null;
                                    img.src =
                                        "https://placehold.co/120x120/6b7280/ffffff?text=Logo";
                                }}
                            />
                        </div>

                        <!-- Team Info -->
                        <div class="p-4 text-center">
                            <h2
                                class="mt-2 text-2xl font-bold text-gray-900 group-hover:text-indigo-700 transition-colors duration-200 truncate"
                                title={team.name}
                            >
                                {team.name}
                            </h2>
                            <p
                                class="text-sm text-gray-600 font-medium mt-1 flex items-center justify-center gap-1"
                            >
                                <UserRound class="w-4 h-4 text-gray-500" />
                                {team.coach}
                            </p>

                            <div
                                class="grid grid-cols-2 gap-x-4 gap-y-2 mt-4 text-sm text-gray-700"
                            >
                                <div
                                    class="flex items-center justify-center gap-1"
                                >
                                    <Users class="w-4 h-4 text-blue-500" />
                                    {team.playersCount} Pemain
                                </div>
                                <div
                                    class="flex items-center justify-center gap-1"
                                >
                                    <Trophy class="w-4 h-4 text-yellow-500" />
                                    {team.wins} Menang - {team.losses} Kalah
                                </div>
                                <div
                                    class="col-span-2 flex items-center justify-center gap-1 text-gray-500"
                                >
                                    <Calendar class="w-4 h-4" /> Didirikan: {team.establishedYear}
                                </div>
                            </div>
                        </div>

                        <!-- Overlay/Hover Effect for More Info -->
                        <div
                            class="absolute inset-0 bg-indigo-700 bg-opacity-90 flex items-center justify-center opacity-0 group-hover:opacity-100 transition-opacity duration-300 rounded-2xl"
                        >
                            <span class="text-white text-lg font-semibold"
                                >Lihat Detail</span
                            >
                        </div>
                    </a>
                    <!-- Closed the <a> tag -->
                {/each}
            </div>
        {:else}
            <!-- No Results State -->
            <div class="text-center py-16 bg-white rounded-2xl shadow-lg">
                <Search class="w-24 h-24 text-gray-400 mx-auto mb-6" />
                <p class="text-2xl font-semibold text-gray-600 mb-2">
                    Tidak ada tim ditemukan
                </p>
                <p class="text-lg text-gray-500">
                    Coba cari dengan kata kunci lain.
                </p>
            </div>
        {/if}
    </div>
</section>

<style>
    /* Subtle bounce animation for the basketball emoji */
    @keyframes bounce-slow {
        0%,
        100% {
            transform: translateY(0);
        }
        50% {
            transform: translateY(-8px);
        }
    }

    .animate-bounce-slow {
        animation: bounce-slow 2s infinite ease-in-out;
    }
</style>
