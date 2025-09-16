<script lang="ts" module>
	import * as PlyrJS from 'plyr';

	// Export types for external use
	export type PlyrInstance = PlyrJS.default;
	export type PlyrOptions = PlyrJS.Options;
	export type PlyrSource = PlyrJS.SourceInfo;
</script>

<script lang="ts">
	import { onMount, onDestroy, untrack } from 'svelte';
	import type { HTMLVideoAttributes } from 'svelte/elements';

	interface Props extends HTMLVideoAttributes {
		source?: PlyrJS.SourceInfo;
		options?: PlyrJS.Options;
	}

	const { source, options, ...rest }: Props = $props();

	let mediaElement = $state<HTMLVideoElement | HTMLAudioElement | null>(null);
	let player: PlyrJS.default | null = $state(null);

	// Initialize Plyr instance
	onMount(() => {
		// Ensure media element is available before initializing Plyr
		if (!mediaElement) {
			throw new Error('Media element not found. Make sure to provide proper source prop.');
		}

		if (!player) {
			player = new PlyrJS.default(mediaElement, options ?? {});
			if (source) {
				player.source = source;
			}
		}
	});

	// Cleanup on destroy
	onDestroy(() => {
		if (player) {
			player.destroy();
			player = null;
		}
	});

	// Function to get the player instance
	export function getPlayer(): PlyrJS.default | null {
		return player;
	}

	// Reactive updates for source
	$effect(() => {
		const untrackedPlayer = untrack(() => player);
		if (untrackedPlayer && source) {
			untrackedPlayer.source = source;
		}
	});

	// Reactive updates for options
	$effect(() => {
		const untrackedPlayer = untrack(() => player);
		if (untrackedPlayer && options && mediaElement) {
			// Store current source before recreating player
			const currentSource = untrackedPlayer.source;
			const currentTime = untrackedPlayer.currentTime;
			const paused = untrackedPlayer.paused;

			// Destroy current player
			untrackedPlayer.destroy();

			// Create new player with updated options
			player = new PlyrJS.default(mediaElement, options);

			// Restore source if it exists
			if (currentSource) {
				player.source = currentSource;
			}

			// Restore playback state
			if (currentTime > 0 && player) {
				player.once('ready', () => {
					if (player) {
						player.currentTime = currentTime;
						if (!paused) {
							player.play();
						}
					}
				});
			}
		}
	});
</script>

{#if source?.type === 'audio'}
	<audio bind:this={mediaElement} {...rest as any}></audio>
{:else}
	<video bind:this={mediaElement} {...rest as any}></video>
{/if}
