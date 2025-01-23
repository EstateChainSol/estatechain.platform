<script lang="ts">
  let selectedType = "all";
  let selectedLocation = "all";
  let minPrice = 0;
  let maxPrice = 10000000;
  let sortBy = "newest";

  const properties = [
    {
      id: 1,
      title: "Luxury Penthouse",
      location: "Miami, FL",
      price: 2500000,
      yield: 8.5,
      type: "residential",
      image: "https://images.unsplash.com/photo-1512917774080-9991f1c4c750?auto=format&w=800&q=80",
      tokenized: 75,
      sqft: 3200,
      bedrooms: 3,
      bathrooms: 3.5,
      yearBuilt: 2020
    },
    {
      id: 2,
      title: "Modern Office Complex",
      location: "Austin, TX",
      price: 4800000,
      yield: 7.2,
      type: "commercial",
      image: "https://images.unsplash.com/photo-1486406146926-c627a92ad1ab?auto=format&w=800&q=80",
      tokenized: 60,
      sqft: 12000,
      yearBuilt: 2019
    },
    {
      id: 3,
      title: "Beachfront Villa",
      location: "Malibu, CA",
      price: 3200000,
      yield: 6.8,
      type: "residential",
      image: "https://images.unsplash.com/photo-1523217582562-09d0def993a6?auto=format&w=800&q=80",
      tokenized: 45,
      sqft: 4500,
      bedrooms: 5,
      bathrooms: 4,
      yearBuilt: 2018
    },
    {
      id: 4,
      title: "Retail Shopping Center",
      location: "Denver, CO",
      price: 6500000,
      yield: 7.8,
      type: "retail",
      image: "https://images.unsplash.com/photo-1519420573924-65fcd45245f8?auto=format&w=800&q=80",
      tokenized: 85,
      sqft: 25000,
      yearBuilt: 2015
    },
    {
      id: 5,
      title: "Industrial Warehouse",
      location: "Phoenix, AZ",
      price: 3800000,
      yield: 8.2,
      type: "industrial",
      image: "https://images.unsplash.com/photo-1586528116311-ad8dd3c8310d?auto=format&w=800&q=80",
      tokenized: 65,
      sqft: 40000,
      yearBuilt: 2017
    },
    {
      id: 6,
      title: "Downtown Apartment Complex",
      location: "Seattle, WA",
      price: 7200000,
      yield: 6.5,
      type: "residential",
      image: "https://images.unsplash.com/photo-1545324418-cc1a3fa10c00?auto=format&w=800&q=80",
      tokenized: 90,
      sqft: 18000,
      bedrooms: 24,
      bathrooms: 24,
      yearBuilt: 2016
    }
  ];

  $: filteredProperties = properties
    .filter(p => selectedType === "all" || p.type === selectedType)
    .filter(p => selectedLocation === "all" || p.location === selectedLocation)
    .filter(p => p.price >= minPrice && p.price <= maxPrice)
    .sort((a, b) => {
      if (sortBy === "price-low") return a.price - b.price;
      if (sortBy === "price-high") return b.price - a.price;
      if (sortBy === "yield") return b.yield - a.yield;
      return b.id - a.id; // newest
    });

  const formatPrice = (price: number) => {
    return new Intl.NumberFormat('en-US', {
      style: 'currency',
      currency: 'USD',
      minimumFractionDigits: 0,
      maximumFractionDigits: 0,
    }).format(price);
  };
</script>

<svelte:head>
  <title>Properties | EstateChain</title>
</svelte:head>

