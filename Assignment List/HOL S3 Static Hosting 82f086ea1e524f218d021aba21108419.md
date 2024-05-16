# HOL S3 Static Hosting

# Create new S3 bucket

1. Search S3(Simple Storage Service) → Create bucket
2. Choose “Asia Pacific (Singapore) ap-southest-1” as AWS Region Fill unique bucket name
3. Select “ACLs disabled” option as Object Ownership and **Block *all* public access**
4. Disabled Bucket Versioning
5. Select service side encryption as (SSE-S3) and default settings for the rest options
6. Create bucket successfully

![HOL%20S3%20Static%20Hosting%2082f086ea1e524f218d021aba21108419/Assignment_HOL_S3_Static_Hosting_8a2714c9422c4a8fa7c91709707e248dUntitled.png](HOL%20S3%20Static%20Hosting%2082f086ea1e524f218d021aba21108419/Assignment_HOL_S3_Static_Hosting_8a2714c9422c4a8fa7c91709707e248dUntitled.png)

# Upload html contents

1. Prepare sample portfolio static web project
2. Go to the recent created bucket objects → Upload → Add folder → browse the sample project mentioned step#1
3. After upload succeeded, all files should be within root directory.
4. Select all uploaded files and folders and “Actions → Move” to root directory of bucket

![HOL%20S3%20Static%20Hosting%2082f086ea1e524f218d021aba21108419/Assignment_HOL_S3_Static_Hosting_8a2714c9422c4a8fa7c91709707e248dUntitled_1.png](HOL%20S3%20Static%20Hosting%2082f086ea1e524f218d021aba21108419/Assignment_HOL_S3_Static_Hosting_8a2714c9422c4a8fa7c91709707e248dUntitled_1.png)

# Enable Static web hosting

1. Go to the created bucket → Properties → “Static website hosting” section
2. “Enabled” static website hosting option
3. Select “Hosting type = Host a static website”
4. Enter index document as “index.html”
5. Enter error document as “404.html”
6. Enter redirection rule (refers from [https://docs.aws.amazon.com/AmazonS3/latest/userguide/how-to-page-redirect.html](https://docs.aws.amazon.com/AmazonS3/latest/userguide/how-to-page-redirect.html)
)
7. Sample rule is as below

```jsx
[
    {
        "Condition": {
            "KeyPrefixEquals": "Contact"        },        "Redirect": {
            "ReplaceKeyWith": "index.html"        }
    }
]
```

![HOL%20S3%20Static%20Hosting%2082f086ea1e524f218d021aba21108419/Assignment_HOL_S3_Static_Hosting_8a2714c9422c4a8fa7c91709707e248dUntitled_2.png](HOL%20S3%20Static%20Hosting%2082f086ea1e524f218d021aba21108419/Assignment_HOL_S3_Static_Hosting_8a2714c9422c4a8fa7c91709707e248dUntitled_2.png)

1. Browse link and 403 Forbidden error screen is alerted because files permission haven’t accessed yet.

![HOL%20S3%20Static%20Hosting%2082f086ea1e524f218d021aba21108419/Assignment_HOL_S3_Static_Hosting_8a2714c9422c4a8fa7c91709707e248dUntitled_3.png](HOL%20S3%20Static%20Hosting%2082f086ea1e524f218d021aba21108419/Assignment_HOL_S3_Static_Hosting_8a2714c9422c4a8fa7c91709707e248dUntitled_3.png)

# Enable public access by policy

1. Go to the created bucket → Permission → Edit “Block public access” section
2. Uncheck block public access for below 2 options

![HOL%20S3%20Static%20Hosting%2082f086ea1e524f218d021aba21108419/Assignment_HOL_S3_Static_Hosting_8a2714c9422c4a8fa7c91709707e248dUntitled_4.png](HOL%20S3%20Static%20Hosting%2082f086ea1e524f218d021aba21108419/Assignment_HOL_S3_Static_Hosting_8a2714c9422c4a8fa7c91709707e248dUntitled_4.png)

1. Permission → Bucket policy (refers from [https://docs.aws.amazon.com/AmazonS3/latest/userguide/WebsiteAccessPermissionsReqd.html](https://docs.aws.amazon.com/AmazonS3/latest/userguide/WebsiteAccessPermissionsReqd.html))
2. Sample policy rule is as below

```
"Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "PublicReadGetObject",
            "Effect": "Allow",
            "Principal": "*",
            "Action": [
                "s3:GetObject"
            ],
            "Resource": [
            "arn:aws:s3:::*Bucket-Name*/*"
            ]
        }
    ]
}
```

![HOL%20S3%20Static%20Hosting%2082f086ea1e524f218d021aba21108419/Assignment_HOL_S3_Static_Hosting_8a2714c9422c4a8fa7c91709707e248dUntitled_5.png](HOL%20S3%20Static%20Hosting%2082f086ea1e524f218d021aba21108419/Assignment_HOL_S3_Static_Hosting_8a2714c9422c4a8fa7c91709707e248dUntitled_5.png)

# Navigate URL

1. Browse URL([http://pp-static-web.s3-website-ap-southeast-1.amazonaws.com/](http://pp-static-web.s3-website-ap-southeast-1.amazonaws.com/))
for sample static website

![HOL%20S3%20Static%20Hosting%2082f086ea1e524f218d021aba21108419/Assignment_HOL_S3_Static_Hosting_8a2714c9422c4a8fa7c91709707e248dUntitled_6.png](HOL%20S3%20Static%20Hosting%2082f086ea1e524f218d021aba21108419/Assignment_HOL_S3_Static_Hosting_8a2714c9422c4a8fa7c91709707e248dUntitled_6.png)

1. Error screen (404.html)

![Untitled](HOL%20S3%20Static%20Hosting%2082f086ea1e524f218d021aba21108419/Untitled.png)