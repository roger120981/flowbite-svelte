<script lang="ts">
  import { onMount } from "svelte";
  import { page, navigating } from "$app/state";
  interface WindowWithCarbonAds extends Window {
    _carbonads: {
      refresh: () => void;
    };
  }

  onMount(() => {
    // refreshCarbonAds();
  });

  $effect(() => {
    if (navigating.complete) {
      refreshCarbonAds();
    }
  });

  function refreshCarbonAds() {
    const isCarbonAdsRendered = document.querySelector("#carbonads");

    if (isCarbonAdsRendered) {
      (window as unknown as WindowWithCarbonAds)._carbonads.refresh();
    } else {
      const script = document.createElement("script");
      script.async = true;
      script.id = "_carbonads_js";
      script.src = "//cdn.carbonads.com/carbon.js?serve=CEAIC53I&placement=flowbite-sveltecom";

      const container = document.querySelector("#carbon-container");
      if (container) {
        container.appendChild(script);
      }
    }
  }
</script>

<aside class="fixed right-5 bottom-5 z-50 hidden sm:block">
  <div id="carbon-container"></div>
</aside>
