# Image layer

- Image layer
- union file system
- `history` and `inspect` commands
- Copy on write

## What is image layer?
- Image layers is like git commits. It stores changes of an image
- To show the history of image changes
```
docker image history <image-name:tag>
```
- Each image has many different layers. And the layer on the top is the writable layer, and container state is stored on that top layer. 

## What is layer cache
- When pulling a new image or creating new image, docker will look up in to the installed layer. If the new image's layers have already exist in the local layer cache, then it will use the layer cache. 
- This approach saves a lot of time and space when docker doesn't need to pulling the whole bunch of things from scracth.
- Each layer is identified by SHA
- Layer cache also be use in the Docker Registry. When uploading image or upgrade image, only the new layer will be pushed to registry.

## Sumary
- Image is made up of file system changes and meta data
- Each layer is uniquely identified and only stored once on a host (host can be local or registry as well)
- A container is just a single read/write on the top of image