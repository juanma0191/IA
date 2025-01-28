<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AI Business Assistant</title>
    <link href="https://cdn.jsdelivr.net/npm/tailwindcss@2.2.19/dist/tailwind.min.css" rel="stylesheet">
    <script src="https://js.stripe.com/v3/"></script>
    <style>
        body {
            font-family: 'Inter', sans-serif;
            color: #333333;
            scroll-behavior: smooth;
            background-color: #f9fafb;
        }
        .gradient-bg {
            background: linear-gradient(90deg, #2563eb, #1d4ed8);
            color: white;
        }
        .hero {
            background: url('https://source.unsplash.com/1600x900/?business,technology');
            background-size: cover;
            background-position: center;
            color: #1f2937;
        }
        .hover-effect:hover {
            transform: scale(1.05);
            transition: all 0.3s ease-in-out;
        }
        .light-card {
            background-color: #ffffff;
            border: 1px solid #e5e7eb;
            box-shadow: 0px 4px 20px rgba(0, 0, 0, 0.1);
        }
        .text-primary {
            color: #2563eb;
        }
    </style>
    <script>
        let isSubscribed = false;

        async function handleSubscription() {
            const stripe = Stripe('your-stripe-public-key'); // Replace with your Stripe public key
            try {
                const { error } = await stripe.redirectToCheckout({
                    lineItems: [{ price: 'price_1...', quantity: 1 }], // Replace with your price ID
                    mode: 'subscription',
                    successUrl: window.location.href + '?subscribed=true',
                    cancelUrl: window.location.href,
                });
                if (error) {
                    console.error('Stripe error:', error);
                }
            } catch (err) {
                console.error('Unexpected error:', err);
            }
        }

        function checkSubscriptionStatus() {
            try {
                const urlParams = new URLSearchParams(window.location.search);
                if (urlParams.get('subscribed') === 'true') {
                    isSubscribed = true;
                    document.getElementById('assistant-access').style.display = 'block';
                    document.getElementById('subscribe-message').style.display = 'none';
                } else {
                    document.getElementById('assistant-access').style.display = 'none';
                    document.getElementById('subscribe-message').style.display = 'block';
                }
            } catch (error) {
                console.error('Error checking subscription status:', error);
            }
        }

        document.addEventListener('DOMContentLoaded', checkSubscriptionStatus);
    </script>
</head>
<body>
    <!-- Header Section -->
    <header class="gradient-bg p-6 sticky top-0 z-50">
        <div class="container mx-auto flex justify-between items-center">
            <h1 class="text-3xl font-bold">AI Business Assistant</h1>
            <nav class="space-x-6">
                <a href="#features" class="text-lg hover:underline">Features</a>
                <a href="#assistant" class="text-lg hover:underline">Assistant</a>
                <a href="#pricing" class="text-lg hover:underline">Pricing</a>
                <a href="#contact" class="text-lg hover:underline">Contact</a>
            </nav>
        </div>
    </header>

    <!-- Hero Section -->
    <section class="hero h-screen flex flex-col justify-center items-center text-center">
        <h2 class="text-6xl font-extrabold mb-6">Supercharge Your Business with AI</h2>
        <p class="text-2xl mb-8 text-gray-700">Unlock new levels of efficiency, innovation, and growth with our tailored AI solutions.</p>
        <div class="space-x-4">
            <a href="#pricing" class="px-8 py-4 bg-blue-600 rounded-full text-xl text-white hover:bg-blue-700 hover-effect">Subscribe Now</a>
            <a href="#features" class="px-8 py-4 border border-blue-600 rounded-full text-xl text-blue-600 hover:bg-blue-600 hover:text-white transition">Learn More</a>
        </div>
    </section>

    <!-- Features Section -->
    <section id="features" class="py-20">
        <div class="container mx-auto text-center mb-12">
            <h3 class="text-5xl font-bold mb-4 text-primary">Our Features</h3>
            <p class="text-lg text-gray-500">Discover how our AI solutions transform your business.</p>
        </div>
        <div class="grid grid-cols-1 md:grid-cols-3 gap-12">
            <div class="p-6 light-card text-center rounded-lg hover-effect">
                <img src="https://source.unsplash.com/100x100/?automation" alt="Automation" class="mx-auto mb-4">
                <h4 class="text-2xl font-semibold mb-2">Task Automation</h4>
                <p class="text-gray-600">Streamline operations by automating repetitive tasks.</p>
            </div>
            <div class="p-6 light-card text-center rounded-lg hover-effect">
                <img src="https://source.unsplash.com/100x100/?data" alt="Data Insights" class="mx-auto mb-4">
                <h4 class="text-2xl font-semibold mb-2">Data Insights</h4>
                <p class="text-gray-600">Leverage AI-driven insights for smarter decision-making.</p>
            </div>
            <div class="p-6 light-card text-center rounded-lg hover-effect">
                <img src="https://source.unsplash.com/100x100/?support" alt="24/7 Support" class="mx-auto mb-4">
                <h4 class="text-2xl font-semibold mb-2">24/7 Support</h4>
                <p class="text-gray-600">AI assistance available whenever you need it.</p>
            </div>
        </div>
    </section>

    <!-- Success Stories Section -->
    <section id="success-stories" class="py-20 bg-gray-100">
        <div class="container mx-auto mb-12 text-center">
            <h3 class="text-5xl font-bold mb-4 text-primary">Success Stories</h3>
            <p class="text-lg text-gray-500">See how companies are saving time and optimizing workflows with AI.</p>
        </div>
        <div class="grid grid-cols-1 md:grid-cols-3 lg:grid-cols-3 gap-8">
            <div class="p-6 light-card rounded-lg shadow-md text-center">
                <h4 class="text-xl font-semibold">Global Law Firm</h4>
                <p class="text-gray-600 text-sm mb-2">Automates compiling and analysis of legal docs</p>
                <p class="text-blue-600 text-3xl font-bold">62%</p>
                <p class="text-gray-600">Time Savings</p>
            </div>
            <div class="p-6 light-card rounded-lg shadow-md text-center">
                <h4 class="text-xl font-semibold">European Fintech</h4>
                <p class="text-gray-600 text-sm mb-2">Uses AI agent for new hire onboarding</p>
                <p class="text-blue-600 text-3xl font-bold">12h®️</p>
                <p class="text-gray-600">Saved per week/employee</p>
            </div>
            <div class="p-6 light-card rounded-lg shadow-md text-center">
                <h4 class="text-xl font-semibold">Real Estate Leader</h4>
                <p class="text-gray-600 text-sm mb-2">Automates analysis workflows</p>
                <p class="text-blue-600 text-3xl font-bold">50%</p>
                <p class="text-gray-600">Time Savings</p>
            </div>
            <div class="p-6 light-card rounded-lg shadow-md text-center">
                <h4 class="text-xl font-semibold">Industrial Leader</h4>
                <p class="text-gray-600 text-sm mb-2">Augments customer support</p>
                <p class="text-blue-600 text-3xl font-bold">2x</p>
                <p class="text-gray-600">Issues Resolved</p>
            </div>
            <div class="p-6 light-card rounded-lg shadow-md text-center">
                <h4 class="text-xl font-semibold">Energy Innovator</h4>
                <p class="text-gray-600 text-sm mb-2">Automates compliance audit process</p>
                <p class="text-blue-600 text-3xl font-bold">66%</p>
                <p class="text-gray-600">Time Savings</p>
            </div>
            <div class="p-6 light-card rounded-lg shadow-md text-center">
                <h4 class="text-xl font-semibold">Manufacturer</h4>
                <p class="text-gray-600 text-sm mb-2">Uses AI agent to answer product questions</p>
                <p class="text-blue-600 text-3xl font-bold">95%</p>
                <p class="text-gray-600">Time Savings</p>
            </div>
        </div>
    </section>

    <!-- Pricing Section -->
    <section id="pricing" class="py-20 bg-gray-100">
        <div class="container mx-auto text-center mb-12">
            <h3 class="text-5xl font-bold mb-4 text-primary">Affordable Pricing</h3>
            <p class="text-lg text-gray-500">Unlock full access to our AI assistant for just €25 per month.</p>
        </div>
        <div class="max-w-md mx-auto light-card p-8 rounded-lg text-center shadow-lg">
            <h4 class="text-3xl font-bold mb-4">€25 / Month</h4>
            <p class="text-gray-600 mb-6">Enjoy unlimited access to advanced AI tools and 24/7 assistance.</p>
            <button onclick="handleSubscription()" class="w-full py-3 bg-blue-600 text-white text-xl rounded-lg hover:bg-blue-700">Subscribe Now</button>
        </div>
    </section>

    <!-- AI Assistant Section -->
    <section id="assistant" class="py-20">
        <div class="container mx-auto text-center mb-12">
            <h3 class="text-5xl font-bold mb-4 text-primary">Meet Your AI Assistant</h3>
            <p id="subscribe-message" class="text-lg text-gray-500">Subscribe to access the AI assistant.</p>
            <div id="assistant-access" style="display: none;">
                <div class="max-w-3xl mx-auto light-card p-8 rounded-lg shadow-lg">
                    <div id="chat-box" class="h-96 overflow-y-scroll p-4 border rounded-lg bg-gray-100">
                        <div class="p-2 my-2 bg-blue-600 text-white
