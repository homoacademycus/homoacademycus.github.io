---
{"layout": "post", "categories": "TroubleShooting", "title": "nodejs segmentationFault", "feature-img": "assets/img/feature_img.png"}
---
Segmentation fault (core dumped)

segmentation fault occurs when a program attempts to access a memory location that it is not allowed to access, or attempts to access a memory location in a way that is not allowed 

The rules that you can break to cause this include things like reading or writing to an invalid memory address (e.g. native code somewhere trying to use a null pointer as a memory address), causing a stack or buffer overflow, or reading or writing from memory that's not yours (maybe it was yours but it's now been released, maybe it's unused, or maybe it's owned by another process or the operating system).


Rebuild all your native node modules with npm rebuild. This will recompile native code with your current version of node, and should resolve any issues where your native modules are compiled for the wrong node version.

Find all the native modules you have installed, by searching your node_modules folder for .node files. On Linux/Mac you can list them with:

find node_modules -iname "*.node"


