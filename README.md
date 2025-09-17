# plyr-sv

A Svelte 5 wrapper for [Plyr](https://plyr.io/) - A simple, accessible, and customizable HTML5, YouTube, and Vimeo media player, with Svelte 5 reactiveness.

## Installation

```sh
pnpm install plyr-sv
```

## Usage

### Basic Usage

```svelte
<script>
	import { Plyr } from 'plyr-sv';
	import 'plyr-sv/css'; // Import Plyr styles

	const source = {
		type: 'video',
		sources: [
			{
				src: 'https://cdn.plyr.io/static/demo.mp4',
				type: 'video/mp4'
			}
		]
	};
</script>

<Plyr {source} />
```

### With Options

```svelte
<script>
	import { Plyr } from 'plyr-sv';
	import 'plyr-sv/css';

	const source = {
		type: 'video',
		sources: [
			{
				src: 'https://cdn.plyr.io/static/demo.mp4',
				type: 'video/mp4'
			}
		]
	};

	const options = {
		controls: ['play', 'progress', 'current-time', 'mute', 'volume', 'fullscreen'],
		autoplay: false,
		muted: true
	};
</script>

<Plyr {source} {options} />
```

### YouTube and Vimeo Support

```svelte
<script>
	import { Plyr } from 'plyr-sv';
	import 'plyr-sv/css';

	const youtubeSource = {
		type: 'video',
		sources: [
			{
				src: 'VIDEO_ID',
				provider: 'youtube'
			}
		]
	};

	const vimeoSource = {
		type: 'video',
		sources: [
			{
				src: 'VIDEO_ID',
				provider: 'vimeo'
			}
		]
	};
</script>

<Plyr source={youtubeSource} />
<Plyr source={vimeoSource} />
```

## CSS Import Options

### Option 1: Import from the package (recommended)

```javascript
import 'plyr-sv/css';
```

### Option 2: Direct import from Plyr

```javascript
import 'plyr/dist/plyr.css';
```

## Props

| Prop                            | Type                  | Description                    |
| ------------------------------- | --------------------- | ------------------------------ |
| `source`                        | `SourceInfo`          | Media source configuration     |
| `options`                       | `Options`             | Plyr configuration options     |
| All HTML video/audio attributes | `HTMLVideoAttributes` | Standard HTML media attributes |

## Types

The package exports several TypeScript types:

```typescript
import type { PlyrInstance, PlyrOptions, PlyrSource } from 'plyr-sv';
```

## Reactive Props

The component is fully reactive and will update when `source` or `options` props change:

```svelte
<script>
  let source = $state({ ... });
  let options = $state({ ... });

  function updateSource() {
    source = { /* new source */ };
  }
</script>

<Plyr {source} {options} />
<button on:click={updateSource}>Change Source</button>
```

## Development

```sh
# Install dependencies
bun install

# Start development server
bun run dev

# Run Storybook
bun run storybook

# Build library
bun run build

# Run tests
bun test
```

## License

MIT
