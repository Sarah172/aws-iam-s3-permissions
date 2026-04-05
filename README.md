# AWS IAM Policy for S3 Access Control

> A hands-on lab demonstrating how to enforce least-privilege access to Amazon S3 using IAM policies and validate permissions using AWS CLI.

---

## Overview

This project focuses on implementing **fine-grained access control** for Amazon S3 using IAM.

You will:

- Create an S3 bucket  
- Upload an object  
- Define a custom IAM policy  
- Restrict access to only `GetObject`  
- Validate permissions using AWS CLI  

---

## Architecture
IAM User → IAM Policy (GetObject only) → S3 Bucket
↓
AWS CLI Access

---

## Objectives

- Understand IAM policy structure  
- Apply least privilege access principles  
- Restrict S3 actions to specific operations  
- Test permissions using AWS CLI  
- Identify allowed vs denied actions  

---

## Technologies Used

- Amazon S3  
- AWS IAM  
- AWS CloudShell / CLI  

---

## Implementation Steps (With Screenshots)

### 1. Create S3 Bucket

![Create Bucket](./screenshots/01-create-bucket.png)

---

### 2. Upload Object

![Upload Object](./screenshots/02-upload-object.png)

---

### 3. Create IAM Policy

![Create Policy](./screenshots/03-create-policy.png)

---

### 4. Configure Policy (GetObject Only)

![Policy Config](./screenshots/04-policy-config.png)

---

### 5. Review & Create Policy

![Policy Review](./screenshots/05-policy-review.png)

---

### 6. Create IAM User

![Create User](./screenshots/06-create-user.png)

---

### 7. Generate Access Keys

![Access Keys](./screenshots/07-access-keys.png)

---

### 8. Configure AWS CLI

![AWS Configure](./screenshots/08-aws-configure.png)

---

### 9. Attempt to List Buckets (Expected Failure)

![List Buckets Fail](./screenshots/09-list-buckets-fail.png)

---

### 10. Attempt to List Objects (Expected Failure)

![List Objects Fail](./screenshots/10-list-objects-fail.png)

---

### 11. Successfully Download Object

![Copy Object](./screenshots/11-copy-object-success.png)

---

## Results

- User cannot list buckets (`AccessDenied`)  
- User can download objects using `GetObject`  
- Least privilege successfully enforced  

---

## Key Insights

- **Least Privilege is Critical**  
  Granting only `s3:GetObject` ensured the user could download files but not view or enumerate resources.
- **AWS Uses a Deny-by-Default Model**  
  Any action not explicitly allowed is automatically denied, reinforcing strong security by design.
- **Fine-Grained Permissions Matter**  
  Even closely related actions like `GetObject` and `ListBucket` are completely separate and must be defined individually.
- **Testing Validates Security Design**  
  Using the AWS CLI helped confirm exactly what the user could and could not do in a real-world scenario.
- **IAM Policies Require Precision**  
  Small mistakes in actions or resource scope can lead to either broken access or over-permissioning.

---

## Lessons Learned

- **`s3:GetObject` does NOT allow listing objects**  
  You must explicitly include `s3:ListBucket` if listing is required.
- **Resource Scope is Just as Important as Actions**  
  Defining the correct bucket or object ARN is crucial for policy effectiveness.
- Testing permissions is essential to verify security design  
- IAM misconfigurations can easily lead to over-permissioning  

---

## Challenges Encountered

- Understanding difference between:
  - `GetObject`
  - `ListBucket`
- Correctly scoping resources in IAM policy  
- CLI credential configuration  
- Interpreting AWS permission errors  

---

## Recommendations

### Security

- Always follow **least privilege principle**  
- Avoid using wildcard (`*`) in production policies  

### Improvements

- Add `ListBucket` selectively if needed  
- Restrict access to:
  - Specific objects
  - Specific prefixes  

### Testing

- Use IAM Policy Simulator  
- Test with multiple users and roles  

### Production Use

- Use **IAM Roles instead of users**  
- Rotate access keys regularly  
- Enable logging with:
  - CloudTrail  
  - S3 access logs  

---

## Conclusion

This lab demonstrates how to enforce **secure, minimal access controls** in AWS using IAM policies.

It highlights:

- The importance of least privilege  
- How AWS enforces permissions strictly  
- The value of testing access via CLI  

---

## Project Structure
├── README.md
└── screenshots/



