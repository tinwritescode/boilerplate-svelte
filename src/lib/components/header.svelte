<script lang="ts">
	import AppButton from './appButton.svelte';

	import { page } from '$app/stores';
	import { authStore } from '$lib/store/auth/auth.store';

	$: currentPage = $page.url.pathname;

	let isLoggedIn: boolean;
	authStore.user.subscribe((user) => {
		isLoggedIn = !!user;
	});
</script>

<header class="flex gap-2 justify-between items-center mt-4">
	<a href="/" class="text-2xl font-bold text-gray-800"> HCMUS-Bank Admin </a>

	{#if isLoggedIn}
		<AppButton on:click={authStore.logout}>Logout</AppButton>
	{:else}
		<!-- Router is /login -->
		{#if currentPage === '/login'}
			<AppButton>
				<a href="/register">Register</a>
			</AppButton>
		{:else}
			<AppButton>
				<a href="/login">Login</a>
			</AppButton>
		{/if}
	{/if}
</header>
