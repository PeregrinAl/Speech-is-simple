<script>
	export let showModal; // boolean

	let dialog; // HTMLDialogElement

	$: if (dialog && showModal) dialog.showModal();
</script>

<!-- svelte-ignore a11y-click-events-have-key-events a11y-no-noninteractive-element-interactions -->
<dialog
	bind:this={dialog}
	on:close={() => (showModal = false)}
	on:click|self={() => dialog.close()}
>
	<!-- svelte-ignore a11y-no-static-element-interactions -->
	<div on:click|stopPropagation>
		<slot name="header" />
		<slot />
		<!-- svelte-ignore a11y-autofocus -->
        <div class="spaceBetween">
		<button class="bg-indigo-300 hover:bg-indigo-400 text-white font-bold p-2 my-2 rounded-md font-mono" autofocus on:click={() => dialog.close()}>Закрыть</button>
        <button class="bg-indigo-300 hover:bg-indigo-400 text-white font-bold p-2 my-2 rounded-md font-mono" on:click={() => dialog.close()}>Добавить</button>
    </div>
	</div>
</dialog>

<style>
    
	dialog {
		max-width: 40em;
		border-radius: 0.2em;
		border: none;
	}
	dialog > div {
		padding: 1em;
	}
	dialog[open] {
		animation: zoom 0.3s cubic-bezier(0.34, 1.56, 0.64, 1);
	}
	@keyframes zoom {
		from {
			transform: scale(0.95);
		}
		to {
			transform: scale(1);
		}
	}
	dialog[open]::backdrop {
		animation: fade 0.2s ease-out;
	}
	@keyframes fade {
		from {
			opacity: 0;
		}
		to {
			opacity: 1;
		}
	}
    .spaceBetween {
        display: flex;
        justify-content: space-between;
    }
</style>