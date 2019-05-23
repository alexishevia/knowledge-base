# s3cmd
AWS S3 Command Line Client
[s3cmd](http://s3tools.org/s3cmd)

## Configure
Will generate a ~/.s3cfg file with access details:
```
s3cmd --configure
```

You can optionally rename ~/.s3cfg and then specify it when running an s3cmd
Example:
```
s3cmd --config=/path/to/config.file ls
```

## List Buckets
```
s3cmd ls
s3cmd ls s3://BucketName
```

## Sync local folder to S3 bucket
```
s3cmd sync /path/to/local/folder/ s3://bucketname --exclude '.git*' --exclude '.DS_Store' --dry-run
```
(remove the --dry-run param when you're sure the command will upload the correct files)

## Create presigned url (GET only)
```
s3cmd signurl s3://BUCKET/OBJECT expiry_epoch

# example:
s3cmd signurl s3://alexishevia/presigntest 1503077374
```

# hosting a site on Amazon S3

Si se está usando Amazon Route 53 como DNS manager y CloudFront como CDN, aquí hay una guía:
[http://www.michaelgallego.fr/blog/2013/08/27/static-website-on-s3-cloudfront-and-route-53-the-right-way/]()

Para hacer deployments a S3, primero instalar s3cmd. Luego correr un comando como: 
```
s3cmd --config=/home/alexishevia/.s3cfg.hevia.alexis sync ./ s3://alexishevia.com --exclude '.git*' --exclude '.DS_Store' --dry-run
```
(quitar el `--dry-run` cuando estemos seguros que el comando va a subir los archivos que queremos)


Asegurarse de setear billing alarms
[https://portal.aws.amazon.com/gp/aws/developer/account/index.html?ie=UTF8&action=billing-alerts&]()

Colocar este policy en los bucket permissions para asegurarse que los archivos puedan ser accedidos:
```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "AddPerm",
      "Effect": "Allow",
      "Principal": { "AWS": "*" },
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::yourBucketName/*"
    }
  ]
}
```

Opcionalmente se puede configurar CloudFront para tener caching y respuestas más rápidas. Ver [esta guía](http://docs.aws.amazon.com/gettingstarted/latest/swh/getting-started-create-cfdist.html)
