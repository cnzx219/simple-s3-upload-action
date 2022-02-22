# Simple S3 Upload

## FORKED FROM: https://github.com/shallwefootball/upload-s3-action

This action upload directory to AWS S3 by [public read](https://docs.aws.amazon.com/AmazonS3/latest/dev/WebsiteAccessPermissionsReqd.html) with custom destination directory

## Usage

### `workflow.yml` Example

Place in a `.yml` file such as this one in your `.github/workflows` folder. [Refer to the documentation on workflow YAML syntax here.](https://help.github.com/en/articles/workflow-syntax-for-github-actions)

```yaml
name: Upload to S3

on: [pull_request]

jobs:
  upload:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@master
      - uses: cnzx219/simple-s3-upload-action@master
        with:
          AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
          AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY}}
          AWS_S3_REGION: ${{ secrets.AWS_S3_REGION }}
          AWS_S3_BUCKET: ${{ secrets.AWS_S3_BUCKET }}
          SOURCE_DIR: '<directory name>'
          DEST_DIR: '<destination directory name to your S3 bucket>'
```

## Action inputs

The following settings must be passed as environment variables as shown in the example. Sensitive information, especially `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY`, should be [set as encrypted secrets](https://help.github.com/en/articles/virtual-environments-for-github-actions#creating-and-using-secrets-encrypted-variables) — otherwise, they'll be public to anyone browsing your repository's source code

| name                    | description                                                                                                                           |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| `AWS_ACCESS_KEY_ID`            | (Required) Your AWS Access Key. [More info here.](https://docs.aws.amazon.com/general/latest/gr/managing-aws-access-keys.html)        |
| `AWS_SECRET_ACCESS_KEY` | (Required) Your AWS Secret Access Key. [More info here.](https://docs.aws.amazon.com/general/latest/gr/managing-aws-access-keys.html) |
| `AWS_S3_REGION`            | (Required) The region of the bucket you're upload to.                                                                                   |
| `AWS_S3_BUCKET`            | (Required) The name of the bucket you're upload to.                                                                                   |
| `SOURCE_DIR`            | (Required) The local directory you wish to upload to S3.                                                                              |
| `DEST_DIR`              | (Required) The output directory you with to be uploaded in your S3 bucket.                                                            |

## Action outputs

| name               | description                                                                             |
| ------------------ | --------------------------------------------------------------------------------------- |
| `object_locations` | S3 Object Locations                                                                     |
