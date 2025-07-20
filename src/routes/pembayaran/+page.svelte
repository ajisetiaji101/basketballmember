<script lang="ts">
    import QRCode from "qrcode";

    import qris from "$lib/images/payment/qris.png";
    import mandiri from "$lib/images/payment/mandiri.png";
    import bca from "$lib/images/payment/bca.png";
    import bni from "$lib/images/payment/bni.png";
    import dana from "$lib/images/payment/dana.png";
    import gopay from "$lib/images/payment/gopay.jpg";

    let name = "Member Basketball";
    let email = "member@example.com";
    let amount = "1000000";

    let paymentMethod = "qris";
    let qrCodeDataUrl: string | null = null;

    const methods = [
        { id: "qris", label: "QRIS", logo: qris },
        { id: "mandiri", label: "Mandiri", logo: mandiri },
        { id: "bca", label: "BCA", logo: bca },
        { id: "bni", label: "BNI", logo: bni },
        { id: "dana", label: "DANA", logo: dana },
        { id: "gopay", label: "GoPay", logo: gopay },
    ];

    const handleSubmit = async (event: Event) => {
        event.preventDefault();
        const paymentData = `Nama: ${name}, Email: ${email}, Jumlah: Rp${amount}, Metode: ${paymentMethod}`;
        try {
            qrCodeDataUrl = await QRCode.toDataURL(paymentData);
        } catch (err) {
            console.error("Gagal generate QR:", err);
        }
    };
</script>

<div
    class="min-h-screen flex items-center justify-center bg-gradient-to-br from-indigo-200 via-white to-blue-100 px-4 py-10"
>
    <div
        class="bg-white w-full max-w-xl rounded-3xl shadow-2xl p-10 space-y-8 animate-fade-in"
    >
        <h2
            class="text-3xl font-extrabold text-center text-indigo-700 drop-shadow-md"
        >
            Pembayaran Membership Basketball Club
        </h2>

        <form on:submit={handleSubmit} class="space-y-6 animate-slide-up">
            <div class="space-y-4 text-gray-700">
                <div class="flex justify-between border-b pb-2">
                    <span class="font-medium">Nama</span>
                    <span>{name}</span>
                </div>
                <div class="flex justify-between border-b pb-2">
                    <span class="font-medium">Email</span>
                    <span>{email}</span>
                </div>
                <div class="flex justify-between border-b pb-2">
                    <span class="font-medium">Jumlah</span>
                    <span class="text-indigo-600 font-semibold"
                        >Rp {amount}</span
                    >
                </div>
            </div>

            <div>
                <label class="block text-sm font-medium text-gray-700 mb-2">
                    Pilih Metode Pembayaran
                </label>
                <div class="grid grid-cols-3 gap-4">
                    {#each methods as method}
                        <div
                            class="border rounded-xl p-2 flex flex-col items-center cursor-pointer transition-all duration-200 hover:scale-105 hover:shadow-md"
                            class:border-indigo-500={paymentMethod ===
                                method.id}
                            class:ring-2={paymentMethod === method.id}
                            class:ring-indigo-400={paymentMethod === method.id}
                            on:click={() => (paymentMethod = method.id)}
                        >
                            <img
                                src={method.logo}
                                alt={method.label}
                                class="w-14 h-14 object-contain mb-1"
                            />
                            <span
                                class="text-sm font-medium"
                                class:text-indigo-600={paymentMethod ===
                                    method.id}
                            >
                                {method.label}
                            </span>
                        </div>
                    {/each}
                </div>
            </div>

            <button
                type="submit"
                class="w-full py-2 px-4 bg-indigo-600 hover:bg-indigo-700 text-white font-semibold rounded-xl transition duration-200 shadow-md hover:shadow-lg"
            >
                Bayar Sekarang
            </button>
        </form>

        {#if qrCodeDataUrl}
            <div class="text-center space-y-3 pt-6 animate-scale-in">
                <p class="text-lg text-gray-700 font-medium">
                    Scan QR Code untuk membayar
                </p>
                <img
                    src={qrCodeDataUrl}
                    alt="QR Code"
                    class="mx-auto w-48 h-48 rounded-xl shadow-lg border"
                />
            </div>
        {/if}
    </div>
</div>

<style>
    @keyframes fade-in {
        from {
            opacity: 0;
            transform: scale(0.95);
        }
        to {
            opacity: 1;
            transform: scale(1);
        }
    }

    @keyframes slide-up {
        from {
            opacity: 0;
            transform: translateY(20px);
        }
        to {
            opacity: 1;
            transform: translateY(0);
        }
    }

    @keyframes scale-in {
        from {
            transform: scale(0.5);
            opacity: 0;
        }
        to {
            transform: scale(1);
            opacity: 1;
        }
    }

    .animate-fade-in {
        animation: fade-in 0.6s ease-out forwards;
    }

    .animate-slide-up {
        animation: slide-up 0.6s ease-out forwards;
    }

    .animate-scale-in {
        animation: scale-in 0.4s ease-out forwards;
    }
</style>
