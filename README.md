# Template for Neovim Plugins in Rust

Template for [ModProg/nvim-rust](https://github.com/ModProg/nvim-rust)

## Use with `cargo-hatch`
1. Install `cargo install cargo-hatch`
2. Use template `cargo hatch git https://github.com/ModProg/nvim-rust-hatch`

## Build and test with `cargo-make`
1. Install `cargo install cargo-make`

### Build the plugin
1. `makers release`
2. Copy `lua/*` to `lua` in the [nvim config directory](https://neovim.io/doc/user/starting.html#base-directories)
3. Add `require"{{ module_name }}".setup()` to your `init.lua`

### Run it directly
1. `makers run`
2. Adjust invocation of plugin in `Makefile.toml`:
```sh
exec nvim --cmd "set runtimepath+=." "+lua require'${module_name}'.hello()"
```

## Installation of finished plugin
### `packer.nvim`
depends on `cargo-make`:

```lua
use {
    'ModProg/rust-nvim-template', 
    run = 'makers release',
    config = function()
        require"{{ module_name }}".setup()
    end
}
```

### Manually

1. Compile the code with `cargo build --release`
2. Copy `target/release/lib{{ project_name | replace(from="-", to="_") }}.so` to your nvim directory `lua/{{ module_name }}.so`
3. Add `require"{{ module_name }}".setup()` to your nvim initialization (i.e. `init.lua`)
