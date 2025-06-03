	
<script lang="ts">
    import { Skeleton } from "$lib/components/ui/skeleton/index.js";

    import * as Card from "$lib/components/ui/card/index.js";
    import * as Carousel from "$lib/components/ui/carousel/index.js";
    import type { CarouselAPI } from "$lib/components/ui/carousel/context.js";
   
    let api = $state<CarouselAPI>();
   
    const count = $derived(api ? api.scrollSnapList().length : 0);
    let current = $state(0);
   
    $effect(() => {
      if (api) {
        current = api.selectedScrollSnap() + 1;
        api.on("select", () => {
          current = api!.selectedScrollSnap() + 1;
        });
      }
    });
</script>
   
  <Carousel.Root
    setApi={(emblaApi) => (api = emblaApi)}
    class="w-full max-w-xs"
  >
    <Carousel.Content>
      {#each Array(5) as _, i (i)}
        <Carousel.Item>
          <Card.Root>
            <Card.Content
              class="flex flex-col items-center justify-center"
            >
            <div class="flex items-center space-x-4">
                <Skeleton class="size-12 rounded-full" />
                <div class="space-y-2">
                  <Skeleton class="h-4 w-[250px]" />
                  <Skeleton class="h-4 w-[200px]" />
                </div>
              </div>
              <div>
                Messages go here!
              </div>
            </Card.Content>
          </Card.Root>
        </Carousel.Item>
      {/each}
    </Carousel.Content>
    <Carousel.Previous />
    <Carousel.Next />
  </Carousel.Root>
  <div class="text-muted-foreground py-2 text-center text-sm">
    Slide {current} of {count}
  </div>
  
  
  
