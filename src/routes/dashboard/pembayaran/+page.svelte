<script lang="ts">
    import {
        CheckCircle,
        Clock,
        XCircle,
        DollarSign,
        CalendarDays,
        User,
    } from "lucide-svelte"; // Added more icons for detail

    const payments = [
        {
            id: 1,
            name: "Aji Setiaji",
            amount: 150000,
            status: "Paid",
            date: "2025-07-15",
        },
        {
            id: 2,
            name: "Dharma Syahputra",
            amount: 200000,
            status: "Pending",
            date: "2025-07-16",
        },
        {
            id: 3,
            name: "Silvia Ratna",
            amount: 180000,
            status: "Paid",
            date: "2025-07-17",
        },
        {
            id: 4,
            name: "Reno Rafly",
            amount: 250000,
            status: "Failed",
            date: "2025-07-18",
        },
    ];

    function formatCurrency(amount: number) {
        return new Intl.NumberFormat("id-ID", {
            style: "currency",
            currency: "IDR",
            minimumFractionDigits: 0, // Remove decimals if not needed for IDR
        }).format(amount);
    }

    function formatDate(dateStr: string) {
        const options: Intl.DateTimeFormatOptions = {
            day: "2-digit",
            month: "long", // Changed to 'long' for fuller month name
            year: "numeric",
        };
        return new Date(dateStr).toLocaleDateString("id-ID", options);
    }

    // Computed property for total amount
    $: totalAmount = payments.reduce((sum, payment) => sum + payment.amount, 0);
</script>

<section class="min-h-screen py-16 px-4 sm:px-6 lg:px-8">
    <div class="max-w-4xl mx-auto">
        <header class="text-center mb-12">
            <h1
                class="text-5xl font-extrabold text-gray-900 mb-4 tracking-tight"
            >
                <span class="inline-block animate-wave">👋</span> Daftar Transaksi
            </h1>
            <p class="text-lg text-gray-700 max-w-2xl mx-auto">
                Kelola dan pantau semua riwayat pembayaran Anda dengan mudah.
            </p>
            <div
                class="mt-8 bg-white p-6 rounded-2xl shadow-lg inline-flex items-center space-x-4"
            >
                <DollarSign class="w-8 h-8 text-green-600" />
                <div>
                    <p class="text-sm text-gray-500 font-medium">
                        Total Pembayaran
                    </p>
                    <p class="text-2xl font-bold text-green-700">
                        {formatCurrency(totalAmount)}
                    </p>
                </div>
            </div>
        </header>

        <div class="bg-white rounded-3xl shadow-xl overflow-hidden">
            <div class="p-6 border-b border-gray-100">
                <h2
                    class="text-2xl font-bold text-gray-800 flex items-center gap-2"
                >
                    <Clock class="w-6 h-6 text-indigo-500" /> Riwayat Pembayaran
                    ({payments.length})
                </h2>
            </div>

            <div class="divide-y divide-gray-100">
                {#each payments as payment (payment.id)}
                    <div
                        class="p-6 flex flex-col sm:flex-row justify-between items-start sm:items-center gap-4 group hover:bg-gray-50 transition-all duration-200 ease-in-out"
                    >
                        <div class="flex items-center gap-4 flex-grow">
                            <div
                                class="flex-shrink-0 p-3 rounded-full
                                {payment.status === 'Paid'
                                    ? 'bg-green-100 text-green-600'
                                    : ''}
                                {payment.status === 'Pending'
                                    ? 'bg-yellow-100 text-yellow-600'
                                    : ''}
                                {payment.status === 'Failed'
                                    ? 'bg-red-100 text-red-600'
                                    : ''}"
                            >
                                {#if payment.status === "Paid"}
                                    <CheckCircle class="w-5 h-5" />
                                {:else if payment.status === "Pending"}
                                    <Clock class="w-5 h-5" />
                                {:else}
                                    <XCircle class="w-5 h-5" />
                                {/if}
                            </div>

                            <div class="flex flex-col">
                                <h3
                                    class="text-xl font-semibold text-gray-900 flex items-center gap-2"
                                >
                                    <User class="w-4 h-4 text-indigo-400" />
                                    {payment.name}
                                </h3>
                                <p
                                    class="text-sm text-gray-500 flex items-center gap-1 mt-1"
                                >
                                    <CalendarDays class="w-4 h-4" />
                                    {formatDate(payment.date)}
                                </p>
                            </div>
                        </div>

                        <div
                            class="text-left sm:text-right flex flex-col items-start sm:items-end"
                        >
                            <p class="text-2xl font-extrabold text-indigo-700">
                                {formatCurrency(payment.amount)}
                            </p>
                            <span
                                class="inline-block mt-1 px-3 py-1 rounded-full text-xs font-semibold uppercase tracking-wide
                                {payment.status === 'Paid'
                                    ? 'bg-green-500 text-white'
                                    : payment.status === 'Pending'
                                      ? 'bg-yellow-500 text-white'
                                      : 'bg-red-500 text-white'}"
                            >
                                {payment.status === "Paid"
                                    ? "Berhasil"
                                    : payment.status === "Pending"
                                      ? "Tertunda"
                                      : "Gagal"}
                            </span>
                        </div>
                    </div>
                {/each}
            </div>

            {#if payments.length === 0}
                <div class="p-8 text-center text-gray-500">
                    <p class="text-lg">Belum ada transaksi yang tercatat.</p>
                </div>
            {/if}
        </div>
    </div>
</section>

<style>
    /* Add a subtle wave animation for the emoji */
    @keyframes wave {
        0% {
            transform: rotate(0deg);
        }
        10% {
            transform: rotate(14deg);
        }
        20% {
            transform: rotate(-8deg);
        }
        30% {
            transform: rotate(14deg);
        }
        40% {
            transform: rotate(-4deg);
        }
        50% {
            transform: rotate(10deg);
        }
        60% {
            transform: rotate(0deg);
        }
        100% {
            transform: rotate(0deg);
        }
    }

    .animate-wave {
        animation: wave 2.5s infinite;
        transform-origin: 70% 70%;
        display: inline-block; /* Essential for animation */
    }
</style>
