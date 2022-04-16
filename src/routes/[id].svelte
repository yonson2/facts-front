<script context="module">
  import { parseISO, format } from 'date-fns'
  export async function load({fetch, params}) {
    const url = `${import.meta.env.VITE_FACTS_URL}/facts/${params.id}`;
    const response = await fetch(url);
    const data = response.ok && await response.json();
    const fact = {...data, CreatedAt: format(parseISO(data.CreatedAt), 'do MMM, yyyy')}

    return {
      status: response.status,
      props: {
        fact
      }
    };
  }
</script>

<script>
  export let fact;
</script>

<div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
  <div class="relative py-16 bg-white overflow-hidden">
    <div class="relative px-4 sm:px-6 lg:px-8">
      <div class="text-lg max-w-prose mx-auto">
        <h1>
          <span class="block text-base text-center text-indigo-600 font-semibold tracking-wide uppercase">Introducing</span>
          <span class="mt-2 block text-3xl text-center leading-8 font-extrabold tracking-tight text-gray-900 sm:text-4xl">Fact number {fact.Number}</span>
        </h1>
        <p class="mt-8 text-xl text-gray-500 leading-8">{fact.Content}</p>
      </div>
    </div>
  </div>
</div>
