# aws-temporary-tokens
Python script for enabling AWS temporary tokens for your CLI commands when MFA is enforced through IAM policies in your AWS account.

You need to have first the following:

1. An AWS user account.
2. An AccessKey and SecretKey already assigned to your user.
3. A JSON File in your home directory named ".aws_temporary_tokens.json".

The content of that file is very simple (for now, who knows in the future):
```
{
        "default": [
                {
                        "arn_device": "None"
                }
        ],
        "other-profile": [
                {
                        "arn_device": "arn:aws:iam::<account>:mfa/<name>"
                }
        ]
}
```

Once you have that, you can just execute the script (Python3):

- python aws-temporary-tokens.py -c 556677
or
- python aws-temporary-tokens.py -c 556677 -p other-profile

This will open a new terminal with these variables attached to it:
* AWS_ACCESS_KEY_ID
* AWS_SECRET_ACCESS_KEY
* AWS_SESSION_TOKEN

Then you will be able to run your aws cli commands as usual.
- aws s3 ls
- etc
