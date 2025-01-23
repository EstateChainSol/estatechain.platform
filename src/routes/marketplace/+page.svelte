<script lang="ts">
  let selectedProperty = "all";
  let orderType = "buy";
  let amount = "";
  let price = "";

  const properties = [
    {
      id: 1,
      name: "Luxury Penthouse",
      symbol: "LUXPH",
      price: 2.50,
      change: 5.2,
      volume: 125000,
      marketCap: 5000000
    },
    {
      id: 2,
      name: "Modern Office Complex",
      symbol: "MDOFF",
      price: 3.45,
      change: -2.1,
      volume: 89000,
      marketCap: 6900000
    },
    {
      id: 3,
      name: "Beachfront Villa",
      symbol: "BCHVL",
      price: 4.20,
      change: 1.8,
      volume: 67000,
      marketCap: 4200000
    }
  ];

  const orderBook = {
    bids: [
      { price: 2.48, amount: 5000, total: 12400 },
      { price: 2.47, amount: 7500, total: 18525 },
      { price: 2.46, amount: 10000, total: 24600 },
      { price: 2.45, amount: 15000, total: 36750 },
      { price: 2.44, amount: 20000, total: 48800 }
    ],
    asks: [
      { price: 2.52, amount: 4000, total: 10080 },
      { price: 2.53, amount: 6000, total: 15180 },
      { price: 2.54, amount: 8000, total: 20320 },
      { price: 2.55, amount: 12000, total: 30600 },
      { price: 2.56, amount: 15000, total: 38400 }
    ]
  };

  const recentTrades = [
    { time: "14:32:15", price: 2.50, amount: 2000, type: "buy" },
    { time: "14:31:55", price: 2.49, amount: 1500, type: "sell" },
    { time: "14:31:30", price: 2.50, amount: 3000, type: "buy" },
    { time: "14:30:45", price: 2.48, amount: 5000, type: "sell" },
    { time: "14:30:15", price: 2.51, amount: 2500, type: "buy" }
  ];

  const formatCurrency = (amount: number) => {
    return new Intl.NumberFormat('en-US', {
      style: 'currency',
      currency: 'USD',
      minimumFractionDigits: 2,
      maximumFractionDigits: 2,
    }).format(amount);
  };

  const formatNumber = (num: number) => {
    return new Intl.NumberFormat('en-US').format(num);
  };
</script>

