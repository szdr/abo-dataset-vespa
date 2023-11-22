# abo-dataset-vespa
Vespa Application with Amazon Berkeley Objects (ABO) Dataset

https://amazon-berkeley-objects.s3.amazonaws.com/index.html

* abo-listings.tar
* abo-images-small.tar

# prepare feed data

1. download ABO dataset
2. run preprocess/make_dataset.ipynb
3. run preprocess/make_feed_data.ipynb

# deploy and feed

```
❯ docker run --detach --name vespa --hostname vespa-container \
  --publish 8080:8080 --publish 19071:19071 \
  vespaengine/vespa
```

```
❯ cd vespa-app
❯ vespa deploy --wait 300
```