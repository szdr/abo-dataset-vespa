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

run docker

```
❯ docker run --detach --name vespa --hostname vespa-container \
  --publish 8080:8080 --publish 19071:19071 \
  vespaengine/vespa
```

deploy vespa application

```
❯ cd vespa-app
❯ vespa deploy --wait 300
```

feed

```
❯ vespa feed output/feed.jsonl
```

query

```
❯ vespa query "select * from item where userQuery()" "query=item_name_en_us:'usb+wall+charger'" "type=all"
{
    "root": {
        "id": "toplevel",
        "relevance": 1.0,
        "fields": {
            "totalCount": 13
        },
        "coverage": {
            "coverage": 100,
            "documents": 20355,
            "full": true,
            "nodes": 1,
            "results": 1,
            "resultsFull": 1
        },
        "children": [
            {
                "id": "id:item:item::B0773JY6T2",
                "relevance": 0.20949854698488654,
                "source": "item",
                "fields": {
                    "sddocname": "item",
                    "documentid": "id:item:item::B0773JY6T2",
                    "item_id": "B0773JY6T2",
                    "item_name_en_us": "AmazonBasics 40W 4-Port USB Wall Charger - White",
                    "path": "b8/b8154df7.jpg"
                }
            },
...
```