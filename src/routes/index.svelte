<script context="module">
  import { parseISO, format } from 'date-fns'
  export async function load({fetch}) {
    const url = `${import.meta.env.VITE_FACTS_URL}/facts`;
    const response = await fetch(url);
    const data = response.ok && await response.json();
    const facts = data
      .map((f) => ({...f, CreatedAt: format(parseISO(f.CreatedAt), 'do MMM, yyyy')}))
      .sort((a, b) => b.Number - a.Number);

    return {
      status: response.status,
      props: {
        facts
      }
    };
  }
</script>

<script>
  export let facts;
</script>

<div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
  <div class="bg-white pt-16 pb-20 px-4 sm:px-6 lg:pt-24 lg:pb-28 lg:px-8">
    <div class="relative max-w-lg mx-auto divide-y-2 divide-gray-200 lg:max-w-7xl">
      <div>
        <h2 class="text-3xl tracking-tight font-extrabold text-gray-900 sm:text-4xl">Peter's facts</h2>
        <div class="mt-3 sm:mt-4 lg:grid lg:grid-cols-1 lg:gap-5 lg:items-center">
          <p class="text-xl text-gray-500">Just a collection of small little snippets of wisdom, all information of this website shall be treated as completely true and empirically proven if applicable</p>
        </div>
      </div>
      <div class="mt-6 pt-10 grid gap-16 lg:grid-cols-2 lg:gap-x-5 lg:gap-y-12">

      {#each facts as { ID, Number, Content, CreatedAt }}
        <div>
          <p class="text-sm text-gray-500">
            <time datetime="2020-03-16">{CreatedAt}</time>
          </p>
          <a href="/{ID}" class="mt-2 block">
            <p class="text-xl font-semibold">
              <span class="text-gray-900">Fact number </span><span class="text-indigo-600">{Number}</span>
            </p>
          </a>
          <p class="mt-3 text-base text-gray-500">{Content}</p>
        </div>
      {/each}
      </div>
    </div>
  </div>
</div>
