<script lang="ts">
	interface Activity {
		name: string;
	}

	let activities: Activity[] = [];

	const handleSubmit = (event: SubmitEvent) => {
		const formData = new FormData(event.target as HTMLFormElement);
		const name = formData.get('activity-name') as string;

		activities = [...activities, {name}];
	};

  $: count = activities.length;
</script>

<form on:submit={handleSubmit}>
	<label for="activity-name">Activity: </label>
	<input type="text" id="activity-name" name="activity-name" /><br />
	<input type="submit" value="Submit" />
</form>

<h2>Activities</h2>
<p>You have {count} activities</p>
{#if activities.length}
	<ul>
		{#each activities as activity}
			<li>{activity.name}</li>
		{/each}
	</ul>
{:else}
	<p>No activities yet</p>
{/if}