<div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-12">
  <!-- Header -->
  <div class="mb-12">
    <h1 class="text-4xl font-bold mb-4">Token Marketplace</h1>
    <p class="text-gray-400">Trade property tokens in real-time</p>
  </div>

  <!-- Market Overview -->
  <div class="grid grid-cols-1 md:grid-cols-3 gap-8 mb-12">
    {#each properties as property}
      <div class="p-6 rounded-2xl bg-white/5 backdrop-blur-lg border border-white/10">
        <div class="flex justify-between items-start mb-4">
          <div>
            <h3 class="text-xl font-semibold">{property.name}</h3>
            <p class="text-gray-400">{property.symbol}</p>
          </div>
          <span class={`px-3 py-1 rounded-full ${property.change >= 0 ? 'bg-green-500/20 text-green-400' : 'bg-red-500/20 text-red-400'}`}>
            {property.change >= 0 ? '+' : ''}{property.change}%
          </span>
        </div>
        <div class="grid grid-cols-2 gap-4">
          <div>
            <p class="text-sm text-gray-400">Price</p>
            <p class="text-lg font-semibold">{formatCurrency(property.price)}</p>
          </div>
          <div>
            <p class="text-sm text-gray-400">Volume</p>
            <p class="text-lg font-semibold">{formatNumber(property.volume)}</p>
          </div>
        </div>
      </div>
    {/each}
  </div>

  <div class="grid grid-cols-1 lg:grid-cols-3 gap-8">
    <!-- Trading Interface -->
    <div class="lg:col-span-2 grid grid-cols-1 md:grid-cols-2 gap-8">
      <!-- Order Book -->
      <div class="space-y-6">
        <h2 class="text-2xl font-bold mb-6">Order Book</h2>
        <div class="p-6 rounded-2xl bg-white/5 backdrop-blur-lg border border-white/10">
          <!-- Asks -->
          <div class="space-y-2 mb-4">
            {#each orderBook.asks.slice().reverse() as ask}
              <div class="flex justify-between text-sm">
                <span class="text-red-400">{formatCurrency(ask.price)}</span>
                <span>{formatNumber(ask.amount)}</span>
                <span class="text-gray-400">{formatCurrency(ask.total)}</span>
              </div>
            {/each}
          </div>

          <!-- Spread -->
          <div class="text-center py-2 border-y border-white/10 mb-4">
            <span class="text-sm text-gray-400">Spread: {formatCurrency(orderBook.asks[0].price - orderBook.bids[0].price)}</span>
          </div>

          <!-- Bids -->
          <div class="space-y-2">
            {#each orderBook.bids as bid}
              <div class="flex justify-between text-sm">
                <span class="text-green-400">{formatCurrency(bid.price)}</span>
                <span>{formatNumber(bid.amount)}</span>
                <span class="text-gray-400">{formatCurrency(bid.total)}</span>
              </div>
            {/each}
          </div>
        </div>
      </div>

      <!-- Trade Form -->
      <div class="space-y-6">
        <h2 class="text-2xl font-bold mb-6">Place Order</h2>
        <div class="p-6 rounded-2xl bg-white/5 backdrop-blur-lg border border-white/10">
          <div class="space-y-4">
            <div>
              <label class="block text-sm text-gray-400 mb-2">Select Property</label>
              <select
                bind:value={selectedProperty}
                class="w-full bg-white/5 border border-white/10 rounded-lg px-4 py-2 text-white focus:outline-none focus:border-blue-500"
              >
                <option value="all">Select Property</option>
                {#each properties as property}
                  <option value={property.symbol}>{property.name}</option>
                {/each}
              </select>
            </div>

            <div>
              <label class="block text-sm text-gray-400 mb-2">Order Type</label>
              <div class="grid grid-cols-2 gap-4">
                <button
                  class={`px-4 py-2 rounded-lg ${orderType === 'buy' ? 'bg-green-500/20 text-green-400 border-green-500/50' : 'bg-white/5 text-gray-400 border-white/10'} border`}
                  on:click={() => orderType = 'buy'}
                >
                  Buy
                </button>
                <button
                  class={`px-4 py-2 rounded-lg ${orderType === 'sell' ? 'bg-red-500/20 text-red-400 border-red-500/50' : 'bg-white/5 text-gray-400 border-white/10'} border`}
                  on:click={() => orderType = 'sell'}
                >
                  Sell
                </button>
              </div>
            </div>

            <div>
              <label class="block text-sm text-gray-400 mb-2">Amount</label>
              <input
                type="number"
                bind:value={amount}
                placeholder="Enter amount"
                class="w-full bg-white/5 border border-white/10 rounded-lg px-4 py-2 text-white focus:outline-none focus:border-blue-500"
              />
            </div>

            <div>
              <label class="block text-sm text-gray-400 mb-2">Price</label>
              <input
                type="number"
                bind:value={price}
                placeholder="Enter price"
                class="w-full bg-white/5 border border-white/10 rounded-lg px-4 py-2 text-white focus:outline-none focus:border-blue-500"
              />
            </div>

            <button
              class={`w-full px-4 py-3 rounded-lg font-semibold ${
                orderType === 'buy'
                  ? 'bg-gradient-to-r from-green-500 to-green-600 hover:from-green-600 hover:to-green-700'
                  : 'bg-gradient-to-r from-red-500 to-red-600 hover:from-red-600 hover:to-red-700'
              } transition-all`}
            >
              {orderType === 'buy' ? 'Buy' : 'Sell'} Tokens
            </button>
          </div>
        </div>
      </div>
    </div>

    <!-- Recent Trades -->
    <div>
      <h2 class="text-2xl font-bold mb-6">Recent Trades</h2>
      <div class="p-6 rounded-2xl bg-white/5 backdrop-blur-lg border border-white/10">
        <div class="space-y-4">
          {#each recentTrades as trade}
            <div class="flex justify-between items-center">
              <div>
                <p class="text-sm text-gray-400">{trade.time}</p>
                <p class={`font-semibold ${trade.type === 'buy' ? 'text-green-400' : 'text-red-400'}`}>
                  {formatCurrency(trade.price)}
                </p>
              </div>
              <div class="text-right">
                <p class="font-semibold">{formatNumber(trade.amount)}</p>
                <p class="text-sm text-gray-400">{formatCurrency(trade.price * trade.amount)}</p>
              </div>
            </div>
          {/each}
        </div>
      </div>
    </div>
  </div>
</div> 