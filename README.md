# What is it?
Opinionated declarative utility library for writing dataset classes. Intended for small pytorch experiments.

# Rationale
Pytorch dataset loading often involves certain common tasks:
- Load tensors or values from a filelist
- Truncate sequence/spatial dims to a maximum length
- Drop items that don't satisfy particular requirements
- Pad sequence/spatial dims to a multiple of a number or a maximum per-batch length
- Pad sequence/spatial dims in groups across multiple data fields in a batch
- Or (on training datasets only) randomly subsample sequence/spatial dims to meet a maximum length constraint
- Apply data augmentations
Implementing these tasks is often highly repetitive and error prone.

Dataset loading code can be further simplified by making certain assumptions:
- All data to be loaded takes the form of either a literal or a single file tensor which can be loaded from disk.
- Each dataset class takes only one filelist.
- Filelists contain only paths to tensors or python literals (such as class IDs).
- (?) Tensors are saved in channel-last order. A 1D feature would be of shape `[T, C]`, a 2D feature of shape `[W, H, C]`.