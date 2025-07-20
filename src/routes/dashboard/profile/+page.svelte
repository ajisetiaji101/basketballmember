<script lang="ts">
    import {
        UserRound,
        Mail,
        Phone,
        MapPin,
        Calendar,
        BadgeCheck,
        Edit, // Import the Edit icon
    } from "lucide-svelte";

    const profile = {
        name: "Aji Setiaji",
        email: "aji@example.com",
        phone: "+62 812-3456-7890",
        address: "Jl. Merdeka No. 10, Jakarta",
        birthday: "1990-05-12",
        role: "Member Aktif",
        avatarUrl: "https://i.pravatar.cc/150?img=8",
    };

    function formatDate(dateStr: string) {
        return new Date(dateStr).toLocaleDateString("id-ID", {
            day: "2-digit",
            month: "long",
            year: "numeric",
        });
    }

    // Function to handle edit button click (you'd replace this with actual logic)
    function handleEditProfile() {
        alert("Edit Profile button clicked!");
        // In a real application, you would navigate to an edit form
        // or open a modal here.
    }
</script>

<section
    class="min-h-screen py-16 px-4 sm:px-6 lg:px-8 flex items-center justify-center bg-white"
    role="region"
    aria-label="Profil pengguna"
>
    <div class="max-w-4xl w-full mx-auto relative">
        <button
            on:click={handleEditProfile}
            class="absolute top-0 right-0 p-3 bg-indigo-500 text-white rounded-full focus:outline-none focus:ring-2 focus:ring-indigo-400 focus:ring-opacity-75 transition-colors duration-200"
            aria-label="Edit Profile"
            title="Edit Profile"
        >
            <Edit class="w-5 h-5" />
        </button>

        <div
            class="flex flex-col sm:flex-row items-center sm:items-start gap-10"
        >
            <div class="flex-shrink-0 relative">
                <img
                    src={profile.avatarUrl}
                    alt={`Foto profil ${profile.name}`}
                    class="w-48 h-48 rounded-full border-4 border-indigo-400 object-cover transform transition-transform duration-300 hover:scale-105"
                    loading="lazy"
                />
                <span
                    class="absolute bottom-3 right-3 block w-6 h-6 rounded-full bg-green-500 ring-4 ring-white"
                ></span>
            </div>

            <div
                class="flex-1 space-y-7 text-gray-700 text-center sm:text-left"
            >
                <h1
                    class="text-4xl font-extrabold text-gray-800 mb-2 leading-tight"
                >
                    {profile.name}
                </h1>

                <div class="flex justify-center sm:justify-start mb-6">
                    <span
                        class="inline-flex items-center bg-indigo-600 text-white px-5 py-2 rounded-full text-md font-semibold tracking-wide"
                    >
                        <BadgeCheck class="w-5 h-5 mr-2" />
                        {profile.role}
                    </span>
                </div>

                <div class="grid grid-cols-1 md:grid-cols-2 gap-x-8 gap-y-5">
                    {#each [{ icon: Mail, label: "Email", value: profile.email }, { icon: Phone, label: "Telepon", value: profile.phone }, { icon: MapPin, label: "Alamat", value: profile.address }, { icon: Calendar, label: "Tanggal Lahir", value: formatDate(profile.birthday) }] as item}
                        <div class="flex items-center gap-4">
                            <svelte:component
                                this={item.icon}
                                class="text-indigo-500 w-6 h-6 flex-shrink-0"
                                aria-label={item.label}
                            />
                            <div class="flex flex-col items-start">
                                <span class="text-sm font-medium text-gray-500"
                                    >{item.label}</span
                                >
                                <span
                                    class="text-base font-semibold text-gray-800"
                                    >{item.value}</span
                                >
                            </div>
                        </div>
                    {/each}
                </div>
            </div>
        </div>
    </div>
</section>
