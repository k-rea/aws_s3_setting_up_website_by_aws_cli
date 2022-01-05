# aws_s3_setting_up_website_by_aws_cli
[AWS CLIを使ってS3をWeb公開](https://siguniang.wordpress.com/2014/03/23/hosting-a-static-website-on-amazon-s3-with-aws-cli/)
```shell
aws s3 mb s3://clitest20220105
aws s3 ls
aws s3 website s3://clitest20220105 --index-document index.html
aws s3api get-bucket-website --bucket clitest20220105
cat policy.json
```

```json
{
  "Version": "2012-10-17",
  "Statement": [{
    "Sid": "PublicReadForGetBucketObjects",
    "Effect": "Allow",
    "Principal": {
      "AWS": "*"
    },
    "Action":["s3:GetObject"],
    "Resource":["arn:aws:s3:::clitest20220105/*"]
  }]
}
```

```shell
aws s3api put-bucket-policy --bucket clitest20220105 --policy fil
```