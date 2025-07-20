<script lang="ts">
    import dharma from "$lib/images/dharma.jpeg"; // Assuming this path is correct for your images
    import { Users, User, Search } from "lucide-svelte"; // Added relevant icons

    // Create a diverse set of avatars for more visual interest
    const avatarUrls = [
        "https://i.pravatar.cc/150?img=1",
        "https://i.pravatar.cc/150?img=2",
        "https://i.pravatar.cc/150?img=3",
        "https://i.pravatar.cc/150?img=4",
        "https://i.pravatar.cc/150?img=5",
        "https://i.pravatar.cc/150?img=6",
        "https://i.pravatar.cc/150?img=7",
        "https://i.pravatar.cc/150?img=8",
        "https://i.pravatar.cc/150?img=9",
        "https://i.pravatar.cc/150?img=10",
        "https://i.pravatar.cc/150?img=11",
        "https://i.pravatar.cc/150?img=12",
        "https://i.pravatar.cc/150?img=13",
        "https://i.pravatar.cc/150?img=14",
        "https://i.pravatar.cc/150?img=15",
        "https://i.pravatar.cc/150?img=16",
        "https://i.pravatar.cc/150?img=17",
        "https://i.pravatar.cc/150?img=18",
        "https://i.pravatar.cc/150?img=19",
        "https://i.pravatar.cc/150?img=20",
    ];

    const generateMembers = (count: number) => {
        return Array.from({ length: count }, (_, i) => ({
            id: i + 1,
            name: `Anggota ${i + 1}`,
            image: avatarUrls[i % avatarUrls.length], // Cycle through diverse avatars
            role:
                i % 3 === 0 ? "Admin" : i % 2 === 0 ? "Kontributor" : "Anggota",
            status: i % 4 === 0 ? "Online" : "Offline",
        }));
    };

    let allMembers = generateMembers(40);
    let searchTerm = "";

    // Filtered members based on search term
    $: filteredMembers = allMembers.filter((member) =>
        member.name.toLowerCase().includes(searchTerm.toLowerCase()),
    );
</script>

<section class="min-h-screen py-16 px-4 sm:px-6 lg:px-8">
    <div class="max-w-7xl mx-auto">
        <header class="text-center mb-12">
            <h1
                class="text-5xl font-extrabold text-gray-900 mb-4 tracking-tight flex items-center justify-center gap-3"
            >
                <Users class="w-10 h-10 text-indigo-600" /> Daftar Anggota
            </h1>
            <p class="text-lg text-gray-700 max-w-2xl mx-auto mb-6">
                Temukan semua anggota komunitas kami di sini.
            </p>
            <div
                class="inline-flex items-center bg-white p-4 rounded-2xl shadow-lg"
            >
                <Users class="w-7 h-7 text-indigo-500 mr-3" />
                <div>
                    <p class="text-sm text-gray-500 font-medium">
                        Total Anggota
                    </p>
                    <p class="text-2xl font-bold text-indigo-700">
                        {allMembers.length}
                    </p>
                </div>
            </div>
        </header>

        <div
            class="mb-10 max-w-lg mx-auto relative shadow-md rounded-full overflow-hidden"
        >
            <input
                type="text"
                placeholder="Cari anggota..."
                class="w-full py-3 pl-12 pr-4 text-lg border-2 border-indigo-200 rounded-full focus:outline-none focus:border-indigo-500 transition-all duration-200"
                bind:value={searchTerm}
            />
            <Search
                class="absolute left-4 top-1/2 -translate-y-1/2 text-gray-400 w-6 h-6"
            />
        </div>

        {#if filteredMembers.length > 0}
            <div
                class="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-4 lg:grid-cols-5 xl:grid-cols-6 gap-6 sm:gap-8"
            >
                {#each filteredMembers as member (member.id)}
                    <div
                        class="group relative bg-white rounded-2xl shadow-lg hover:shadow-xl transition-all duration-300 ease-in-out cursor-pointer transform hover:-translate-y-1 overflow-hidden"
                        tabindex="0"
                        aria-label={`Profil ${member.name}`}
                    >
                        <div
                            class="relative pt-6 pb-2 px-4 flex justify-center"
                        >
                            <img
                                src={member.image}
                                alt={member.name}
                                class="w-28 h-28 rounded-full object-cover border-4 border-indigo-300 group-hover:border-indigo-500 transition-colors duration-300 shadow-md"
                                loading="lazy"
                            />
                            <span
                                class="absolute top-8 right-6 block w-4 h-4 rounded-full
                                {member.status === 'Online'
                                    ? 'bg-green-500'
                                    : 'bg-gray-400'} ring-2 ring-white"
                            ></span>
                        </div>

                        <div class="p-4 text-center">
                            <h2
                                class="mt-2 text-xl font-bold text-gray-900 group-hover:text-indigo-700 transition-colors duration-200 truncate"
                                title={member.name}
                            >
                                {member.name}
                            </h2>
                            <p
                                class="text-sm text-indigo-500 font-semibold mt-1"
                            >
                                {member.role}
                            </p>
                        </div>

                        <div
                            class="absolute inset-0 bg-indigo-700 bg-opacity-90 flex items-center justify-center opacity-0 group-hover:opacity-100 transition-opacity duration-300 rounded-2xl"
                        >
                            <span class="text-white text-lg font-semibold"
                                >Lihat Profil</span
                            >
                        </div>
                    </div>
                {/each}
            </div>
        {:else}
            <div class="text-center py-16">
                <User class="w-24 h-24 text-gray-400 mx-auto mb-6" />
                <p class="text-2xl font-semibold text-gray-600 mb-2">
                    Tidak ada anggota ditemukan
                </p>
                <p class="text-lg text-gray-500">
                    Coba cari dengan kata kunci lain.
                </p>
            </div>
        {/if}
    </div>
</section>
