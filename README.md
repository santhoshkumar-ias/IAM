# Experiment 6 – Implementing Identity Management Using Amazon IAM
# Name   : SANTHOSH KUMAR V
# Reg No : 212225040381

## Aim
To create and configure IAM users and groups in AWS, assign permissions using IAM policies, enable console access, and verify role-based access to Amazon S3.

## Requirements
- AWS Account
- Internet Connection
- Web Browser
- Amazon S3 Bucket

## PART A – ACCESS AWS IAM

### Step 1: Login to AWS Management Console

1. Open the AWS Management Console.
2. Sign in using your AWS account credentials.
3. Search for **IAM** using the AWS search bar.
4. Select **IAM (Identity and Access Management)**.

**Screenshot 1 – AWS IAM Dashboard**

<img width="1833" height="961" alt="Screenshot 2026-11-22 140830" src="https://github.com/user-attachments/assets/bb28131a-96ce-40e1-b151-a9ca3f6bcb84" />


## PART B – CREATE AN IAM GROUP

### Step 2: Create an IAM Group

1. In the IAM dashboard, select **User groups** from the left-side menu.
2. Click **Create group**.
3. Enter the group name:

   `cloudSecurity_2026`

4. Do not add users at this stage.
5. Click **Create group**.

The IAM group `cloudSecurity_2026` is created.

**Screenshot 2 – IAM Group Creation**

<img width="1856" height="596" alt="Screenshot 2026-11-22 140940" src="https://github.com/user-attachments/assets/9383b6fd-eb06-4dac-ad73-c3b587df15dd" />

### Step 3: Attach an IAM Policy to the Group

1. Open the `cloudSecurity_2026` group.
2. Select the **Permissions** tab.
3. Click **Add permissions**.
4. Select **Attach policies directly**.
5. Search for:

   `AmazonS3ReadOnlyAccess`

6. Select the checkbox next to the policy.
7. Click **Next** and then **Add permissions**.

The group is now assigned read-only access to Amazon S3.

**Screenshot 3 – Attached IAM Policy**

<img width="1596" height="703" alt="Screenshot 2026-11-22 141103" src="https://github.com/user-attachments/assets/a2d8390a-3957-4450-bfb3-54e557cb76be" />

## PART C – CREATE AN IAM USER

### Step 4: Create an IAM User

1. From the IAM navigation menu, select **Users**.
2. Click **Create user**.
3. Enter the username:

   `student01`

4. Enable AWS Management Console access.
5. Configure a console password.
6. Click **Next**.

**Screenshot 4 – IAM User Creation**

<img width="1566" height="787" alt="Screenshot 2026-11-22 141306" src="https://github.com/user-attachments/assets/79e758f1-d995-4690-916e-52b51288665b" />

### Step 5: Add the User to the IAM Group

1. On the Permissions page, select **Add user to group**.
2. Select the group:

   `cloudSecurity_2026`

3. Click **Next**.
4. Review the configuration.
5. Click **Create user**.

The user `student01` is now a member of the `cloudSecurity_2026` group.

**Screenshot 5 – User Added to Group**

<img width="1602" height="625" alt="Screenshot 2026-11-22 141432" src="https://github.com/user-attachments/assets/774e918e-8f42-4635-bdd8-d6971c4a909d" />


## PART D – VERIFY IAM PERMISSIONS

### Step 6: Verify User Permissions

1. Open **IAM → Users**.
2. Click `student01`.
3. Open the **Permissions** tab.
4. Verify that the following policy is displayed:

   `AmazonS3ReadOnlyAccess`

5. Check the **Attached via** column.
6. Verify that the policy is attached through the group `cloudSecurity_2026`.

The permission hierarchy is:

```text
student01
    |
    v
cloudSecurity_2026
    |
    v
AmazonS3ReadOnlyAccess
    |
    v
Amazon S3 Read-only Access
```

**Screenshot 6 – User Permissions Verification**

<img width="1602" height="625" alt="Screenshot 2026-11-22 141432" src="https://github.com/user-attachments/assets/849ccbe8-39fd-43e8-acca-52c45fd8f35e" />


