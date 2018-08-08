# nuclias.app

This is a fans app for Nuclias developer.

## Project Initialize

``` bash
$ nvm use stable
$ npm install -g @angular/cli
$ ng new nuclias-app
```

## Startup Local Development Web Server

``` bash
$ cd nuclias-app
$ ng serve --open
```

## Static Site Generator

``` bash
$ cd nuclias-app
$ ng build
```

## Deploy

``` bash
$ cd nuclias-app/dist/nuclias-app/
$ aws s3 sync --profile yihua --acl public-read --exclude .DS_Store . s3://nuclias.app
```

## Deploy only different and new files

## Add Route 53 TXT record

```
$ aws route53 change-resource-record-sets --profile yihua --hosted-zone-id /hostedzone/Z3MC3HGHEJ3T8J \
  --change-batch \
  '{
    "Comment": "Create TXT for Free SSL Certificate Validation",
    "Changes": [
      {
        "Action": "CREATE",
        "ResourceRecordSet": {
          "Name": "_acme-challenge.nuclias.app.",
          "Type": "TXT",
          "TTL": 1,
          "ResourceRecords": [
            {
              "Value": "\"RtZGCr9TJg-n_mUgeQM1_rpjWT-VPduWYLFFYvI2w08\""
            }
          ]
        }
      }
    ]
  }'
```

``` bash
$ aws --profile yihua route53 list-hosted-zones
```

``` bash
$ aws --profile yihua route53 list-resource-record-sets --hosted-zone-id /hostedzone/Z3MC3HGHEJ3T8J
$ aws --profile yihua route53 list-resource-record-sets --hosted-zone-id /hostedzone/Z3B29MHHYI5BO
```

### References

1. [diff to output only the file names](https://stackoverflow.com/questions/6217628/diff-to-output-only-the-file-names)

## Deploy Frontend Static Files

``` bash
$ cd ~/bizcloud/manager/build/nodeapp/build/public
$ aws s3 sync --profile nuclias --acl public-read --exclude .DS_Store . s3://2-0-3.nuclias.app
$ aws s3 sync --profile nuclias --acl public-read --exclude .DS_Store data s3://2-0-3.nuclias.app/data
```

```
$ cd ~/bizcloud/manager/build/nodeapp/build/public
$ aws s3 sync --profile yihua --acl public-read --exclude .DS_Store . s3://nuclias.app
$ aws s3 sync --profile yihua --acl public-read --exclude .DS_Store data s3://nuclias.app/data
```