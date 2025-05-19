<script>
	import { Clipboard } from '@lucide/svelte';
	import { onMount } from 'svelte';
	import { Toaster, toast } from 'svelte-sonner';

	let ipinfo;

	async function getIp() {
		const response = await fetch('https://ipwho.is/');
		const data = await response.json();
		ipinfo = data;
	}

	function copyIP() {
		navigator.clipboard.writeText(ipinfo?.ip);
		toast('IP Copied to clipboard');
	}

	onMount(() => {
		getIp();
	});
</script>

<svelte:head>
	<title>IP: {ipinfo?.ip}</title>
</svelte:head>

{#if ipinfo}
	<div class="mt-10 flex flex-col items-center">
		<div class="card bg-base-200 w-full max-w-2xl shadow-xl">
			<div class="card-body items-center text-center">
				<div class="flex items-center space-x-4">
					<img src={ipinfo?.flag?.img} alt={ipinfo?.country} class="h-10 rounded-sm" />
					<h2 class="card-title text-2xl">{ipinfo?.country}</h2>
				</div>
				<div class="mt-4">
					<p class="text-primary text-4xl font-bold">
						{ipinfo?.ip}
						<button class="" on:click={copyIP} title="Copy IP">
							<Clipboard class="h-5 w-5" />
						</button>
					</p>
				</div>
				<div class="mt-6 grid w-full grid-cols-1 gap-4 text-left md:grid-cols-2">
					<p><strong>City:</strong> {ipinfo?.city}</p>
					<p><strong>Region:</strong> {ipinfo?.region}</p>
					<p><strong>Postal Code:</strong> {ipinfo?.postal}</p>
					<p><strong>Capital:</strong> {ipinfo?.capital}</p>
					<p><strong>Borders:</strong> {ipinfo?.borders}</p>
					<p><strong>ISP:</strong> {ipinfo?.connection?.isp}</p>
					<p><strong>Timezone:</strong> {ipinfo?.timezone?.abbr}</p>
					<p><strong>Timezone ID:</strong> {ipinfo?.timezone?.id}</p>
				</div>
			</div>
		</div>
		<a href="https://parcoil.com" class="text-base-content/50 mt-5 text-sm hover:underline">
			Go back to parcoil.com
		</a>
	</div>
{:else}
	<div class="flex h-screen flex-col items-center justify-center text-center">
		<span class="loading loading-ring font-3xl w-[70px]"></span>
		<a href="https://parcoil.com" class="text-base-content/50 mt-5 text-sm hover:underline">
			Go back to parcoil.com
		</a>
	</div>
{/if}
