<script>
  import { onMount } from "svelte";
  import { DataSet, Network } from "vis-network/standalone";

  let container;

  onMount(() => {
    const nodes = [];
    const edges = [];

    for (let i = 0; i <= 200; i++) {
      const x = i - 10;
      const y = Math.sin(x);

      nodes.push({
        id: i,
        label: `x:${x}`,
        x: x * 100,
        y: -y * 200,
        fixed: true,
        color: "#3b82f6",
      });

      if (i > 0) {
        edges.push({ from: i - 1, to: i, color: "#64748b" });
      }
    }

    const data = { nodes: new DataSet(nodes), edges: new DataSet(edges) };
    const options = {
      physics: false,
      interaction: { dragNodes: false, zoomView: true },
    };

    new Network(container, data, options);
  });
</script>

<main class="min-h-screen bg-slate-100 flex flex-col items-center p-10">
  <div class="max-w-4xl w-full bg-white rounded-2xl shadow-2xl overflow-hidden">
    <div class="bg-blue-600 p-4 text-white text-center">
      <h1 class="text-xl font-bold">Vizualizare Funcție: f(x) = sin(x)</h1>
    </div>
    <div bind:this={container} class="w-full bg-white"></div>
  </div>
</main>
