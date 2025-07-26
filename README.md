# niri-babel-config

This is a learning experiment to use babel to generate the `niri config.kdl` file. There are a number of limitations using KDL that make it difficult to access environment variables, define reusable variables, and use substitutions.

To generate the `niri config.kdl` using each of the Emacs steps:

## GENERATE FILE

1. Open `niri_config.babel`

2. Run `M-x org-babel-execute-buffer`  
   *(This will evaluate all of the code blocks that have been marked for evaluation and display the results just below the code block. To evaluate any code block individually, place the cursor inside the code block and press `C-c C-c`.)*

3. While inside the `niri_config.org` file, run `M-x org-babel-tangle`  
   *(This will produce the `config.kdl` file in the `niri_config` directory.)*

4. Copy `config.kdl` to the `~/.config/niri/` directory.

5. To run steps 1–4 fully automated, run `M-x niri-build-and-deploy`.  
   *(If you want the Lisp code, message me and I’ll send it to you. The live `config.kdl` will be copied to the `niri/` directory. Before overwriting, a backup will be created with the naming convention `config.999`, where `999` is a sequential number. The last 5 backups are kept for rollback purposes.)*

## THEMING

I am using the Archcraft distro which uses **pywal**. Anytime a new theme is generated, it also generates a new `colors.sh` file that is applied to all the basic shell apps (e.g. Waybar, terminal). The `niri_config.org` babel file imports `colors.sh` into a Python dict that substitutes hardcoded color values in the config. This enables automatic color changes when I execute the theme switcher script.

## FINDINGS

Babel is cool and powerful. It’s fun to add a layer of indirection when generating `niri/config.kdl`, but it may be overengineered for this use case. Once your WTM config is optimized for your workflow, there’s rarely a need to change it.

I'll probably forget most of what I’ve learned and revert to editing `niri/config.kdl` manually.

That said, mixing languages in Org Babel is a big plus. I used Python since it's easier for me to read than Lisp. Generating the `config.kdl` takes ~15 seconds with Python (about half that using Lisp).

### BENFITS:

1. Creation and reusability of variables.
2. Programmatic control – you can do nearly anything.
3. Debug output preview – see exactly what will be tangled before it’s written to file.
4. Use of external files and environment variables (e.g. importing `colors.sh`).
