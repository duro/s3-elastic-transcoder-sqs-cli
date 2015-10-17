# S3 -> ELTC -> SQS

```
processFile [file] <options>

Options:
  -c, --config    Config JS File to use. This will ignore all other config args
                  . If this is not provided, and there is no .config.js in your
                  current working directory, all other options are required
  -k, --key       S3 API Key
  -s, --secret    S3 API Secret
  -b, --bucket    S3 Bucket
  -r, --region    AWS Region
  -p, --prefix    S3 File Key Prefix (Path)
  -q, --queue     SQS Url
  -i, --pipeline  The Elastic Transcoder pipeline ID
```

This simple example script shows how to move a file from disk up to S3, trigger an Elastic Transcoder job, and wait for the job to be complete by listening to an SQS queue.

You can run the configure the script via the CLI arguments, or by placing a config file named `.config.js` in your current working directory.

The format of that config file looks like this:

```
module.exports = {
  accessKey: '...',
  accessSecret: '...',
  region: '...',
  bucket: '...',
  prefixPath: '...',
  queueUrl: '...',
  pipelineId: '...'
}
```

In order for this to work, you must have an S3 bucket created, an Elastic Transcoder pipeline created, have it configured to send notifications to SNS, and and SQS queue setup as a subscriber to the SNS topic.

Consult the AWS docs for doing the above.
