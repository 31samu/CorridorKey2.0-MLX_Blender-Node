# CorridorKey2.0 Blender Add-On
![my corridorkey logo](images/corridorkey.png)

### important stuff
  
This is a blender add-on integration of [CorridorKey2.0](https://github.com/nikopueringer/CorridorKey2.0) by Niko Pueringer, though not affiliated with them.   
This extension was made using AI, if you want to stay away from anything related to it, I totally understand.

Apple Silicon is supported and tested, using the [MLX port](https://github.com/peterteravskis/corridorkey-v2-mlx) by Peter Teravskis.
[Download](UNZIPME.zip?raw=true)

Windows/Nvidea is experimental and still untested (please test):
[experimental windows/nvidea extension download](experimental/corridorkey_compositor-0.4.3-experimental.zip?raw=true)
->[more information](experimental/README.md)

### specifics

The extension gives you a node in the compositor in which you can plug a video sequence and after an analysis it outputs the keyed result as well as a mask.   
To use it, install the extension, then under the add-on preferences download the backend.  
  
At the moment this officially only works on an apple silicon mac as that is what I’m working with, although it should be pretty easy to swap out the backend for something else, see above for experimental windows/nvidea support.  
I want to improve this a bit further, supporting windows and linux to an extent (although I can’t test that so contribution are welcome) but feel free to take anything and do what you want with it. I only wanted to use this amazing tool (the keyer) in blender, I’m also happy if someone else does a better job.  
  
This repository only hosts the blender add-on framework and workings, the actual key is hosted elsewhere and has to be downloaded separately (the extension can do it for you).  

![preview of the blender compositor node](images/node.webp)

Some notes on the design of the node:

I really want the image input to be inline with the image output but that's not possible for python extension, only for blender internal ones. Similarly the dropdown would maybe be better placed ontop but again same story (I believe).\
The biggest annoyance by far is that extension nodes such as this one don't show up in the list when dragging from a socket and releasing.\