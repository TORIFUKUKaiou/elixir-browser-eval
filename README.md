# Elixir runs in your browser. No server. No install.

Run Elixir code directly in your browser. No server required. No installation needed.

## Demo

https://elixir-browser-eval.torifuku-kaiou.app/

## What is WebAssembly (Wasm)?

WebAssembly is a compact binary format that runs safely inside modern browsers. It lets non-JavaScript languages run in the browser by compiling them into Wasm modules that execute alongside JavaScript.

```mermaid
flowchart LR
    subgraph Browser
        JS[JavaScript] --> JSE[JS Engine]
        WASM[Wasm Module] --> WR[Wasm Runtime]
    end
    ELX[Elixir/Erlang source] --> BEAM[BEAM bytecode]
    BEAM --> AVM[AtomVM compiled to Wasm]
    AVM --> WR
```

## How it works

```mermaid
flowchart TB
    subgraph Browser
        UI["Textarea + button"]
        JS["Popcorn JS bridge"]
        WASM["AtomVM (Wasm)"]
        AVM["bundle.avm"]
        EVAL["Code.eval_string/3"]
        UI -->|code input| JS
        JS -->|load| AVM
        JS -->|call| WASM
        WASM --> EVAL
        EVAL -->|result| JS
        JS -->|display| UI
    end
```

This project uses:
- **[Popcorn](https://github.com/software-mansion/popcorn)** - A library to run Elixir in browsers via WebAssembly
- **[AtomVM](https://github.com/atomvm/AtomVM)** - A lightweight Erlang VM for microcontrollers and WebAssembly

## Build

This repository contains pre-built artifacts from [Popcorn](https://github.com/software-mansion/popcorn).

```bash
git clone https://github.com/software-mansion/popcorn.git
cd popcorn

# Trust mise configuration (required for cloned repositories)
mise trust

# Install required versions (OTP 26.0.2 and Elixir 1.17.3)
mise install

cd examples/eval_in_wasm
mix deps.get
mix popcorn.cook
```

The `static/` directory is deployed to Cloudflare Pages as-is.

## Credits

- [Popcorn](https://github.com/software-mansion/popcorn) by [Software Mansion](https://swmansion.com/)
- [AtomVM](https://github.com/atomvm/AtomVM)
