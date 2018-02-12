# isa-explorer-demo

Goal: Demonstrate effective display of ISA-Tab data.

We want to try out isa-explorer, https://github.com/ISA-tools/isa-explorer

Plan

1. Find isa-explorer, initial desk check;
2. Get isa-explorer running, example / mock data, on laptop / dev instance;
3. Get isa-explorer running, our real ISA-Tab data, laptop / dev instance;
4. Install on publicly visible instance
5. Install on maintained instance.

Progress

1. Done, looks ok;
2. Done, some fiddling of node versions, etc. Best to proceed by installing nvm first.
3. In progress: Fixed the UTF-8 problem by editing the Investigation file myself. Now we have a problem with optional columns in the study file that are required by the isa-explorer `build_index.py` script. Which I am fixing by editing that script.
4. 2 days? Can we use a static S3 site?
5. 2 days?

