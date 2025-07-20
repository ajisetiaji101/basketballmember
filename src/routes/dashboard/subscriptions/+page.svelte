<script lang="ts">
    import {
        Mail,
        MessageCircle,
        User,
        CalendarDays,
        Search,
        Users,
    } from "lucide-svelte"; // Icons for various details

    // --- Mock Data ---
    // In a real application, this data would come from your backend API
    const generateMembers = (count: number) => {
        const members = [];
        const today = new Date();
        for (let i = 1; i <= count; i++) {
            // Randomly assign to email or whatsapp or both
            let isEmail = Math.random() > 0.3;
            let isWhatsapp = Math.random() > 0.3;

            // Ensure at least one subscription
            if (!isEmail && !isWhatsapp) {
                if (Math.random() > 0.5) {
                    isEmail = true;
                } else {
                    isWhatsapp = true;
                }
            }

            // Generate a random past date for joined date
            const daysAgo = Math.floor(Math.random() * 365); // Up to 1 year ago
            const joinedDate = new Date(today);
            joinedDate.setDate(today.getDate() - daysAgo);

            members.push({
                id: i,
                name: `Anggota ${i} ${String.fromCharCode(65 + Math.floor(Math.random() * 26))}${String.fromCharCode(65 + Math.floor(Math.random() * 26))}`, // Example name like "Anggota 1 AB"
                email: isEmail ? `anggota${i}@example.com` : null,
                whatsapp: isWhatsapp
                    ? `+62 812-1111-${String(1000 + i).slice(-4)}`
                    : null,
                joinedDate: joinedDate.toISOString().split("T")[0], // YYYY-MM-DD format
            });
        }
        return members;
    };

    let allMembers = generateMembers(50); // Generate 50 mock members
    let searchTerm = "";

    // --- Utility Functions ---
    function formatDate(dateStr: string) {
        const options: Intl.DateTimeFormatOptions = {
            day: "2-digit",
            month: "short",
            year: "numeric",
        };
        return new Date(dateStr).toLocaleDateString("id-ID", options);
    }

    // --- Reactive Filtering ---
    $: filteredMembers = allMembers.filter((member) => {
        const lowerCaseSearchTerm = searchTerm.toLowerCase();
        return (
            member.name.toLowerCase().includes(lowerCaseSearchTerm) ||
            (member.email &&
                member.email.toLowerCase().includes(lowerCaseSearchTerm)) ||
            (member.whatsapp &&
                member.whatsapp.toLowerCase().includes(lowerCaseSearchTerm))
        );
    });

    // --- Computed Counts ---
    $: totalEmailSubscribers = allMembers.filter((m) => m.email).length;
    $: totalWhatsappSubscribers = allMembers.filter((m) => m.whatsapp).length;
</script>

