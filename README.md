# Unfold_mobilevit_install
If encounters ValueError: Task image-classification is not compatible with this dataset! Available tasks: [] <br>
edit train.py [159]
```
if args.dataset_name is not None:
    # dataset = load_dataset(args.dataset_name, task="image-classification")
    dataset = load_dataset(args.dataset_name)
else:
    data_files = {}
    if args.train_dir is not None:
        data_files["train"] = os.path.join(args.data_train, "**")
    if args.validation_dir is not None:
        data_files["validation"] = os.path.join(args.data_val, "**")
    dataset = load_dataset(
        "imagefolder",
        data_files=data_files,
        # cache_dir=args.cache_dir,
        # task="image-classification",
    )
```
search ["labels"] and edit:
```
labels = dataset["train"].features["label"].names
```
```
labels = torch.tensor([example["label"] for example in examples])
```
