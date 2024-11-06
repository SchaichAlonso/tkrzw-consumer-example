# tkrzw-consumer-example
This project uses vcpkg to provision SchaichAlonso/tkrzw@3653a70a3a8d02d39cb2e087d057e4159ad86f2a and then builds/runs/bundles the examples that are part of the upstream tkrzw project against vcpkg's tkrzw.

Run 
  
    cmake --list-presets

to see a list of implemented presets and then 

  cmake --workflow --preset ${preset}

on an available preset to deploy.
