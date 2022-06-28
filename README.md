# aws-temporary-tokens
Python script for enabling AWS temporary tokens for your CLI commands when MFA is enforced through IAM policies in your AWS account.

You need to have first the following:

1. Python **3.7** or **newer**
2. An AWS user account.
3. An **AccessKey** and **SecretKey** already assigned to your user.
4. The arn of the [assigned MFA device](https://us-east-1.console.aws.amazon.com/iam/home#/security_credentials).
4. Confirm that your default output is json in your **~/.aws/config** file. Example:
```
    [profile my_second_profile]
    region = us-east-2
    output = json
```
5. A JSON file in your home directory named **".aws_temporary_tokens.json"** if you have different AWS profiles and/or don't want to pass the arn of the MFA device everytime.

The content of that file is very simple (for now, who knows in the future). You need to have an entry for each profile defined 
in your **~/.aws/credentials** file. Also, the name of the profiles **must match in both files**:
```
{
        "default": [
                {
                        "arn_device": "arn:aws:iam::<account>:mfa/<name>"
                }
        ],
        "my_second_profile": [
                {
                        "arn_device": "arn:aws:iam::<account>:mfa/<name>"
                }
        ],
        "my_third_profile": [
                {
                        "arn_device": "arn:aws:iam::<account>:mfa/<name>"
                }
        ]
}
```

Once you have that, you can just execute the script (Python3) using the following syntax:

_python3 aws-temporary-tokens.py -c <mfa_auth_token> -p <profile_name> -d <MFA_arn> -t <expiration_time_in_seconds>_

The only parameter required is **-c <mfa_auth_token>**

Some examples:

- python3 aws-temporary-tokens.py -c 556677
or
- python3 aws-temporary-tokens.py -c 472384 -p my_second_profile

This will open a new terminal on MacOS with these variables attached to it:
* AWS_ACCESS_KEY_ID
* AWS_SECRET_ACCESS_KEY
* AWS_SESSION_TOKEN

You can check it using the command _env_ in that terminal.

For Linux, you can copy/paste the variables and export those in any terminal.

Then you will be able to run your aws cli commands as usual.
- aws s3 ls
- etc
