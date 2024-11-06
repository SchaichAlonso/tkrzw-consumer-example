# tkrzw-consumer-example
This project uses vcpkg to provision [tkrzw](https://github.com/estraier/tkrzw) and then builds/runs/bundles the examples that are part of the upstream tkrzw project against the vcpkg deployed tkrzw.

Run 
  
    cmake --list-presets

to see a list of implemented presets and then 

  cmake --workflow --preset ${preset}

on an available preset to deploy.
