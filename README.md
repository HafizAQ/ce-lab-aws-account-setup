# Lab: AWS Account Setup and Security Basics

## Overview

In this lab, you'll configure essential security settings for your AWS account. You'll enable Multi-Factor Authentication (MFA), set up billing alerts, and configure your account for safe cloud learning.

**Estimated Time:** 30-45 minutes

## Learning Objectives

By the end of this lab, you will be able to:

- Enable Multi-Factor Authentication (MFA) on your AWS root account
- Set up billing alerts to monitor AWS spending
- Create an AWS account alias for easier sign-in
- Configure Free Tier usage alerts
- Apply AWS security best practices

## Prerequisites

- AWS account created
- Access to email associated with AWS account
- Smartphone with authenticator app installed (Google Authenticator, Microsoft Authenticator, or Authy)

## Lab Structure

This lab consists of 5 main exercises:

1. Enable MFA on root account
2. Create billing alerts
3. Set up account alias
4. Configure Free Tier alerts
5. Document and reflect

---

## Exercise 1: Enable Multi-Factor Authentication (MFA)

MFA adds a second layer of security beyond your password. Even if your password is compromised, attackers cannot access your account without the MFA code.

### Steps:

**1. Sign in as Root User**

- Go to [AWS Console](https://console.aws.amazon.com/)
- Use your account email and password

**2. Navigate to Security Credentials**

- Click your account name (top right corner)
- Select "Security credentials"

**3. Enable MFA**

- Scroll to "Multi-factor authentication (MFA)" section
- Click "Activate MFA"

**4. Choose Virtual MFA Device**

- Select "Virtual MFA device"
- Click "Continue"

**5. Set Up Authenticator App**

- Open your authenticator app on your phone
- Scan the QR code shown by AWS
- Or manually enter the secret key

**6. Enter Two Consecutive MFA Codes**

- Enter the first 6-digit code from your app
- Wait for the code to refresh (~30 seconds)
- Enter the second 6-digit code
- Click "Assign MFA"

**7. Verify Success**

- You should see "MFA device successfully associated"
- Note: Save backup codes if offered!

### Deliverable:

- Screenshot showing MFA successfully enabled
- Save to `screenshots/mfa-enabled.png`

---

## Exercise 2: Create Billing Alerts

Billing alerts help you avoid unexpected charges by notifying you when costs exceed thresholds.

### Part A: Enable Billing Alerts

**1. Navigate to Billing Preferences**

- Click account name (top right) → "Billing Dashboard"
- In left sidebar, click "Billing preferences"

**2. Enable Alerts**

- Check ☑️ "Receive PDF Invoice By Email"
- Check ☑️ "Receive Free Tier Usage Alerts"
- Check ☑️ "Receive Billing Alerts"
- Enter your email address
- Click "Save preferences"

**Note:** It may take 15-30 minutes for billing alerts to activate.

### Part B: Create CloudWatch Billing Alarm

**1. Navigate to CloudWatch**

- Search for "CloudWatch" in AWS Console search bar
- Click "CloudWatch"

**2. Create Billing Alarm**

- In left sidebar: Alarms → Billing
- Click "Create alarm"

**3. Select Metric**

- Click "Select metric"
- Choose "Billing" → "Total Estimated Charge"
- Check the box for "USD"
- Click "Select metric"

**4. Define Alarm Conditions**

- Threshold type: **Static**
- Whenever EstimatedCharges is: **Greater than**
- Define threshold value: **10** (for $10)
- Click "Next"

**5. Configure Notifications**

- Click "Create new topic"
- Topic name: `billing-alerts`
- Email endpoint: Your email address
- Click "Create topic"
- Click "Next"

**6. Name Your Alarm**

- Alarm name: `Billing-Alert-$10`
- Alarm description: `Alert when charges exceed $10`
- Click "Next"

**7. Review and Create**

- Review all settings
- Click "Create alarm"

**8. Confirm Email Subscription**

- Check your email for "AWS Notification - Subscription Confirmation"
- Click "Confirm subscription"

### Deliverables:

- Screenshot of billing preferences saved: `screenshots/billing-preferences.png`
- Screenshot of alarm created: `screenshots/billing-alarm.png`
- Screenshot of email confirmation: `screenshots/sns-confirmed.png`

---

## Exercise 3: Create Account Alias

An account alias makes your sign-in URL easier to remember.

### Steps:

**1. Navigate to IAM**

- Search for "IAM" in console search bar
- Click "IAM"

**2. Create Account Alias**

- In the IAM Dashboard, find "AWS Account" section
- Click "Create" next to "Account Alias"
- Enter a unique alias (e.g., `yourname-ironhack-bootcamp`)
- Click "Create alias"

**3. Note Your New Sign-In URL**

- Your URL is now: `https://YOUR-ALIAS.signin.aws.amazon.com/console`
- Test it by signing out and back in

### Deliverable:

- Screenshot of account alias created: `screenshots/account-alias.png`
- Document your alias in `SOLUTION.md`

---

## Exercise 4: Configure Free Tier Alerts

Monitor your Free Tier usage to avoid unexpected charges.

### Steps:

**1. Navigate to Billing Dashboard**

- Account name → Billing Dashboard

**2. Access Free Tier**

- In left sidebar, click "Free Tier"

**3. Review Current Usage**

- Examine each service's usage
- Note which services you're using
- Check for any warnings (yellow/orange)

**4. Set Up Email Alerts** (if not done in Exercise 2)

- Billing preferences → "Receive Free Tier Usage Alerts"

### Deliverable:

- Screenshot of Free Tier dashboard: `screenshots/free-tier-dashboard.png`
- Document your current usage in `SOLUTION.md`

---

## Exercise 5: Security Best Practices Documentation

### Review and Document:

Answer the following questions in `SOLUTION.md`:

1. **Why is MFA important even for a personal learning account?**
2. **What would happen if you left your root user unprotected?**
3. **How do billing alerts help prevent unexpected charges?**
4. **What threshold did you set for your billing alert and why?**
5. **What is your account alias and why did you choose it?**
6. **What services are you currently using according to the Free Tier dashboard?**

---

## Submission

### Required Deliverables:

1. **Screenshots folder** with all required screenshots:

   - `mfa-enabled.png`
   - `billing-preferences.png`
   - `billing-alarm.png`
   - `sns-confirmed.png`
   - `account-alias.png`
   - `free-tier-dashboard.png`
2. **SOLUTION.md** completed with:

   - Your account alias
   - Current Free Tier usage summary
   - Answers to all reflection questions

### How to Submit:

1. **Commit your work:**

   ```bash
   git add .
   git commit -m "Complete AWS account setup lab"
   git push origin main
   ```
2. **Create Pull Request:**

   - Go to your forked repository on GitHub
   - Click "Pull requests" → "New pull request"
   - Title: "AWS Account Setup Lab - [Your Name]"
   - Description: Brief summary of what you completed
   - Click "Create pull request"
3. **Submit PR URL to Student Portal**

---

## Troubleshooting

### Issue: Can't access Billing Dashboard

**Cause:** Not signed in as root user

**Solution:** Sign out and sign back in using your account email (root user)

---

### Issue: MFA showing "Invalid code"

**Cause:** Time sync issue between device and AWS

**Solution:**

- Check device time settings (should be automatic)
- Ensure authenticator app is synced
- Try re-scanning QR code
- Use a different authenticator app

---

### Issue: Not receiving billing alert emails

**Cause:** SNS subscription not confirmed

**Solution:**

- Check email (including spam folder)
- Look for "AWS Notification - Subscription Confirmation"
- Click confirmation link
- Wait a few minutes for activation

---

### Issue: Can't create CloudWatch billing alarm

**Cause:** Billing alerts not enabled

**Solution:**

- Go to Billing Dashboard → Billing preferences
- Check "Receive Billing Alerts"
- Save preferences
- Wait 15-30 minutes
- Try creating alarm again

---

## Success Criteria

Your lab is complete when:

- ✅ MFA enabled on root account (screenshot proves it)
- ✅ Billing alert configured and email confirmed
- ✅ Free Tier usage alerts enabled
- ✅ Account alias created and documented
- ✅ All screenshots captured and saved
- ✅ All reflection questions answered
- ✅ Work committed to GitHub
- ✅ Pull request created

---

## Additional Resources

- [AWS MFA Documentation](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_mfa.html)
- [AWS Billing Alerts](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/monitor_estimated_charges_with_cloudwatch.html)
- [AWS Security Best Practices](https://aws.amazon.com/premiumsupport/knowledge-center/security-best-practices/)

---

**Good luck! 🔒**
