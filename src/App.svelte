<script lang="ts">
  import { compress } from "../pkg/wasm_flate.js";

  let data: Uint8Array | null = null;
  let file_name: string | null = null;

  function read(event: Event) {
    if (!event.target) {
      return;
    }
    if (!(event.target instanceof HTMLInputElement)) {
      return;
    }
    const file = event.target.files![0];
    const reader = new FileReader();
    reader.onload = (e) => {
      const buffer = e.target!.result as ArrayBuffer;
      data = new Uint8Array(buffer);
      file_name = file.name;
    };
    reader.readAsArrayBuffer(file);
  }

  function download(name: string, data: Uint8Array) {
    const blob = new Blob([data], {
      type: "application/octet-stream",
    });
    const url = URL.createObjectURL(blob);
    const a = document.createElement("a");
    a.href = url;
    a.download = name;
    a.click();
  }

  function compress_and_download() {
    if (!data || !file_name) {
      return;
    }
    const compressed_data = compress(data);
    download(file_name + ".gz", compressed_data);
  }
</script>

<main>
  <div class="main">
    <h1>Compress Files</h1>
    <label for="file">File to Compress</label>
    <div class="upload">
      <input type="file" on:change={read} />
    </div>

    <div>
      <button on:click={compress_and_download} disabled={!data}>
        Download Compressed File
      </button>
    </div>
  </div>
</main>