<section class="min-h-screen bg-gray-50 py-16 px-4 sm:px-6 lg:px-8">
    <div class="max-w-7xl mx-auto">
        <header class="text-center mb-12">
            <h1
                class="text-5xl font-extrabold text-gray-900 mb-4 tracking-tight flex items-center justify-center gap-3"
            >
                <Users class="w-10 h-10 text-purple-600" /> Anggota Berlangganan
            </h1>
            <p class="text-lg text-gray-700 max-w-2xl mx-auto mb-8">
                Pantau daftar lengkap anggota yang telah terhubung dengan kami
                melalui email dan WhatsApp.
            </p>

            <!-- Subscription Summary Cards -->
            <div class="flex flex-wrap justify-center gap-6 mb-12">
                <div
                    class="bg-white p-6 rounded-2xl shadow-md flex items-center space-x-4 border-l-4 border-indigo-500"
                >
                    <Mail class="w-8 h-8 text-indigo-500" />
                    <div>
                        <p class="text-sm text-gray-500 font-medium">
                            Berlangganan Email
                        </p>
                        <p class="text-2xl font-bold text-indigo-700">
                            {totalEmailSubscribers}
                        </p>
                    </div>
                </div>
                <div
                    class="bg-white p-6 rounded-2xl shadow-md flex items-center space-x-4 border-l-4 border-green-500"
                >
                    <MessageCircle class="w-8 h-8 text-green-500" />
                    <div>
                        <p class="text-sm text-gray-500 font-medium">
                            Berlangganan WhatsApp
                        </p>
                        <p class="text-2xl font-bold text-green-700">
                            {totalWhatsappSubscribers}
                        </p>
                    </div>
                </div>
            </div>
        </header>

        <!-- Search Bar -->
        <div
            class="mb-10 max-w-lg mx-auto relative shadow-md rounded-full overflow-hidden"
        >
            <input
                type="text"
                placeholder="Cari nama, email, atau nomor WhatsApp..."
                class="w-full py-3 pl-12 pr-4 text-lg border-2 border-gray-200 rounded-full focus:outline-none focus:border-purple-500 transition-all duration-200"
                bind:value={searchTerm}
            />
            <Search
                class="absolute left-4 top-1/2 -translate-y-1/2 text-gray-400 w-6 h-6"
            />
        </div>

        <!-- Member List Table/Grid -->
        {#if filteredMembers.length > 0}
            <div class="bg-white rounded-2xl shadow-lg overflow-hidden">
                <div class="p-6 border-b border-gray-100">
                    <h2
                        class="text-2xl font-bold text-gray-800 flex items-center gap-2"
                    >
                        <Users class="w-6 h-6 text-purple-500" /> Anggota Ditemukan
                        ({filteredMembers.length})
                    </h2>
                </div>

                <div class="divide-y divide-gray-100">
                    {#each filteredMembers as member (member.id)}
                        <div
                            class="p-6 flex flex-col sm:flex-row items-center sm:justify-between gap-4 group hover:bg-gray-50 transition-colors duration-200"
                        >
                            <!-- Left: Member Name & Joined Date -->
                            <div
                                class="flex items-center gap-4 flex-grow text-center sm:text-left"
                            >
                                <div
                                    class="bg-purple-100 p-3 rounded-full flex-shrink-0"
                                >
                                    <User class="w-5 h-5 text-purple-600" />
                                </div>
                                <div class="flex flex-col">
                                    <h3
                                        class="text-xl font-semibold text-gray-900 truncate max-w-[200px] sm:max-w-none"
                                        title={member.name}
                                    >
                                        {member.name}
                                    </h3>
                                    <p
                                        class="text-sm text-gray-500 flex items-center gap-1 mt-1 justify-center sm:justify-start"
                                    >
                                        <CalendarDays class="w-4 h-4" /> Bergabung:
                                        {formatDate(member.joinedDate)}
                                    </p>
                                </div>
                            </div>

                            <!-- Right: Subscription Channels & Actions -->
                            <div
                                class="flex flex-wrap justify-center sm:justify-end gap-3 min-w-[200px]"
                            >
                                {#if member.email}
                                    <a
                                        href="mailto:{member.email}"
                                        class="inline-flex items-center bg-indigo-100 text-indigo-700 px-3 py-1.5 rounded-full text-sm font-medium hover:bg-indigo-200 transition-colors duration-200"
                                        title="Kirim Email"
                                    >
                                        <Mail class="w-4 h-4 mr-2" /> Email
                                    </a>
                                {/if}
                                {#if member.whatsapp}
                                    <a
                                        href="https://wa.me/{member.whatsapp
                                            .replace(/ /g, '')
                                            .replace(/\+/g, '')}"
                                        target="_blank"
                                        rel="noopener noreferrer"
                                        class="inline-flex items-center bg-green-100 text-green-700 px-3 py-1.5 rounded-full text-sm font-medium hover:bg-green-200 transition-colors duration-200"
                                        title="Kirim Pesan WhatsApp"
                                    >
                                        <MessageCircle class="w-4 h-4 mr-2" /> WhatsApp
                                    </a>
                                {/if}
                            </div>
                        </div>
                    {/each}
                </div>
            </div>
        {:else}
            <!-- No Results State -->
            <div class="text-center py-16 bg-white rounded-2xl shadow-lg">
                <Search class="w-24 h-24 text-gray-400 mx-auto mb-6" />
                <p class="text-2xl font-semibold text-gray-600 mb-2">
                    Tidak ada anggota ditemukan
                </p>
                <p class="text-lg text-gray-500">
                    Coba cari dengan kata kunci lain atau belum ada yang
                    bergabung.
                </p>
            </div>
        {/if}
    </div>
</section>