<div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-12">
  <!-- Header -->
  <div class="mb-12">
    <h1 class="text-4xl font-bold mb-4">Available Properties</h1>
    <p class="text-gray-400">Discover and invest in premium real estate opportunities</p>
  </div>

  <!-- Filters -->
  <div class="grid grid-cols-1 md:grid-cols-5 gap-4 mb-8">
    <select
      bind:value={selectedType}
      class="bg-white/5 border border-white/10 rounded-lg px-4 py-2 text-white focus:outline-none focus:border-blue-500"
    >
      <option value="all">All Types</option>
      <option value="residential">Residential</option>
      <option value="commercial">Commercial</option>
      <option value="retail">Retail</option>
      <option value="industrial">Industrial</option>
    </select>

    <select
      bind:value={selectedLocation}
      class="bg-white/5 border border-white/10 rounded-lg px-4 py-2 text-white focus:outline-none focus:border-blue-500"
    >
      <option value="all">All Locations</option>
      <option value="Miami, FL">Miami, FL</option>
      <option value="Austin, TX">Austin, TX</option>
      <option value="Malibu, CA">Malibu, CA</option>
      <option value="Denver, CO">Denver, CO</option>
      <option value="Phoenix, AZ">Phoenix, AZ</option>
      <option value="Seattle, WA">Seattle, WA</option>
    </select>

    <input
      type="number"
      bind:value={minPrice}
      placeholder="Min Price"
      class="bg-white/5 border border-white/10 rounded-lg px-4 py-2 text-white focus:outline-none focus:border-blue-500"
    />

    <input
      type="number"
      bind:value={maxPrice}
      placeholder="Max Price"
      class="bg-white/5 border border-white/10 rounded-lg px-4 py-2 text-white focus:outline-none focus:border-blue-500"
    />

    <select
      bind:value={sortBy}
      class="bg-white/5 border border-white/10 rounded-lg px-4 py-2 text-white focus:outline-none focus:border-blue-500"
    >
      <option value="newest">Newest First</option>
      <option value="price-low">Price: Low to High</option>
      <option value="price-high">Price: High to Low</option>
      <option value="yield">Highest Yield</option>
    </select>
  </div>

  <!-- Property Grid -->
  <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
    {#each filteredProperties as property}
      <div class="rounded-2xl overflow-hidden bg-white/5 backdrop-blur-lg border border-white/10 hover:border-white/20 transition-all">
        <div class="relative h-48">
          <img src={property.image} alt={property.title} class="w-full h-full object-cover"/>
          <div class="absolute top-4 right-4 px-3 py-1 rounded-full bg-black/50 backdrop-blur-md text-sm">
            {property.tokenized}% Tokenized
          </div>
        </div>
        <div class="p-6">
          <div class="flex justify-between items-start mb-4">
            <div>
              <h3 class="text-xl font-semibold mb-2">{property.title}</h3>
              <p class="text-gray-400">{property.location}</p>
            </div>
            <span class="px-3 py-1 rounded-full bg-white/10 text-sm capitalize">
              {property.type}
            </span>
          </div>
          
          <div class="grid grid-cols-2 gap-4 mb-6">
            <div>
              <p class="text-sm text-gray-400">Property Value</p>
              <p class="text-lg font-semibold">{formatPrice(property.price)}</p>
            </div>
            <div class="text-right">
              <p class="text-sm text-gray-400">Expected Yield</p>
              <p class="text-lg font-semibold text-green-400">{property.yield}%</p>
            </div>
            <div>
              <p class="text-sm text-gray-400">Square Feet</p>
              <p class="text-lg font-semibold">{property.sqft.toLocaleString()}</p>
            </div>
            <div class="text-right">
              <p class="text-sm text-gray-400">Year Built</p>
              <p class="text-lg font-semibold">{property.yearBuilt}</p>
            </div>
          </div>

          {#if property.type === 'residential' && property.bedrooms}
            <div class="flex justify-between items-center py-4 border-t border-white/10 mb-6">
              <span class="flex items-center gap-2">
                <span class="text-gray-400">🛏</span>
                <span>{property.bedrooms} beds</span>
              </span>
              <span class="flex items-center gap-2">
                <span class="text-gray-400">🚿</span>
                <span>{property.bathrooms} baths</span>
              </span>
            </div>
          {/if}

          <button class="group relative w-full px-4 py-2 rounded-lg bg-gradient-to-r from-blue-500/50 to-purple-600/50 hover:from-blue-600/50 hover:to-purple-700/50 transition-all font-semibold">
            <span class="relative z-10 group-hover:opacity-0 transition-opacity">Invest Now</span>
            <span class="absolute inset-0 flex items-center justify-center opacity-0 group-hover:opacity-100 transition-opacity">
              Preview Only
            </span>
          </button>
        </div>
      </div>
    {/each}
  </div>
</div>
