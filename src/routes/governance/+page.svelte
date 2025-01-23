<script lang="ts">
  let selectedFilter = "active";

  const stats = [
    { label: "Total Proposals", value: "156" },
    { label: "Active Proposals", value: "8" },
    { label: "Participation Rate", value: "72.4%" },
    { label: "Your Voting Power", value: "2,500 RT" }
  ];

  const proposals = [
    {
      id: "PROP-156",
      title: "Acquire New Property in Austin Tech District",
      description: "Proposal to acquire a 50,000 sq ft office building in Austin's growing tech district for $12.5M.",
      status: "active",
      endDate: "2024-02-15",
      votes: {
        for: 650000,
        against: 125000,
        abstain: 25000
      },
      quorum: 1000000,
      creator: "0x1234...5678",
      createdAt: "2024-01-15"
    },
    {
      id: "PROP-155",
      title: "Implement Dynamic Rental Pricing Model",
      description: "Introduce an AI-driven rental pricing model to optimize property yields based on market conditions.",
      status: "active",
      endDate: "2024-02-10",
      votes: {
        for: 850000,
        against: 75000,
        abstain: 15000
      },
      quorum: 800000,
      creator: "0x9876...4321",
      createdAt: "2024-01-12"
    },
    {
      id: "PROP-154",
      title: "Upgrade Property Management Protocol",
      description: "Upgrade the smart contract system for property management to improve efficiency and reduce costs.",
      status: "passed",
      endDate: "2024-01-05",
      votes: {
        for: 920000,
        against: 180000,
        abstain: 50000
      },
      quorum: 1000000,
      creator: "0x4567...8901",
      createdAt: "2023-12-28"
    },
    {
      id: "PROP-153",
      title: "Expand to European Markets",
      description: "Strategic initiative to expand RealTokens platform to major European cities starting Q2 2024.",
      status: "rejected",
      endDate: "2024-01-01",
      votes: {
        for: 450000,
        against: 750000,
        abstain: 100000
      },
      quorum: 1000000,
      creator: "0x7890...1234",
      createdAt: "2023-12-20"
    }
  ];

  const formatNumber = (num: number) => {
    return new Intl.NumberFormat('en-US').format(num);
  };

  const formatDate = (dateStr: string) => {
    return new Date(dateStr).toLocaleDateString('en-US', {
      month: 'short',
      day: 'numeric',
      year: 'numeric'
    });
  };

  const getStatusColor = (status: string) => {
    switch (status) {
      case 'active':
        return 'bg-blue-500/20 text-blue-400 border-blue-500/50';
      case 'passed':
        return 'bg-green-500/20 text-green-400 border-green-500/50';
      case 'rejected':
        return 'bg-red-500/20 text-red-400 border-red-500/50';
      default:
        return 'bg-gray-500/20 text-gray-400 border-gray-500/50';
    }
  };

  const calculateProgress = (votes: { for: number; against: number; abstain: number }, quorum: number) => {
    const total = votes.for + votes.against + votes.abstain;
    const forPercentage = (votes.for / quorum) * 100;
    const againstPercentage = (votes.against / quorum) * 100;
    const abstainPercentage = (votes.abstain / quorum) * 100;
    const quorumPercentage = (total / quorum) * 100;

    return {
      for: forPercentage,
      against: againstPercentage,
      abstain: abstainPercentage,
      quorum: quorumPercentage
    };
  };

  $: filteredProposals = proposals.filter(p => 
    selectedFilter === 'all' || p.status === selectedFilter
  );
</script>

<svelte:head>
  <title>Governance | EstateChain</title>
</svelte:head>

