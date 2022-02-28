# Path 
All programs running on the terminal are stored somewhere on the filesystem. For bash to know where to look for these programs, it checks the `PATH` variable. The `PATH` environment variable contains paths separated by a `:` e.g: `my/path:my/other/path`. To see which directories are added to path one can run `echo $PATH`. 

## .bashrc 
Each time bash starts it checks and executes the `.bashrc` file, a file located at the home directory of the user. This file is responsible for setting up bash. Here one can add environment variables using the `export` command. 

## Exporting path in bash

1. Add path to export at the end of `.bashrc` in your home directory
    ```bash
    export PATH = "/my/path/:$PATH"
    ```
2. Save and reload the `.bashrc`
    ```bash
    source ~/.bashrc
    ```
3. Verify that the path was added 
    ```bash
    echo $PATH
    ```
