<script lang="ts">
  const featuredProperties = [
    {
      id: 1,
      title: "Luxury Penthouse",
      location: "Miami, FL",
      price: "2,500,000",
      yield: "8.5",
      image: "https://images.unsplash.com/photo-1512917774080-9991f1c4c750?auto=format&w=800&q=80",
      tokenized: "75"
    },
    {
      id: 2,
      title: "Modern Office Complex",
      location: "Austin, TX",
      price: "4,800,000",
      yield: "7.2",
      image: "https://images.unsplash.com/photo-1486406146926-c627a92ad1ab?auto=format&w=800&q=80",
      tokenized: "60"
    },
    {
      id: 3,
      title: "Beachfront Villa",
      location: "Malibu, CA",
      price: "3,200,000",
      yield: "6.8",
      image: "https://images.unsplash.com/photo-1523217582562-09d0def993a6?auto=format&w=800&q=80",
      tokenized: "45"
    }
  ];

  const stats = [
    { label: "Total Value Locked", value: "$50M+" },
    { label: "Active Investors", value: "10,000+" },
    { label: "Properties Tokenized", value: "150+" },
    { label: "Average Annual Yield", value: "7.8%" }
  ];
</script>

<div class="space-y-24 pb-24">
  <!-- Hero Section -->
  <section class="relative h-[90vh] flex items-center justify-center overflow-hidden">
    <div class="absolute inset-0 z-0">
      <div class="absolute inset-0 bg-gradient-to-r from-blue-900/80 to-purple-900/80 mix-blend-multiply"></div>
      <video 
        class="w-full h-full object-cover"
        autoplay 
        muted 
        loop 
        playsinline
      >
        <source src="https://assets.mixkit.co/videos/preview/mixkit-aerial-view-of-city-buildings-during-night-time-41465-large.mp4" type="video/mp4">
      </video>
    </div>
    
    <div class="relative z-10 max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 text-center">
      <h1 class="text-5xl md:text-7xl font-bold mb-8 bg-clip-text text-transparent bg-gradient-to-r from-blue-400 to-purple-600">
        Own Real Estate<br/>in the Digital Age
      </h1>
      <p class="text-xl md:text-2xl text-gray-200 mb-12 max-w-3xl mx-auto">
        Invest in premium properties worldwide through blockchain technology. 
        Start with as little as $100.
      </p>
      <div class="flex flex-col sm:flex-row gap-4 justify-center">
        <button class="px-8 py-4 rounded-lg bg-gradient-to-r from-blue-500 to-purple-600 hover:from-blue-600 hover:to-purple-700 transition-all text-lg font-semibold">
          Start Investing
        </button>
        <button class="px-8 py-4 rounded-lg border border-white/20 hover:bg-white/10 transition-all text-lg font-semibold">
          Learn More
        </button>
      </div>
    </div>
  </section>

  <!-- Stats Section -->
  <section class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
    <div class="grid grid-cols-2 md:grid-cols-4 gap-8">
      {#each stats as stat}
        <div class="text-center p-6 rounded-2xl bg-white/5 backdrop-blur-lg border border-white/10">
          <p class="text-3xl md:text-4xl font-bold bg-clip-text text-transparent bg-gradient-to-r from-blue-400 to-purple-600">
            {stat.value}
          </p>
          <p class="text-gray-400 mt-2">{stat.label}</p>
        </div>
      {/each}
    </div>
  </section>

  <!-- Featured Properties -->
  <section class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
    <h2 class="text-3xl md:text-4xl font-bold mb-12 text-center">Featured Properties</h2>
    <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
      {#each featuredProperties as property}
        <div class="rounded-2xl overflow-hidden bg-white/5 backdrop-blur-lg border border-white/10 hover:border-white/20 transition-all">
          <div class="relative h-48">
            <img src={property.image} alt={property.title} class="w-full h-full object-cover"/>
            <div class="absolute top-4 right-4 px-3 py-1 rounded-full bg-black/50 backdrop-blur-md text-sm">
              {property.tokenized}% Tokenized
            </div>
          </div>
          <div class="p-6">
            <h3 class="text-xl font-semibold mb-2">{property.title}</h3>
            <p class="text-gray-400 mb-4">{property.location}</p>
            <div class="flex justify-between items-center">
              <div>
                <p class="text-sm text-gray-400">Property Value</p>
                <p class="text-lg font-semibold">${property.price}</p>
              </div>
              <div class="text-right">
                <p class="text-sm text-gray-400">Expected Yield</p>
                <p class="text-lg font-semibold text-green-400">{property.yield}%</p>
              </div>
            </div>
            <button class="w-full mt-6 px-4 py-2 rounded-lg bg-white/10 hover:bg-white/20 transition-all">
              View Details
            </button>
          </div>
        </div>
      {/each}
    </div>
  </section>

  <!-- How It Works -->
  <section class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
    <h2 class="text-3xl md:text-4xl font-bold mb-12 text-center">How It Works</h2>
    <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
      <div class="text-center p-8 rounded-2xl bg-white/5 backdrop-blur-lg border border-white/10">
        <div class="w-16 h-16 mx-auto mb-6 rounded-full bg-gradient-to-r from-blue-500 to-purple-600 flex items-center justify-center text-2xl font-bold">1</div>
        <h3 class="text-xl font-semibold mb-4">Connect Wallet</h3>
        <p class="text-gray-400">Link your Solana wallet to start investing in tokenized real estate</p>
      </div>
      <div class="text-center p-8 rounded-2xl bg-white/5 backdrop-blur-lg border border-white/10">
        <div class="w-16 h-16 mx-auto mb-6 rounded-full bg-gradient-to-r from-blue-500 to-purple-600 flex items-center justify-center text-2xl font-bold">2</div>
        <h3 class="text-xl font-semibold mb-4">Choose Properties</h3>
        <p class="text-gray-400">Browse our curated selection of premium real estate investments</p>
      </div>
      <div class="text-center p-8 rounded-2xl bg-white/5 backdrop-blur-lg border border-white/10">
        <div class="w-16 h-16 mx-auto mb-6 rounded-full bg-gradient-to-r from-blue-500 to-purple-600 flex items-center justify-center text-2xl font-bold">3</div>
        <h3 class="text-xl font-semibold mb-4">Start Earning</h3>
        <p class="text-gray-400">Receive your share of rental income and property appreciation</p>
      </div>
    </div>
  </section>
</div>