<div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-12">
  <!-- Header -->
  <div class="mb-12">
    <h1 class="text-4xl font-bold mb-4">Governance</h1>
    <p class="text-gray-400">Participate in shaping the future of RealTokens</p>
  </div>

  <!-- Stats -->
  <div class="grid grid-cols-2 md:grid-cols-4 gap-8 mb-12">
    {#each stats as stat}
      <div class="p-6 rounded-2xl bg-white/5 backdrop-blur-lg border border-white/10">
        <p class="text-gray-400 mb-2">{stat.label}</p>
        <p class="text-3xl font-bold bg-clip-text text-transparent bg-gradient-to-r from-blue-400 to-purple-600">
          {stat.value}
        </p>
      </div>
    {/each}
  </div>

  <!-- Actions -->
  <div class="flex flex-col sm:flex-row justify-between items-start sm:items-center gap-4 mb-8">
    <div class="flex gap-4">
      <button
        class={`px-4 py-2 rounded-lg border transition-all ${selectedFilter === 'all' ? 'bg-white/10 border-white/20' : 'border-white/10'}`}
        on:click={() => selectedFilter = 'all'}
      >
        All
      </button>
      <button
        class={`px-4 py-2 rounded-lg border transition-all ${selectedFilter === 'active' ? 'bg-white/10 border-white/20' : 'border-white/10'}`}
        on:click={() => selectedFilter = 'active'}
      >
        Active
      </button>
      <button
        class={`px-4 py-2 rounded-lg border transition-all ${selectedFilter === 'passed' ? 'bg-white/10 border-white/20' : 'border-white/10'}`}
        on:click={() => selectedFilter = 'passed'}
      >
        Passed
      </button>
      <button
        class={`px-4 py-2 rounded-lg border transition-all ${selectedFilter === 'rejected' ? 'bg-white/10 border-white/20' : 'border-white/10'}`}
        on:click={() => selectedFilter = 'rejected'}
      >
        Rejected
      </button>
    </div>

    <button class="px-6 py-3 rounded-lg bg-gradient-to-r from-blue-500 to-purple-600 hover:from-blue-600 hover:to-purple-700 transition-all font-semibold">
      Create Proposal
    </button>
  </div>

  <!-- Proposals -->
  <div class="space-y-6">
    {#each filteredProposals as proposal}
      <div class="p-6 rounded-2xl bg-white/5 backdrop-blur-lg border border-white/10">
        <div class="flex flex-col md:flex-row justify-between gap-6">
          <div class="flex-1">
            <div class="flex items-start justify-between mb-4">
              <div>
                <h3 class="text-xl font-semibold mb-2">{proposal.title}</h3>
                <p class="text-gray-400 mb-4">{proposal.description}</p>
              </div>
              <span class={`px-3 py-1 rounded-full border ${getStatusColor(proposal.status)} capitalize`}>
                {proposal.status}
              </span>
            </div>

            <div class="grid grid-cols-2 md:grid-cols-4 gap-4 mb-6">
              <div>
                <p class="text-sm text-gray-400">Created by</p>
                <p class="font-mono">{proposal.creator}</p>
              </div>
              <div>
                <p class="text-sm text-gray-400">Created</p>
                <p>{formatDate(proposal.createdAt)}</p>
              </div>
              <div>
                <p class="text-sm text-gray-400">End Date</p>
                <p>{formatDate(proposal.endDate)}</p>
              </div>
              <div>
                <p class="text-sm text-gray-400">ID</p>
                <p>{proposal.id}</p>
              </div>
            </div>

            <!-- Voting Progress -->
            {#if proposal.status === 'active'}
              <div class="space-y-4">
                <div class="flex items-center gap-4">
                  <div class="flex-1">
                    <div class="h-3 rounded-full bg-white/5 overflow-hidden">
                      <div
                        class="h-full bg-gradient-to-r from-green-500 to-green-600"
                        style="width: {calculateProgress(proposal.votes, proposal.quorum).for}%"
                      ></div>
                    </div>
                    <div class="flex justify-between mt-1">
                      <span class="text-sm text-green-400">For: {formatNumber(proposal.votes.for)} RT</span>
                      <span class="text-sm text-gray-400">{calculateProgress(proposal.votes, proposal.quorum).for.toFixed(1)}%</span>
                    </div>
                  </div>

                  <div class="flex-1">
                    <div class="h-3 rounded-full bg-white/5 overflow-hidden">
                      <div
                        class="h-full bg-gradient-to-r from-red-500 to-red-600"
                        style="width: {calculateProgress(proposal.votes, proposal.quorum).against}%"
                      ></div>
                    </div>
                    <div class="flex justify-between mt-1">
                      <span class="text-sm text-red-400">Against: {formatNumber(proposal.votes.against)} RT</span>
                      <span class="text-sm text-gray-400">{calculateProgress(proposal.votes, proposal.quorum).against.toFixed(1)}%</span>
                    </div>
                  </div>

                  <div class="flex-1">
                    <div class="h-3 rounded-full bg-white/5 overflow-hidden">
                      <div
                        class="h-full bg-gradient-to-r from-gray-400 to-gray-500"
                        style="width: {calculateProgress(proposal.votes, proposal.quorum).abstain}%"
                      ></div>
                    </div>
                    <div class="flex justify-between mt-1">
                      <span class="text-sm text-gray-400">Abstain: {formatNumber(proposal.votes.abstain)} RT</span>
                      <span class="text-sm text-gray-400">{calculateProgress(proposal.votes, proposal.quorum).abstain.toFixed(1)}%</span>
                    </div>
                  </div>
                </div>

                <div class="flex items-center gap-4">
                  <div class="flex-1">
                    <p class="text-sm text-gray-400 mb-1">Quorum Progress</p>
                    <div class="h-2 rounded-full bg-white/5 overflow-hidden">
                      <div
                        class="h-full bg-blue-500"
                        style="width: {calculateProgress(proposal.votes, proposal.quorum).quorum}%"
                      ></div>
                    </div>
                  </div>
                  <span class="text-sm text-gray-400">
                    {calculateProgress(proposal.votes, proposal.quorum).quorum.toFixed(1)}%
                  </span>
                </div>

                <div class="flex gap-4 mt-6">
                  <button class="flex-1 px-4 py-2 rounded-lg bg-green-500/20 text-green-400 border border-green-500/50 hover:bg-green-500/30 transition-all">
                    Vote For
                  </button>
                  <button class="flex-1 px-4 py-2 rounded-lg bg-red-500/20 text-red-400 border border-red-500/50 hover:bg-red-500/30 transition-all">
                    Vote Against
                  </button>
                  <button class="flex-1 px-4 py-2 rounded-lg bg-white/5 text-gray-400 border border-white/10 hover:bg-white/10 transition-all">
                    Abstain
                  </button>
                </div>
              </div>
            {:else}
              <div class="space-y-2">
                <div class="flex items-center gap-4">
                  <div class="flex-1">
                    <div class="h-3 rounded-full bg-white/5 overflow-hidden">
                      <div
                        class="h-full bg-gradient-to-r from-green-500 to-green-600"
                        style="width: {calculateProgress(proposal.votes, proposal.quorum).for}%"
                      ></div>
                    </div>
                    <div class="flex justify-between mt-1">
                      <span class="text-sm text-green-400">For: {formatNumber(proposal.votes.for)} RT</span>
                      <span class="text-sm text-gray-400">{calculateProgress(proposal.votes, proposal.quorum).for.toFixed(1)}%</span>
                    </div>
                  </div>

                  <div class="flex-1">
                    <div class="h-3 rounded-full bg-white/5 overflow-hidden">
                      <div
                        class="h-full bg-gradient-to-r from-red-500 to-red-600"
                        style="width: {calculateProgress(proposal.votes, proposal.quorum).against}%"
                      ></div>
                    </div>
                    <div class="flex justify-between mt-1">
                      <span class="text-sm text-red-400">Against: {formatNumber(proposal.votes.against)} RT</span>
                      <span class="text-sm text-gray-400">{calculateProgress(proposal.votes, proposal.quorum).against.toFixed(1)}%</span>
                    </div>
                  </div>
                </div>
              </div>
            {/if}
          </div>
        </div>
      </div>
    {/each}
  </div>
</div> 