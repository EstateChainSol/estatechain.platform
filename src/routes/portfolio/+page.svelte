<script lang="ts">
  const portfolioStats = [
    { label: "Total Investment", value: "$125,000" },
    { label: "Properties Owned", value: "4" },
    { label: "Total Earnings", value: "$12,450" },
    { label: "Average Yield", value: "7.2%" }
  ];

  const investments = [
    {
      id: 1,
      property: "Luxury Penthouse",
      location: "Miami, FL",
      investmentAmount: 50000,
      tokenAmount: 20000,
      ownership: 2.5,
      yield: 8.5,
      earnings: 4250,
      image: "https://images.unsplash.com/photo-1512917774080-9991f1c4c750?auto=format&w=800&q=80"
    },
    {
      id: 2,
      property: "Modern Office Complex",
      location: "Austin, TX",
      investmentAmount: 35000,
      tokenAmount: 14000,
      ownership: 1.2,
      yield: 7.2,
      earnings: 2520,
      image: "https://images.unsplash.com/photo-1486406146926-c627a92ad1ab?auto=format&w=800&q=80"
    },
    {
      id: 3,
      property: "Beachfront Villa",
      location: "Malibu, CA",
      investmentAmount: 25000,
      tokenAmount: 10000,
      ownership: 0.8,
      yield: 6.8,
      earnings: 1700,
      image: "https://images.unsplash.com/photo-1523217582562-09d0def993a6?auto=format&w=800&q=80"
    },
    {
      id: 4,
      property: "Retail Shopping Center",
      location: "Denver, CO",
      investmentAmount: 15000,
      tokenAmount: 6000,
      ownership: 0.4,
      yield: 7.8,
      earnings: 1170,
      image: "https://images.unsplash.com/photo-1519420573924-65fcd45245f8?auto=format&w=800&q=80"
    }
  ];

  const recentActivity = [
    {
      date: "2024-01-20",
      type: "Rental Income",
      property: "Luxury Penthouse",
      amount: 425
    },
    {
      date: "2024-01-19",
      type: "New Investment",
      property: "Retail Shopping Center",
      amount: 15000
    },
    {
      date: "2024-01-15",
      type: "Rental Income",
      property: "Modern Office Complex",
      amount: 210
    },
    {
      date: "2024-01-10",
      type: "Rental Income",
      property: "Beachfront Villa",
      amount: 142
    }
  ];

  const formatCurrency = (amount: number) => {
    return new Intl.NumberFormat('en-US', {
      style: 'currency',
      currency: 'USD',
      minimumFractionDigits: 0,
      maximumFractionDigits: 0,
    }).format(amount);
  };

  const formatDate = (dateStr: string) => {
    return new Date(dateStr).toLocaleDateString('en-US', {
      month: 'short',
      day: 'numeric',
      year: 'numeric'
    });
  };
</script>

<svelte:head>
  <title>Portfolio | EstateChain</title>
</svelte:head>

<div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-12">
  <!-- Header -->
  <div class="mb-12">
    <h1 class="text-4xl font-bold mb-4">My Portfolio</h1>
    <p class="text-gray-400">Track and manage your real estate investments</p>
  </div>

  <!-- Stats Grid -->
  <div class="grid grid-cols-2 md:grid-cols-4 gap-8 mb-12">
    {#each portfolioStats as stat}
      <div class="p-6 rounded-2xl bg-white/5 backdrop-blur-lg border border-white/10">
        <p class="text-gray-400 mb-2">{stat.label}</p>
        <p class="text-3xl font-bold bg-clip-text text-transparent bg-gradient-to-r from-blue-400 to-purple-600">
          {stat.value}
        </p>
      </div>
    {/each}
  </div>

  <div class="grid grid-cols-1 lg:grid-cols-3 gap-8">
    <!-- Investments List -->
    <div class="lg:col-span-2 space-y-6">
      <h2 class="text-2xl font-bold mb-6">My Investments</h2>
      {#each investments as investment}
        <div class="p-6 rounded-2xl bg-white/5 backdrop-blur-lg border border-white/10">
          <div class="flex gap-6">
            <img 
              src={investment.image} 
              alt={investment.property}
              class="w-24 h-24 rounded-lg object-cover"
            />
            <div class="flex-1">
              <div class="flex justify-between items-start mb-4">
                <div>
                  <h3 class="text-xl font-semibold">{investment.property}</h3>
                  <p class="text-gray-400">{investment.location}</p>
                </div>
                <span class="px-3 py-1 rounded-full bg-white/10 text-sm">
                  {investment.ownership}% Owned
                </span>
              </div>
              
              <div class="grid grid-cols-2 md:grid-cols-4 gap-4">
                <div>
                  <p class="text-sm text-gray-400">Investment</p>
                  <p class="font-semibold">{formatCurrency(investment.investmentAmount)}</p>
                </div>
                <div>
                  <p class="text-sm text-gray-400">Tokens</p>
                  <p class="font-semibold">{investment.tokenAmount.toLocaleString()} RT</p>
                </div>
                <div>
                  <p class="text-sm text-gray-400">Yield</p>
                  <p class="font-semibold text-green-400">{investment.yield}%</p>
                </div>
                <div>
                  <p class="text-sm text-gray-400">Earnings</p>
                  <p class="font-semibold text-green-400">+{formatCurrency(investment.earnings)}</p>
                </div>
              </div>
            </div>
          </div>
        </div>
      {/each}
    </div>

    <!-- Activity Feed -->
    <div>
      <h2 class="text-2xl font-bold mb-6">Recent Activity</h2>
      <div class="p-6 rounded-2xl bg-white/5 backdrop-blur-lg border border-white/10">
        <div class="space-y-6">
          {#each recentActivity as activity}
            <div class="flex items-start gap-4">
              <div class="w-8 h-8 rounded-full bg-white/10 flex items-center justify-center flex-shrink-0">
                {#if activity.type === 'Rental Income'}
                  <span class="text-green-400">💰</span>
                {:else}
                  <span>🏠</span>
                {/if}
              </div>
              <div class="flex-1">
                <div class="flex justify-between items-start">
                  <div>
                    <p class="font-semibold">{activity.type}</p>
                    <p class="text-sm text-gray-400">{activity.property}</p>
                  </div>
                  <div class="text-right">
                    <p class={activity.type === 'Rental Income' ? 'text-green-400 font-semibold' : 'font-semibold'}>
                      {activity.type === 'Rental Income' ? '+' : '-'}{formatCurrency(activity.amount)}
                    </p>
                    <p class="text-sm text-gray-400">{formatDate(activity.date)}</p>
                  </div>
                </div>
              </div>
            </div>
          {/each}
        </div>
      </div>
    </div>
  </div>
</div> 