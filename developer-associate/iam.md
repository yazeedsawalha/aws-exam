# Identity and Access Management (IAM)

IAM stands for **Identity and Access Management**. It is a global AWS service used to create users, assign them to groups, and manage access to AWS resources.

---

## Root Account

- The **root user** is created by default when an AWS account is set up.
- It should only be used for initial account setup and **never for daily tasks or shared**.

---

## Creating Users in IAM

- **Users** represent individuals within your organization.
- Each user is created separately and can be grouped if needed.

---

## Creating Groups in IAM

- **Groups** allow logical organization of users with similar roles or permissions.

### Example:

- **Developers Group**: Alice, Bob, and Charles.
- **Operations Group**: David and Edward.

- Groups can only contain **users**, not other groups.

---

## Users Without Groups

- Users do not necessarily need to belong to a group (e.g., Fred).
- However, it is not considered a **best practice**.

---

## Users in Multiple Groups

- A user can belong to multiple groups.

### Example:

- Charles and David are part of both the **Developers Group** and the **Audit Team Group**.

---

## Purpose of Users and Groups

- To allow access to AWS accounts and services.
- Access is granted through **permissions**.

---

## Permissions and Policies

- **Permissions** are defined using **IAM Policies**, which are JSON documents.
- Policies specify:
  - **Actions** (e.g., `Describe`, `ListUsers`, `GetUsers`)
  - **Resources** (e.g., EC2, Elastic Load Balancing, CloudWatch)
  - **Effect** (e.g., `Allow`, `Deny`)

- Example JSON Policy:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": ["ec2:Describe*", "cloudwatch:ListMetrics"],
      "Resource": "*"
    }
  ]
}
```

---
# IAM Policies In Depth

## Scenario: Managing Policies for Groups and Users

Imagine we have a group of developers:

- **Alice**, **Bob**, and **Charles** are part of the **Developers** group.
- When a policy is attached to the **Developers** group, it applies to all members of the group. This means Alice, Bob, and Charles will inherit this policy.

Now, consider a second group:

- **Operations** group contains **David** and **Edward**, who have a different policy than the Developers group.

If there is an individual user:

- **Fred** is a user who does not belong to any group.
- An **inline policy** can be attached directly to Fred. Inline policies are user-specific and can be used regardless of group membership.

Additionally:

- If **Charles** and **David** both belong to the **Audit Team**, attaching a policy to the Audit Team will apply to both users.
  - In this case:
    - Charles will have policies from the **Developers** group and the **Audit Team**.
    - David will have policies from the **Operations** group and the **Audit Team**.

## IAM Policy Structure Overview

An IAM policy is a JSON document with the following structure:

### Key Components of the Policy Structure

1. **Version**
   - Specifies the policy language version.
   - Default value: `2012-10-17`.

2. **ID** (optional)
   - Used to identify the policy.

3. **Statements**
   - A policy can have one or multiple **statements**. Each statement contains:

     - **SID** (optional)
       - The Statement ID, an identifier for the statement.

     - **Effect**
       - Determines whether the statement allows or denies access.
       - Example: `Allow` or `Deny`.

     - **Principal**
       - Specifies which accounts, users, or roles the policy applies to.
       - Example: The root account of your AWS account.

     - **Action**
       - Lists the API calls that are either allowed or denied based on the **Effect**.

     - **Resource**
       - Lists the resources to which the actions will be applied.
       - Example: A specific S3 bucket.

     - **Condition** (optional)
       - Specifies conditions under which the statement is applied.

### Example Policy Structure

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "1",
      "Effect": "Allow",
      "Principal": {
        "AWS": "arn:aws:iam::123456789012:root"
      },
      "Action": "s3:*",
      "Resource": "arn:aws:s3:::example-bucket"
    }
  ]
}
```

### Key Elements for the Exam

Ensure you understand the following:

1. **Effect**: Determines whether the statement allows or denies actions.
2. **Principal**: Identifies the entity (account, user, or role) to which the policy applies.
3. **Action**: Specifies the API actions affected by the policy.
4. **Resource**: Lists the resources the actions apply to.


## Best Practices

