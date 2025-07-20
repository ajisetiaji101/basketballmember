<script lang="ts">
    import { fade, slide } from "svelte/transition";
    import { cubicOut } from "svelte/easing";

    type ClassOption = {
        id: number;
        name: string;
        discount: number;
        price: number;
        originalPrice: number;
        image: string;
        description: string;
        features: string[]; // Added features for each class
    };

    let classes: ClassOption[] = [
        {
            id: 1,
            name: "Advanced Drills Squad",
            discount: 10,
            price: 150000,
            originalPrice: 165000,
            image: "https://images.unsplash.com/photo-1579952528373-d25089e02c61?auto=format&fit=crop&q=80&w=1974&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D",
            description:
                "Master complex techniques and elevate your game with intensive, high-level training.",
            features: [
                "Intensive advanced drills",
                "Personalized feedback",
                "Scrimmages with elite players",
                "Advanced strategy sessions",
            ],
        },
        {
            id: 2,
            name: "Fundamental Skills Pro",
            discount: 15,
            price: 120000,
            originalPrice: 141000,
            image: "https://images.unsplash.com/photo-1546519638-68e109498ffc?auto=format&fit=crop&q=80&w=1974&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D",
            description:
                "Build a strong foundation. Perfect for beginners or those refining core basketball abilities.",
            features: [
                "Dribbling & shooting basics",
                "Footwork & passing fundamentals",
                "Defensive stance & positioning",
                "Beginner-friendly environment",
            ],
        },
        {
            id: 3,
            name: "Team Strategy Masters",
            discount: 5,
            price: 175000,
            originalPrice: 184000,
            image: "https://images.unsplash.com/photo-1518604724657-9d7831d102e5?auto=format&fit=crop&q=80&w=1974&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D",
            description:
                "Learn advanced team plays, defensive strategies, and effective communication on the court.",
            features: [
                "Offensive & defensive schemes",
                "In-game decision making",
                "Team communication drills",
                "Leadership development",
            ],
        },
    ];

    let selectedClassId: number | null = null;
    let parallaxOffset = 0;

    function handleSelect(id: number) {
        selectedClassId = id;
    }

    // Parallax effect for hero section
    function handleScroll() {
        parallaxOffset = window.scrollY * 0.3; // Adjust multiplier for desired effect
    }
</script>

<svelte:head>
    <title>Classes | Hardwood Heroes Academy</title>
    <link
        rel="stylesheet"
        href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css"
        integrity="sha512-Fo3rlalHrx31u/SCiK8EmLhUq0eW8T9e3+8P+p1z+r9zV6Gf0c5/b6k3w4h1v+x+K4QJ2/v6p5e0/Q2+g=="
        crossorigin="anonymous"
        referrerpolicy="no-referrer"
    />
    <link
        href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700;800;900&display=swap"
        rel="stylesheet"
    />
</svelte:head>