### Step 7: Enable Console Access

1. Open **IAM → Users → student01**.
2. Select **Security credentials**.
3. Locate AWS Management Console access.
4. Verify that console access is enabled.
5. Configure or reset the console password if required.
6. Complete the configuration.

**Note:** The console password must be kept confidential and should not be shared.

**Screenshot 7 – Console Access Configuration**

<img width="1602" height="625" alt="Screenshot 2026-11-22 141432" src="https://github.com/user-attachments/assets/1bde6cfd-8731-4186-9bba-98fd9fd55d23" />


## PART E – LOGIN AS IAM USER

### Step 8: Obtain the AWS Account ID

1. Open the AWS Management Console.
2. Click the account name in the top-right corner.
3. Locate the **Account ID**.
4. Copy the 12-digit AWS account ID.

Students should use their own AWS account ID when performing this experiment.

### Step 9: Login as the IAM User

1. Open a new browser window or Incognito/Private window.
2. Visit the AWS sign-in page: https://signin.aws.amazon.com/console
3. Select **IAM user** login if prompted.
4. Enter your AWS Account ID.
5. Enter the IAM username:

   `student01`

6. Enter the configured password.
7. Click **Sign in**.
8. Complete the password change if prompted.

The AWS Management Console should now open under the IAM user `student01`.

**Screenshot 8 – IAM User Login**

<img width="1840" height="842" alt="Screenshot 2026-11-22 141715" src="https://github.com/user-attachments/assets/b5d6c423-7b2e-477c-a36a-0ffcaeb4b0aa" />


## PART F – VERIFY AMAZON S3 ACCESS

### Step 10: Verify Amazon S3 Access

1. After logging in as `student01`, search for **S3**.
2. Open Amazon S3.
3. Select **General purpose buckets**.
4. Verify that the previously created S3 bucket is visible.
5. Open the bucket.
6. Verify that the user can view the bucket and its objects.

This confirms that the IAM policy provides the assigned S3 read permissions.

**Screenshot 9 – S3 Bucket Access**

<img width="1840" height="842" alt="Screenshot 2026-11-22 141715" src="https://github.com/user-attachments/assets/9cbfb9fb-3ff8-4fcc-855b-1d16f44315ce" />


### Step 11: Verify Least-Privilege Access

The user `student01` has been assigned the policy:

`AmazonS3ReadOnlyAccess`

Therefore, the user should have read access but should not have permission to perform S3 write or delete operations.

For testing:

1. Open the S3 bucket as `student01`.
2. Observe the available operations.
3. Do not delete any existing object.
4. If testing an upload operation, use a harmless test file.
5. Attempt the upload.
6. Verify that AWS returns an **Access Denied** response for the unauthorized write operation.

**Important:** The S3 console may display an Upload button even when the user does not have permission to complete the upload. The actual permission check occurs when AWS attempts the operation.

**Screenshot 10 – Access Denied Verification**

<img width="1840" height="842" alt="Screenshot 2026-11-22 141715" src="https://github.com/user-attachments/assets/4e1c2615-f358-4b82-a3d6-a33ed68910f8" />


## PART G – PERMISSION VERIFICATION TABLE

| Parameter | Configuration |
|---|---|
| IAM Group | cloudSecurity_2026 |
| IAM User | student01 |
| Attached Policy | AmazonS3ReadOnlyAccess |
| Policy Attachment | Through IAM Group |
| Console Access | Enabled |
| S3 Read Access | Allowed |
| S3 Upload Access | Denied |
| S3 Delete Access | Denied |

## RESULT

Thus, Identity and Access Management (IAM) was implemented in AWS by creating an IAM group, assigning the `AmazonS3ReadOnlyAccess` policy, creating an IAM user, enabling console access, and adding the user to the group.

The IAM user's permissions were verified by accessing Amazon S3 and checking the assigned read-only permissions. The experiment demonstrated how AWS IAM provides centralized identity management, group-based permissions, and least-privilege access control for cloud resources.
