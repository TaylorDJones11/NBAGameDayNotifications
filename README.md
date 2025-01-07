# NBAGameDayNotifications 🏀 - Day 2

This project is a real-time NBA game alert system that notifies subscribed users via SMS or email about live game scores. It uses AWS services like SNS, Lambda, and EventBridge, along with NBA APIs, to deliver up-to-date game information to basketball fans. The project highlights cloud computing concepts and efficient notification handling.

- [Blog Link](https://dev.to/onetayjones/devops-challenge-day-2-building-an-automated-nba-score-alert-system-with-aws-3i6j)

## Features
- Fetches live NBA game scores from an external API.
- Sends formatted score updates to subscribers via SMS/Email using Amazon SNS.
- Automates regular updates with Amazon EventBridge.
- Designed with security best practices, ensuring IAM roles follow the principle of least privilege.

<img width="250" alt="Screenshot 2025-01-07 at 16 39 45" src="https://github.com/user-attachments/assets/270b1880-5a78-4e0a-9d69-7ff32c25e604" />



## Technical Architecture
<img width="500" alt="Screenshot 2025-01-07 at 13 43 40" src="https://github.com/user-attachments/assets/bc7ada9f-0ed1-4e7d-8235-147edc1cb340" />


## Project Technologies

- **Cloud Provider:** AWS  
- **Core Services:** SNS, Lambda, EventBridge  
- **External API:** NBA Game API (SportsData.io)  
- **Programming Language:** Python 3.x  
- **IAM Security:**  
  - Least privilege policies for Lambda, SNS, and EventBridge.
 


## Setting Up an NBA Game Alert System with AWS SNS and Lambda 🔑

### **1. Create an SNS Topic**
- Open the **AWS Management Console** and go to the **SNS service**.
- Click **Create Topic** and select **Standard** as the topic type.
- Enter a name for the topic (e.g., `gameday_topic`) and note the **ARN**.
- Click **Create Topic** to finalize.

### **2. Add Subscriptions to the SNS Topic**
- Open the SNS topic from the list.
- Navigate to the **Subscriptions** tab and click **Create Subscription**.
- Choose a **protocol**:
  - **For Email:**
    - Select **Email** and enter a valid email address.
  - **For SMS (phone number):**
    - Select **SMS** and enter a valid phone number in international format (e.g., `+1234567890`).
- Click **Create Subscription**.
- **Confirm the Subscription:**
  - **For Email:** Check your inbox and click the confirmation link.
  - **For SMS:** The subscription is active immediately after creation.

### **3. Create an SNS Publish Policy**
- Open the **IAM service** in the AWS Management Console.
- Go to **Policies → Create Policy**.
- Click **JSON** and paste the JSON policy from `gameday_sns_policy.json`.
- Replace **REGION** and **ACCOUNT_ID** with your AWS details.
- Click **Next: Tags** (optional), then **Next: Review**.
- Enter a name for the policy (e.g., `gameday_sns_policy`) and click **Create Policy**.

 ### **4. Create an IAM Role for Lambda**
- Open the **IAM service** in the AWS Management Console.
- Navigate to **Roles → Create Role**.
- Select **AWS Service** and choose **Lambda**.
- Attach the following policies:
  - **SNS Publish Policy** (`gameday_sns_policy`) – created in the previous step.
  - **Lambda Basic Execution Role** (`AWSLambdaBasicExecutionRole`) – an AWS-managed policy.
- Click **Next: Tags** (optional), then **Next: Review**.
- Enter a name for the role (e.g., `gameday_role`).
- Click **Create Role**.
- Copy and save the **ARN** of this role for use in the Lambda function.

### **5. Deploy the Lambda Function**
- Open the **AWS Management Console** and navigate to the **Lambda service**.
- Click **Create Function**.
- Select **Author from Scratch**.
- Enter a function name (e.g., `gameday_notifications`).
- Choose **Python 3.x** as the runtime.
- Assign the **IAM role** created earlier (`gameday_role`) to the function.
- Under the **Function Code** section:
  - Copy the contents of `src/gameday_notifications.py` from your repository.
  - Paste it into the inline code editor.
- Under the **Environment Variables** section, add:
  - `NBA_API_KEY`: Your NBA API key.
  - `SNS_TOPIC_ARN`: The ARN of the SNS topic created earlier.
- Click **Create Function**.

### **6. Set Up Automation with EventBridge**
- Open the **AWS Management Console** and navigate to the **EventBridge** service.
- Go to **Rules → Create Rule**.
- Select **Event Source: Schedule**.
- Define the **cron schedule** for when updates should be sent (e.g., hourly).
- Under **Targets**, select the Lambda function (`gd_notifications`) and save the rule.

### **7. Test the System**
- Open the **Lambda function** in the AWS Management Console.
- Create a **test event** to simulate execution.
- Run the function and check **CloudWatch Logs** for errors.
- Verify that **SMS or email notifications** are sent to subscribed users.

---

 **What I Learned**
- Building a **real-time notification system** with AWS SNS and Lambda.
- Implementing **least privilege IAM policies** for secure access.
- Automating workflows using **EventBridge**.
- Integrating **external APIs** into AWS services.

## **Future Enhancements**
- Add **NBA Parlay Predictions** to expand the system.
- Store **user preferences** (teams, game types) in **DynamoDB** for personalized alerts.
- Develop a **web-based UI** for user subscription management.