<div class="font-poppins antialiased text-gray-800 bg-gray-100">
    <section
        class="relative h-screen bg-cover bg-fixed flex items-center justify-center text-white overflow-hidden"
        style="background-image: url('https://www.journalgazette.net/storyimage/JG/20250718/SPORTS/250719875/AR/0/AR-250719875.jpg'); background-position-y: {-parallaxOffset}px;"
        on:scroll={handleScroll}
    >
        <div
            class="absolute inset-0 bg-gradient-to-br from-blue-950 to-black opacity-90"
        ></div>
        <div class="relative z-10 text-center p-4 max-w-5xl mx-auto">
            <h1
                class="text-6xl md:text-8xl font-extrabold leading-tight mb-7 tracking-tight animate-fade-in-down"
            >
                Dribble. Shoot. Score. <br /> Your Journey Starts Here!
            </h1>
            <p
                class="text-xl md:text-3xl mb-12 text-blue-100 animate-fade-in-up font-light"
            >
                Transform your game with **expert coaching**, **cutting-edge
                training facilities**, and a **winning community**. From
                fundamental drills to advanced strategies, we've got a class
                tailored for every ambition.
            </p>
            <a
                href="#class-selection"
                class="inline-flex items-center justify-center bg-yellow-500 hover:bg-yellow-600 text-blue-900 font-bold py-5 px-12 rounded-full
                       text-xl md:text-2xl transition duration-300 transform hover:scale-105 shadow-2xl ring-4 ring-yellow-300
                       animate-pulse-slow group"
            >
                <i
                    class="fas fa-arrow-down mr-4 text-3xl animate-bounce-icon group-hover:text-yellow-700"
                ></i>
                Find Your Perfect Class!
            </a>
        </div>
    </section>

    <section class="py-24 bg-blue-900 text-white">
        <div class="container mx-auto px-6 text-center">
            <h2 class="text-4xl md:text-5xl font-extrabold mb-16">
                Why Hardwood Heroes Academy?
            </h2>
            <div class="grid grid-cols-1 md:grid-cols-3 gap-12">
                <div
                    class="p-8 bg-blue-800 rounded-xl shadow-2xl transform hover:scale-105 transition duration-300 ease-out border-b-4 border-yellow-500"
                >
                    <i
                        class="fas fa-user-tie text-6xl mx-auto mb-6 text-yellow-400 drop-shadow-lg"
                    ></i>
                    <h3 class="text-3xl font-bold mb-4">Expert Coaches</h3>
                    <p class="text-blue-200 text-lg leading-relaxed">
                        Learn from seasoned professionals, ex-pros, and
                        certified trainers dedicated to unlocking your full
                        potential.
                    </p>
                </div>
                <div
                    class="p-8 bg-blue-800 rounded-xl shadow-2xl transform hover:scale-105 transition duration-300 ease-out border-b-4 border-yellow-500"
                >
                    <i
                        class="fas fa-chart-line text-6xl mx-auto mb-6 text-yellow-400 drop-shadow-lg"
                    ></i>
                    <h3 class="text-3xl font-bold mb-4">Dynamic Programs</h3>
                    <p class="text-blue-200 text-lg leading-relaxed">
                        Our meticulously crafted programs cater to all levels,
                        ensuring progressive growth from basics to elite
                        tactics.
                    </p>
                </div>
                <div
                    class="p-8 bg-blue-800 rounded-xl shadow-2xl transform hover:scale-105 transition duration-300 ease-out border-b-4 border-yellow-500"
                >
                    <i
                        class="fas fa-users text-6xl mx-auto mb-6 text-yellow-400 drop-shadow-lg"
                    ></i>
                    <h3 class="text-3xl font-bold mb-4">Winning Community</h3>
                    <p class="text-blue-200 text-lg leading-relaxed">
                        Join a supportive and competitive community where you'll
                        build lasting friendships and grow together.
                    </p>
                </div>
            </div>
        </div>
    </section>

    <section
        id="class-selection"
        class="py-24 bg-gradient-to-br from-gray-50 to-gray-100"
    >
        <div class="container mx-auto px-6">
            <h2
                class="text-4xl md:text-6xl font-extrabold text-center text-gray-900 mb-16 leading-tight"
            >
                Pick Your Squad: <br class="sm:hidden" /> Ignite Your Passion!
            </h2>
            <p
                class="text-xl text-center text-gray-700 mb-14 max-w-4xl mx-auto font-normal"
            >
                Ready to take the court by storm? Choose the class that best
                fits your goals and skill level. Each squad is meticulously
                designed to push your limits and maximize your potential.
            </p>

            <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-12">
                {#each classes as classItem}
                    <div
                        class={`relative border-2 rounded-3xl overflow-hidden cursor-pointer
                               transition-all duration-400 ease-in-out transform
                               ${
                                   selectedClassId === classItem.id
                                       ? "ring-blue-600 ring-offset-4 ring-offset-gray-100 shadow-3xl scale-105 bg-white border-blue-600"
                                       : "hover:shadow-xl hover:-translate-y-2 hover:border-blue-400 bg-white border-gray-200"
                               }
                               flex flex-col group`}
                        on:click={() => handleSelect(classItem.id)}
                    >
                        <div
                            class="absolute top-4 left-4 bg-gradient-to-r from-red-600 to-red-400
                                   text-white text-base font-bold px-4 py-2 rounded-full shadow-lg
                                   transform -rotate-6 z-10 animate-fade-in border border-red-300"
                        >
                            <i class="fas fa-bolt mr-2"></i> Save {classItem.discount}%!
                        </div>

                        <div class="flex-shrink-0 relative overflow-hidden">
                            <img
                                src={classItem.image}
                                alt={classItem.name}
                                class="w-full h-60 object-cover rounded-t-3xl
                                       transition-transform duration-500 ease-in-out group-hover:scale-110"
                            />
                            <div
                                class="absolute inset-0 bg-gradient-to-t from-black/60 via-transparent to-transparent"
                            ></div>
                        </div>

                        <div
                            class="p-8 flex-grow flex flex-col justify-between"
                        >
                            <div>
                                <h3
                                    class="text-3xl font-extrabold text-gray-900 mb-3 leading-tight"
                                >
                                    {classItem.name}
                                </h3>
                                <p
                                    class="text-gray-700 text-lg mb-6 leading-relaxed"
                                >
                                    {classItem.description}
                                </p>
                                <ul
                                    class="text-gray-800 space-y-2 mb-6 text-base"
                                >
                                    {#each classItem.features as feature}
                                        <li class="flex items-center">
                                            <i
                                                class="fas fa-check-circle text-green-500 mr-3 text-lg"
                                            ></i>
                                            <span>{feature}</span>
                                        </li>
                                    {/each}
                                </ul>
                            </div>

                            <div>
                                <div class="flex items-baseline mb-4 mt-6">
                                    <span
                                        class="text-5xl font-extrabold text-blue-700 tracking-tight"
                                    >
                                        Rp{classItem.price.toLocaleString(
                                            "id-ID",
                                        )}
                                    </span>
                                    {#if classItem.discount > 0}
                                        <span
                                            class="text-lg text-gray-500 line-through ml-3 font-medium"
                                        >
                                            Rp{classItem.originalPrice.toLocaleString(
                                                "id-ID",
                                            )}
                                        </span>
                                    {/if}
                                    <span
                                        class="text-xl text-gray-600 ml-2 font-medium"
                                        >/month</span
                                    >
                                </div>

                                {#if selectedClassId === classItem.id}
                                    <div
                                        class="mt-6 text-xl text-green-700 font-semibold flex items-center justify-center py-3 px-6 bg-green-100 rounded-xl shadow-inner animate-fade-in-up-small"
                                    >
                                        <i
                                            class="fas fa-check-circle text-green-600 mr-3 text-2xl"
                                        ></i>
                                        <span>Class Selected!</span>
                                    </div>
                                {:else}
                                    <button
                                        class="mt-6 w-full bg-blue-600 text-white py-4 px-8 rounded-xl
                                               hover:bg-blue-700 transition-colors duration-300
                                               font-bold text-xl shadow-lg hover:shadow-xl transform hover:-translate-y-0.5"
                                        on:click|stopPropagation={() =>
                                            handleSelect(classItem.id)}
                                    >
                                        Join This Squad!
                                    </button>
                                {/if}
                            </div>
                        </div>
                    </div>
                {/each}
            </div>
        </div>
    </section>

    <section class="py-24 bg-blue-900 text-white">
        <div class="container mx-auto px-6">
            <h2 class="text-4xl md:text-5xl font-extrabold text-center mb-16">
                Hear It From Our MVP Members
            </h2>
            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-10">
                <div
                    class="bg-blue-800 p-8 rounded-2xl shadow-2xl flex flex-col items-center text-center
                           border-b-4 border-yellow-500 transform hover:scale-105 transition duration-300 ease-out"
                >
                    <img
                        src="https://randomuser.me/api/portraits/men/32.jpg"
                        alt="Rizky P. Testimonial"
                        class="w-28 h-28 rounded-full mb-7 ring-4 ring-yellow-400 object-cover shadow-lg"
                    />
                    <p
                        class="text-lg italic text-blue-100 mb-7 leading-relaxed"
                    >
                        "Before joining, I was stuck. Now, my **dribbling is
                        sharper**, and my **confidence is through the roof**!
                        This academy is a game-changer. The coaches are simply
                        incredible."
                    </p>
                    <p class="font-bold text-yellow-400 text-xl">
                        - Rizky P., Advanced Drills Squad
                    </p>
                </div>
                <div
                    class="bg-blue-800 p-8 rounded-2xl shadow-2xl flex flex-col items-center text-center
                           border-b-4 border-yellow-500 transform hover:scale-105 transition duration-300 ease-out"
                >
                    <img
                        src="https://randomuser.me/api/portraits/women/44.jpg"
                        alt="Ayu W. Testimonial"
                        class="w-28 h-28 rounded-full mb-7 ring-4 ring-yellow-400 object-cover shadow-lg"
                    />
                    <p
                        class="text-lg italic text-blue-100 mb-7 leading-relaxed"
                    >
                        "The coaches break down complex plays into
                        **easy-to-understand steps**. I feel like a true
                        strategist on the court now! My team skills have vastly
                        improved."
                    </p>
                    <p class="font-bold text-yellow-400 text-xl">
                        - Ayu W., Team Strategy Masters
                    </p>
                </div>
                <div
                    class="bg-blue-800 p-8 rounded-2xl shadow-2xl flex flex-col items-center text-center
                           border-b-4 border-yellow-500 transform hover:scale-105 transition duration-300 ease-out"
                >
                    <img
                        src="https://randomuser.me/api/portraits/men/78.jpg"
                        alt="Budi S. Testimonial"
                        class="w-28 h-28 rounded-full mb-7 ring-4 ring-yellow-400 object-cover shadow-lg"
                    />
                    <p
                        class="text-lg italic text-blue-100 mb-7 leading-relaxed"
                    >
                        "As a beginner, I was nervous, but the **Fundamental
                        Skills Pro** class made me confident. I'm hitting shots
                        I never thought I could! The support here is amazing."
                    </p>
                    <p class="font-bold text-yellow-400 text-xl">
                        - Budi S., Fundamental Skills Pro
                    </p>
                </div>
            </div>
        </div>
    </section>

    <section class="py-24 bg-blue-700 text-white text-center">
        <div class="container mx-auto px-6 max-w-4xl">
            <h2 class="text-4xl md:text-6xl font-extrabold mb-8 leading-tight">
                Ready to Dominate the Court?
            </h2>
            <p class="text-xl md:text-2xl mb-12 max-w-3xl mx-auto font-light">
                Don't just play basketball, **master it**! Spots are filling up
                fast for our next season. **Secure your place now** and start
                your journey to becoming an unforgettable player.
            </p>
            <a
                href="#class-selection"
                class="inline-flex items-center justify-center bg-yellow-400 text-blue-900 hover:bg-yellow-300 font-bold py-6 px-14 rounded-full
                       text-2xl md:text-3xl transition duration-300 transform hover:scale-105 shadow-2xl ring-4 ring-yellow-200"
            >
                <i class="fas fa-clipboard-list mr-4 text-3xl"></i> Enroll & Elevate
                Your Game!
            </a>
        </div>
    </section>

    <footer class="bg-gray-950 text-gray-400 py-12 text-center">
        <div class="container mx-auto px-6">
            <p class="mb-5 text-lg">
                &copy; {new Date().getFullYear()} Hardwood Heroes Academy. All rights
                reserved.
            </p>
            <div
                class="flex flex-col sm:flex-row justify-center space-y-3 sm:space-y-0 sm:space-x-10 text-base"
            >
                <a
                    href="#"
                    class="hover:text-white transition-colors duration-200"
                    >Privacy Policy</a
                >
                <a
                    href="#"
                    class="hover:text-white transition-colors duration-200"
                    >Terms of Service</a
                >
                <a
                    href="#"
                    class="hover:text-white transition-colors duration-200"
                    >Contact Us</a
                >
            </div>
        </div>
    </footer>
</div>

<style>
    /* Google Font Import */
    @import url("https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700;800;900&display=swap");

    .font-poppins {
        font-family: "Poppins", sans-serif;
    }

    /* Keyframe Animations */
    @keyframes fadeInDown {
        from {
            opacity: 0;
            transform: translateY(-40px);
        }
        to {
            opacity: 1;
            transform: translateY(0);
        }
    }

    @keyframes fadeInUp {
        from {
            opacity: 0;
            transform: translateY(40px);
        }
        to {
            opacity: 1;
            transform: translateY(0);
        }
    }

    @keyframes fadeInUpSmall {
        from {
            opacity: 0;
            transform: translateY(10px);
        }
        to {
            opacity: 1;
            transform: translateY(0);
        }
    }

    @keyframes pulseSlow {
        0%,
        100% {
            transform: scale(1);
        }
        50% {
            transform: scale(1.02); /* Reduced pulse for subtlety */
        }
    }

    @keyframes bounceIcon {
        0%,
        100% {
            transform: translateY(0);
        }
        50% {
            transform: translateY(-8px); /* Increased bounce */
        }
    }

    @keyframes fadeIn {
        from {
            opacity: 0;
        }
        to {
            opacity: 1;
        }
    }

    /* Animation Classes */
    .animate-fade-in-down {
        animation: fadeInDown 1.4s ease-out forwards;
    }
    .animate-fade-in-up {
        animation: fadeInUp 1.4s ease-out forwards 0.4s;
    }
    .animate-fade-in-up-small {
        animation: fadeInUpSmall 0.5s ease-out forwards;
    }
    .animate-pulse-slow {
        animation: pulseSlow 3s infinite ease-in-out;
    }
    .animate-bounce-icon {
        animation: bounceIcon 1.2s infinite ease-in-out;
    }
    .animate-fade-in {
        animation: fadeIn 1s ease-out forwards;
    }
</style>
