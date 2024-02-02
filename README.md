# wasmzip

Vite app that compresses a file directly in the browser using WebAssembly.

## Running Locally

1. Install language frameworks:

   - [Rust](https://www.rust-lang.org/)
   - [Node.js](https://nodejs.org/)
   - [npm](https://www.npmjs.com/)

1. Clone the repo, and install the dependencies:

   ```sh
   git clone git@github.com:shadanan/wasmzip.git
   npm install
   cargo install wasm-pack
   ```

1. Compile the WebAssembly binary:

   ```sh
   wasm-pack build
   ```

1. Run the development server:

   ```sh
   npm run dev
   ```
