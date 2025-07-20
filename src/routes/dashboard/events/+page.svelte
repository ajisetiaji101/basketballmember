<script lang="ts">
    import eventImage from "$lib/images/basket.webp"; // Ensure this path is correct
    import { CalendarDays, MapPin, Tag } from "lucide-svelte"; // Added relevant icons

    const events = [
        {
            id: 1,
            title: "Basketball Championship 2025",
            date: "2025-08-15",
            description:
                "Join us for the annual regional basketball championship at the city stadium. Witness top teams compete for glory!",
            location: "City Sports Arena",
            category: "Championship",
        },
        {
            id: 2,
            title: "Youth Basketball Workshop",
            date: "2025-09-01",
            description:
                "A comprehensive workshop designed to develop fundamental basketball skills for youths aged 12-18.",
            location: "Community Sports Hall",
            category: "Workshop",
        },
        {
            id: 3,
            title: "Charity Basketball Game",
            date: "2025-10-05",
            description:
                "A star-studded charity game featuring local celebrities to raise funds for youth sports programs. Don't miss out!",
            location: "Grand Exhibition Center",
            category: "Charity",
        },
        {
            id: 4,
            title: "Summer Basketball Camp",
            date: "2025-07-10", // This event is in the past relative to current date 2025-07-20
            description:
                "An intensive training camp for aspiring players to improve skills, fitness, and game strategy.",
            location: "Green Valley Sports Complex",
            category: "Camp",
        },
        {
            id: 5,
            title: "3-on-3 Street Basketball Tournament",
            date: "2025-11-20",
            description:
                "Fast-paced street basketball tournament open for all ages and skill levels. Form your team and compete!",
            location: "Downtown Plaza Courts",
            category: "Tournament",
        },
        {
            id: 6,
            title: "Coaching Clinic for Aspiring Coaches",
            date: "2025-08-25",
            description:
                "A specialized clinic for coaches focusing on modern basketball techniques, strategy, and player development.",
            location: "Sports University Auditorium",
            category: "Clinic",
        },
    ];

    function formatDate(dateStr: string) {
        // Use a more detailed format
        const options: Intl.DateTimeFormatOptions = {
            weekday: "long", // e.g., "Monday"
            year: "numeric",
            month: "long", // e.g., "August"
            day: "numeric", // e.g., "15"
        };
        return new Date(dateStr).toLocaleDateString("en-US", options); // Using en-US for more common format, adjust to "id-ID" if preferred
    }

    // Function to check if an event date is in the past
    function isEventPast(eventDate: string) {
        const today = new Date();
        today.setHours(0, 0, 0, 0); // Normalize to start of day
        const eventDay = new Date(eventDate);
        eventDay.setHours(0, 0, 0, 0); // Normalize to start of day
        return eventDay < today;
    }
</script>

<section class="min-h-screen py-16 px-4 sm:px-6 lg:px-8">
    <div class="max-w-7xl mx-auto">
        <header class="text-center mb-16">
            <h1
                class="text-5xl font-extrabold text-gray-900 mb-4 tracking-tight flex items-center justify-center gap-4"
            >
                <span class="inline-block animate-bounce-slow">🏀</span> Acara Mendatang
            </h1>
            <p class="text-lg text-gray-700 max-w-2xl mx-auto">
                Jangan lewatkan acara-acara menarik kami! Catat tanggalnya dan
                bergabunglah dengan keseruannya.
            </p>
            <div
                class="mt-8 inline-flex items-center bg-white p-4 rounded-2xl shadow-lg"
            >
                <CalendarDays class="w-7 h-7 text-indigo-500 mr-3" />
                <div>
                    <p class="text-sm text-gray-500 font-medium">
                        Jumlah Acara
                    </p>
                    <p class="text-2xl font-bold text-indigo-700">
                        {events.length}
                    </p>
                </div>
            </div>
        </header>

        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-10">
            {#each events as event (event.id)}
                <article
                    class="group bg-white rounded-3xl overflow-hidden shadow-xl hover:shadow-2xl transition-all duration-300 transform hover:-translate-y-2 hover:scale-[1.03] flex flex-col relative
                    {isEventPast(event.date) ? 'opacity-70 grayscale' : ''} "
                    aria-label={`Event card for ${event.title}`}
                >
                    {#if isEventPast(event.date)}
                        <div
                            class="absolute inset-0 bg-black bg-opacity-60 flex items-center justify-center z-10 rounded-3xl"
                        >
                            <span
                                class="text-white text-2xl font-bold uppercase tracking-wide px-4 py-2 bg-red-600 rounded-lg shadow-xl"
                            >
                                Selesai
                            </span>
                        </div>
                    {/if}

                    <div class="relative overflow-hidden aspect-[16/9]">
                        <img
                            src={eventImage}
                            alt={event.title}
                            class="w-full h-full object-cover transition-transform duration-500 ease-in-out group-hover:scale-110"
                            loading="lazy"
                        />
                        <div
                            class="absolute top-4 left-4 bg-indigo-600 text-white text-sm font-bold px-4 py-2 rounded-lg shadow-md flex items-center gap-2"
                        >
                            <CalendarDays class="w-4 h-4" />
                            {formatDate(event.date)}
                        </div>
                    </div>

                    <div class="p-6 flex flex-col flex-grow space-y-4">
                        <h2
                            class="text-2xl font-extrabold text-gray-900 leading-tight group-hover:text-indigo-700 transition-colors duration-200"
                        >
                            {event.title}
                        </h2>
                        <p
                            class="text-gray-700 text-base flex-grow line-clamp-3"
                        >
                            {event.description}
                        </p>

                        <div class="flex flex-wrap gap-3 mt-2">
                            <span
                                class="inline-flex items-center bg-gray-100 text-gray-700 text-xs font-medium px-3 py-1.5 rounded-full"
                            >
                                <MapPin class="w-3 h-3 mr-1" />
                                {event.location}
                            </span>
                            <span
                                class="inline-flex items-center bg-blue-100 text-blue-700 text-xs font-medium px-3 py-1.5 rounded-full"
                            >
                                <Tag class="w-3 h-3 mr-1" />
                                {event.category}
                            </span>
                        </div>

                        <button
                            class="mt-auto w-full flex justify-center items-center gap-2 bg-indigo-600 hover:bg-indigo-700 text-white font-semibold py-3 px-6 rounded-xl transition duration-300 shadow-md hover:shadow-lg focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2"
                        >
                            Detail Acara →
                        </button>
                    </div>
                </article>
            {/each}
        </div>
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

    /* For line-clamp, in case Tailwind's built-in doesn't fully work in all environments */
    .line-clamp-3 {
        display: -webkit-box;
        -webkit-line-clamp: 3;
        -webkit-box-orient: vertical;
        overflow: hidden;
    }
</style>
