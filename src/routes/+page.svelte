<script lang="ts">
	import Plyr from '$lib/Plyr.svelte';
	import '$lib/plyr.css';
</script>

<Plyr
	source={{
		type: 'video',
		sources: [{ src: 'asZI5dIXoUs', provider: 'youtube' }]
	}}
/>
