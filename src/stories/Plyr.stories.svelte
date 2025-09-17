<script module>
	import { defineMeta } from '@storybook/addon-svelte-csf';
	import Plyr from '../lib/Plyr.svelte';
	import '../lib/plyr.css';

	// More on how to set up stories at: https://storybook.js.org/docs/writing-stories
	const { Story } = defineMeta({
		title: 'Media/Plyr',
		component: Plyr,
		tags: ['autodocs'],
		argTypes: {
			type: {
				control: { type: 'select' },
				options: ['video', 'audio']
			},
			provider: {
				control: { type: 'select' },
				options: ['html5', 'youtube', 'vimeo']
			},
			autoplay: { control: 'boolean' },
			controls: { control: 'boolean' },
			loop: { control: 'boolean' },
			muted: { control: 'boolean' },
			preload: {
				control: { type: 'select' },
				options: ['none', 'metadata', 'auto']
			},
			crossorigin: {
				control: { type: 'select' },
				options: [undefined, 'anonymous', 'use-credentials']
			}
		},
		args: {
			type: 'video',
			provider: 'html5',
			autoplay: false,
			controls: true,
			loop: false,
			muted: true,
			preload: 'metadata'
		}
	});
</script>

<!-- HTML5 Video Story -->
<Story
	name="HTML5 Video"
	args={{
		type: 'video',
		provider: 'html5',
		source: {
			type: 'video',
			sources: [
				{
					src: 'http://distribution.bbb3d.renderfarming.net/video/mp4/bbb_sunflower_1080p_60fps_normal.mp4',
					type: 'video/mp4',
					size: 1080
				},
				{
					src: 'http://distribution.bbb3d.renderfarming.net/video/mp4/bbb_sunflower_2160p_60fps_normal.mp4',
					type: 'video/mp4',
					size: 2160
				}
			],
			poster: 'https://cdn.plyr.io/static/demo.jpg',
			tracks: [
				{
					kind: 'captions',
					label: 'English',
					srcLang: 'en',
					src: 'https://cdn.plyr.io/static/demo.vtt',
					default: true
				}
			]
		},
		poster: 'https://cdn.plyr.io/static/demo.jpg',
		muted: true
	}}
/>

<!-- HTML5 Audio Story -->
<Story
	name="HTML5 Audio"
	args={{
		type: 'audio',
		provider: 'html5',
		source: {
			type: 'audio',
			sources: [
				{
					src: 'https://cdn.plyr.io/static/sample.mp3',
					type: 'audio/mp3'
				},
				{
					src: 'https://cdn.plyr.io/static/sample.ogg',
					type: 'audio/ogg'
				}
			]
		}
	}}
/>

<!-- YouTube Video Story -->
<Story
	name="YouTube Video"
	args={{
		type: 'video',
		provider: 'youtube',
		source: {
			type: 'video',
			sources: [
				{
					src: 'YE7VzlLtp-4',
					provider: 'youtube'
				}
			]
		}
	}}
/>

<!-- Vimeo Video Story -->
<Story
	name="Vimeo Video"
	args={{
		type: 'video',
		provider: 'vimeo',
		source: {
			type: 'video',
			sources: [
				{
					src: '1084537',
					provider: 'vimeo'
				}
			]
		}
	}}
/>

<!-- Custom Controls Story -->
<Story
	name="Custom Controls"
	args={{
		type: 'video',
		provider: 'html5',
		source: {
			type: 'video',
			sources: [
				{
					src: 'http://distribution.bbb3d.renderfarming.net/video/mp4/bbb_sunflower_1080p_60fps_normal.mp4',
					type: 'video/mp4'
				}
			]
		},
		options: {
			controls: [
				'play-large',
				'play',
				'progress',
				'current-time',
				'mute',
				'volume',
				'captions',
				'settings',
				'pip',
				'airplay',
				'fullscreen'
			]
		},
		muted: true
	}}
/>

<!-- Autoplay Video Story -->
<Story
	name="Autoplay Video"
	args={{
		type: 'video',
		provider: 'html5',
		source: {
			type: 'video',
			sources: [
				{
					src: 'https://cdn.plyr.io/static/demo.mp4',
					type: 'video/mp4'
				}
			]
		},
		autoplay: true,
		muted: true,
		loop: true
	}}
/>

<!-- Minimal Controls Story -->
<Story
	name="Minimal Controls"
	args={{
		type: 'video',
		provider: 'html5',
		source: {
			type: 'video',
			sources: [
				{
					src: 'http://distribution.bbb3d.renderfarming.net/video/mp4/bbb_sunflower_1080p_60fps_normal.mp4',
					type: 'video/mp4'
				}
			]
		},
		options: {
			controls: ['play', 'progress', 'current-time', 'mute', 'volume']
		},
		muted: true
	}}
/>

<!-- Advanced Options Story -->
<Story
	name="Advanced Options"
	args={{
		type: 'video',
		provider: 'html5',
		source: {
			type: 'video',
			sources: [
				{
					src: 'http://distribution.bbb3d.renderfarming.net/video/mp4/bbb_sunflower_1080p_60fps_normal.mp4',
					type: 'video/mp4'
				}
			]
		},
		options: {
			quality: {
				default: 720,
				options: [4320, 2880, 2160, 1440, 1080, 720, 576, 480, 360, 240]
			},
			speed: {
				selected: 1,
				options: [0.5, 0.75, 1, 1.25, 1.5, 1.75, 2]
			},
			keyboard: {
				focused: true,
				global: false
			},
			tooltips: {
				controls: true,
				seek: true
			}
		},
		muted: true
	}}
/>

<!-- No Source Story -->
<Story
	name="No Source"
	args={{
		type: 'video',
		provider: 'html5'
	}}
/>
