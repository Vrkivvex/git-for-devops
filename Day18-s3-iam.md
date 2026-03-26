# Day 18 – AWS S3 & IAM (Detailed Notes)

---

## 1. AWS S3 (Simple Storage Service)

### Definition
S3 is an object storage service used to store and retrieve files from the cloud.

---

## Core Components

### Bucket
- Top-level container for storage
- Must have globally unique name

### Object
- File stored in bucket (image, HTML, etc.)

### Key
- Path/name of file inside bucket

---

## Bucket Creation Settings

- Region: ap-south-1 (Mumbai)
- Object Ownership: ACLs disabled
- Public Access: Disabled (for learning we unchecked block public access)
- Versioning: Disabled
- Encryption: Default (SSE-S3)

---

## Public Access Configuration

To make files accessible via browser:
- Disable Block Public Access
- Add Bucket Policy

---

## Bucket Policy (Public Read)

{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::bucket-name/*"
    }
  ]
}

Replace bucket-name with your actual bucket name.

---

## Static Website Hosting

Steps:
1. Upload index.html
2. Go to Properties → Enable Static Website Hosting
3. Set index document: index.html
4. Use endpoint URL

---

## Important Points

- Only supports static files (HTML, CSS, JS)
- No backend support
- Used for hosting simple websites

---

## 2. IAM (Identity and Access Management)

### Definition
IAM is used to manage users and permissions in AWS.

---

## Root vs IAM User

Root Account:
- Full access
- Used only for setup

IAM User:
- Limited access
- Used for daily work

---

## Permission Types

- Full Access → everything allowed
- Read Only → only view
- Custom Policy → specific control

---

## Custom Policy (Used)

{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "s3:ListAllMyBuckets",
      "Resource": "*"
    },
    {
      "Effect": "Allow",
      "Action": "s3:ListBucket",
      "Resource": "arn:aws:s3:::bucket-name"
    },
    {
      "Effect": "Allow",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::bucket-name/*"
    }
  ]
}

---

## Key Concepts

- Least Privilege → only required access
- Access ≠ Visibility
- Permissions are granular (list, read, write separate)

---

## Cost

- IAM → Free
- S3 → very low (free tier covers small usage)

---

## Summary

- S3 = storage
- IAM = access control
- Policies define permissions
- Security is critical in cloud