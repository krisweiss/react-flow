<script lang="ts">
  import { getRectOfNodes } from '@xyflow/system';

  import { useStore } from '$lib/store';
  import { Selection } from '$lib/components/Selection';
  import drag from '$lib/actions/drag';

  const store = useStore();
  const { selectionRectMode, nodes } = store;

  $: selectedNodes = $nodes.filter((n) => n.selected);
  $: rect = getRectOfNodes(selectedNodes);
</script>

{#if selectedNodes && $selectionRectMode === 'nodes'}
  <div
    class="selection-wrapper nopan"
    style="width: {rect.width}px; height: {rect.height}px; transform: translate({rect.x}px, {rect.y}px)"
    use:drag={{ disabled: false, store }}
  >
    <Selection width="100%" height="100%" x={0} y={0} />
  </div>
{/if}

<style>
  .selection-wrapper {
    position: absolute;
    top: 0;
    left: 0;
    z-index: 7;
    pointer-events: all;
  }
</style>