1. **Avoid using the root account**.
2. Create users and assign them to appropriate groups.
3. Define permissions based on the **Least Privilege Principle**:
   - Only grant the minimum permissions required for a user or group to perform their job.
   - This minimizes security risks and potential costs.

---

# Protecting Users in AWS Groups

## How Do We Protect Users?
Now that we have created users in groups, it’s time to protect them from being compromised. For this, we have two defense mechanisms:

### 1. Define a Password Policy
Why is this important? Well, the stronger the password you use, the more secure your accounts will be. In AWS, you can set up a password policy with these options:

- **Set Minimum Password Length:** Define how long the password should be.
- **Require Specific Character Types:** For example, include:
  - An uppercase letter
  - A lowercase letter
  - A number
  - A special character, like `?` or `!`
- **Allow or Restrict Password Changes:** Decide if IAM users can change their own passwords.
- **Force Password Expiry:** Require users to update their passwords periodically (e.g., every 90 days).
- **Prevent Password Reuse:** Stop users from reusing their old passwords.

A good password policy is very helpful against brute-force attacks on your account.

### 2. Multi-Factor Authentication (MFA)
The second layer of protection is **Multi-Factor Authentication (MFA)**. You may have already used this on other websites, but in AWS, it’s a must-have. Why? Because it makes it much harder for someone to gain access to your account, even if they steal your password.

#### How Does MFA Work?
MFA combines two things:
1. Something you **know** (your password).
2. Something you **have** (a security device).

For example, Alice knows her password and also has an MFA device generating a unique token. When Alice logs in, she uses both the password and the token to gain access. If her password is stolen, her account is still safe because the hacker would also need her MFA device (e.g., her phone).

#### Types of MFA Devices in AWS
Here are the options available in AWS:

1. **Virtual MFA Device:**
   - Use apps like Google Authenticator (single-device) or Authy (supports multiple tokens).
   - Ideal for managing multiple accounts on one device.

2. **Universal 2nd Factor (U2F) Security Key:**
   - Example: YubiKey by Yubico (third-party device).
   - A physical key you can attach to your keychain.
   - Supports multiple root and IAM users with one device.

3. **Hardware Key Fob MFA Device:**
   - Example: Provided by Gemalto (third-party).
   - A standalone hardware device.

4. **GovCloud MFA Device:**
   - Example: Provided by SurePassID (third-party).
   - Specially designed for AWS GovCloud.

### Why Use These Measures?
Password policies help protect your accounts from brute-force attacks. MFA adds an extra layer of defense by requiring a physical device, making unauthorized access much harder.

---
- **IAM Security Tools**

  - **IAM Credentials Report**
    - This is at the account level.
    - The report contains all your account users and the status of their various credentials.
    - We will generate this report and review it shortly.

  - **IAM Access Advisor**
    - This tool operates at the user level.
    - It shows the service permissions granted to a user and the last time those services were accessed.
    - This tool is very helpful for implementing the principle of least privilege.
    - Using the Access Advisor, you can identify unused permissions and reduce a user's permissions to align with the principle of least privilege.

- **IAM Best Practices**

  - Do not use a root account except when setting up your AWS account.
  - Maintain two accounts: a root account and a personal account.
  - One AWS user equals one physical user. If someone else needs access, create a new user for them.
  - Assign users to groups and manage permissions at the group level.
  - Create and enforce a strong password policy.
  - Use and enforce multi-factor authentication (MFA) to secure accounts.
  - Use roles when assigning permissions to AWS services, including EC2 instances.
  - When using AWS programmatically (e.g., CLI or SDK), generate access keys and keep them secret.
  - Edit account permissions using IAM Credentials Reports or IAM Access Advisor.
  - Never share IAM users or access keys.

- **IAM Summary**

  - IAM users should map to actual physical users in your company, each having a password for the AWS console.
  - Users can be grouped into groups to manage permissions collectively.
  - Attach policies or share JSON documents to define permissions for users or groups.
  - Roles can be created as identities for AWS services, such as EC2 instances.
  - For security, enable multi-factor authentication (MFA) and set a strong password policy for users.
  - Use the CLI to manage AWS services via the command line or the SDK to manage services programmatically.
  - Generate access keys to access AWS using the CLI or SDK.
  - Audit IAM usage with IAM Credentials Reports and IAM Access Advisor.




