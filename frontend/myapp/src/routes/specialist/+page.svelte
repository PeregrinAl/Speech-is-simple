<script>
    import Modal from '$lib/Modal.svelte';
	export let data;

    let showModal = false;
    let patientId = 0;
	const addUser = async() => {
		showModal = true;
		try {
			const response = await fetch('http://localhost:8000/main/addUser', {
				method: 'POST',
				headers: {'Content-Type': 'application/json'},
				credentials: "include",
				body: JSON.stringify({
					patientId
				})
			});
			const content = await response.json();
			if (content.message == "success") {
				// TODO:
			}
			else if (content.message == "already exist")  {
				// TODO:
			}
			else {
				// TODO:
			}
		} 
		
		catch {

		}
  }
  const addScenario = async() => {
	// TODO:
  }
  function handleClick() {
		data.summaries.slice(1);
	}
</script>

<Modal bind:showModal>
	<div>
        <label for="first-name" class="block text-sm font-semibold leading-6 text-gray-900">Введите идентификатор пациента: </label>
        <div class="mt-2.5">
          <input  bind:value={patientId} type="text" name="first-name" id="first-name" autocomplete="given-name" class="block w-full rounded-md border-0 px-3.5 py-2 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6">
        </div>
      </div>
</Modal>
<dev class="grid grid-cols-2 gap-2 m-2">
	<dev class="rounded-md bg-indigo-100">
		<button class="bg-indigo-300 hover:bg-indigo-400 text-white font-bold p-2 m-2 rounded-md font-mono text-xl on:click={addScenario}">Добавить сценарий</button>
	</dev>
	
	<dev class="rounded-md bg-indigo-100">
		<button class="bg-indigo-300 hover:bg-indigo-400 text-white font-bold p-2 m-2 rounded-md font-mono text-xl" on:click={addUser}>Добавить пациента</button>
		<div>
			<ul>
				{#each data.summaries as { first_name, last_name, date_of_birth}}
				<li class="rounded-md bg-white m-2">
					<dev class="grid grid-cols-2 m-2">
						<dev class="rounded-md">
							<p class="m-2 font-mono text-xl py-30 leading-8 text-gray-700">{first_name} {last_name}, {date_of_birth}						
							</p>
						</dev>
						<dev class="rounded-md text-right">
							<button class="m-2">📊</button>
							<button class="m-2">➕</button>
							<button class="m-2" on:click={handleClick}>🗑</button>
						</dev>
					</dev>
			    </li>
				{/each}
			</ul>
		</div>
	</dev>
</dev>