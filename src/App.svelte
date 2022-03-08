<script>
  import Editor from '@toast-ui/editor';
  import '@toast-ui/editor/dist/toastui-editor.css'; // Editor's Style
  import { onMount } from 'svelte';
  import { download } from './lib/utils.js';
  //import { editorContent } from './lib/stores.js';
  let editorEl;

  onMount(() => {
    const text = () => {
      if (localStorage.getItem('toastContent') === null) return '';
      return JSON.parse(localStorage.getItem('toastContent'));
    };

    const editor = new Editor({
      el: editorEl,
      height: 'auto',
      initialEditType: 'markdown',
      previewStyle: 'vertical',
      initialValue: text(),
      minHeight: '400px',
    });
    editor.moveCursorToEnd(true);
    editor.on('change', () =>
      localStorage.setItem('toastContent', JSON.stringify(editor.getMarkdown()))
    );
  });
</script>

<main>
  <div bind:this={editorEl} />
</main>
<div class="test">
  <button
    on:click={() =>
      download(`file.md`, JSON.parse(localStorage.getItem('toastContent')))}
    >Download as Markdown</button
  >
</div>

<style>
</style>
