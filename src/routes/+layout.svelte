<script>
	import { Toaster, toast } from 'svelte-sonner';
	import '../app.css';

	let { children } = $props();
</script>

{@render children()}

<Toaster
	toastOptions={{
		unstyled: true,
		classes: {
			toast: 'rounded-box p-4 shadow-lg text-base-content bg-base-200 flex items-center gap-3',
			title: 'font-bold text-base-content',
			description: 'text-base-content',
			actionButton: 'bg-primary text-primary-content px-3 py-1 rounded',
			cancelButton: 'bg-secondary text-secondary-content px-3 py-1 rounded',
			closeButton: 'text-error',
			error: 'bg-error text-error-content',
			success: 'bg-success text-success-content',
			warning: 'bg-warning text-warning-content',
			info: 'bg-info text-info-content'
		}
	}}
/>
