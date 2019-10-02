# ImageNet to S3

Script to download the Imagenet dataset and upload to s3. Derrived from [imagenet_to_gcs.py](https://github.com/tensorflow/tpu/blob/master/tools/datasets/imagenet_to_gcs.py).

To run the script setup a virtualenv with the following libraries installed.
- `boto3`: Install with `pip install boto3`
- `tensorflow`: Install with `pip install tensorflow`
-  `awscli`: Install with `pip install awscli`

```
sudo yum install python3-pip.noarch
sudo pip3 install -U virtualenv
virtualenv --system-site-packages -p python3 ./venv
source ./venv/bin/activate bash
pip install --upgrade pip
pip list
pip install --upgrade tensorflow boto3 awscli
```

Then configure your AWS credentials

```
aws --configure
```

Once you have all the above libraries setup, you should register on the
[Imagenet website](http://image-net.org/download-images) to get your
username and access_key.

Make sure you have around 300GB of disc space available on the machine where
you're running this script. You can run the script using the following command.

```
python imagenet_to_s3.py \
  --s3_output_path="s3://TEST_BUCKET/IMAGENET_DIR" \
  --local_scratch_dir="./imagenet" \
  --imagenet_username=FILL_ME_IN \
  --imagenet_access_key=FILL_ME_IN \
```

Optionally if the raw data has already been downloaded you can provide a direct
`--raw_data_dir` path. If raw data directory is provided it should be in
the format:
- Training images: train/n03062245/n03062245_4620.JPEG
- Validation Images: validation/ILSVRC2012_val_00000001.JPEG
- Validation Labels: synset_labels.txt

# Training

To use TensorFlow to train against your newly created imagenet dataset in S3, you'll
want to follow the [s3 deployment](https://github.com/tensorflow/examples/blob/master/community/en/docs/deploy/s3.md) examples from the TensorFlow docs.
