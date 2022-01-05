# aws_s3_setting_up_website_by_aws_cli
[AWS CLIを使ってS3をWeb公開](https://siguniang.wordpress.com/2014/03/23/hosting-a-static-website-on-amazon-s3-with-aws-cli/)
```shell
aws s3 mb s3://clitest20220105
aws s3 ls
aws s3 website s3://clitest20220105 --index-document index.html
aws s3api get-bucket-website --bucket clitest20220105
cat policy.json
```
## ポリシー(全許可)
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

## ポリシー(IP制限)
```json
{
  "Id": "SourceIP",
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "SourceIP",
      "Action": "s3:*",
      "Effect": "Allow",
      "Resource": [
        "arn:aws:s3:::clitest20220105",
        "arn:aws:s3:::clitest20220105/*"
      ],
      "Condition": {
        "IpAddress": {
          "aws:SourceIp": [
            "210.161.24.31/32",
            "113.149.140.161/32"
          ]
        }
      },
      "Principal": "*"
    }
  ]
}
```


```shell
aws s3api put-bucket-policy --bucket clitest20220105 --policy file://policy.json
aws s3api get-bucket-policy --bucket clitest20220105 
```

- create index.html file for test

```shell
aws s3 cp index.html s3://clitest20220105/index.html
```

## Test your website
```shell
http https://clitest20220105.s3.ap-northeast-1.amazonaws.com/
```