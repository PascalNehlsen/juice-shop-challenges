# Deluxe Fraud Challenge Report

> [!CAUTION]  
> **Only for Testing Purposes.**  
> Documentation in this repository is entirely written for educational purposes.

**Project**: OWASP Juice Shop - Deluxe Fraud Challenge (Improper Input Validation)
**Tools**: Kali Linux with Burp Suite, Firefox Developer Tools
**Author**: Pascal Nehlsen
**Portfolio**: [https://www.pascal-nehlsen.de/](https://www.pascal-nehlsen.de/)
**GitHub Link**: [https://github.com/PascalNehlsen/juice-shop-challenges/challenges/deluxe-fraud.md](https://github.com/PascalNehlsen/juice-shop-challenges/challenges/deluxe-fraud.md)

## Table of Contents

1. [Introduction](#Introduction)
2. [Objective](#Objective)
3. [Approach](#Approach)
   - [Step 1: Information Gathering](#step-1-information-gathering)
   - [Step 2: Manipulating the Purchase Request](#step-2-manipulating-the-purchase-request)
4. [Conclusion](#Conclusion)

### Introduction

The OWASP Juice Shop is a deliberately vulnerable web application designed to demonstrate security vulnerabilities. This report details the steps I took to complete the Deluxe Fraud Challenge.

### Objective

The objective of the Deluxe Fraud Challenge is to find a way for the user to obtain the "Deluxe Membership" of the OWASP Juice Shop for free or to fraudulently bypass payment processes. This simulates real-world attacks where attackers attempt to manipulate payments or enforce discounts to acquire products without proper payment.

### Approach

#### Step 1: Information Gathering

First, I navigated to the section where users can purchase the Deluxe Membership.

<div align="center">

![Information](/images/deluxe-fraud/information.png)

</div>

Upon clicking "Become a Member," I noticed that the membership costs $49.00, while our wallet balance showed $0.00. The purchase button was also disabled.

<div align="center">

![Become a Member](/images/deluxe-fraud/become-a-member.png)

</div>

To investigate how the button was disabled, I checked the Firefox Developer Tools.

<div align="center">

![Button deactivated](/images/deluxe-fraud/button-deactivated.png)

</div>

In the HTML, I found the attributes `mat-button-disabled` and `disabled='true'`. By removing these attributes through the console, I was able to activate the button.

<div align="center">

![Button Activated](/images/deluxe-fraud/button-activated.png)

</div>

#### Step 1: Manipulating the Purchase Request

However, clicking the button did not trigger any action. Therefore, I intercepted the request sent when clicking the button using Burp Suite. The intercepted request was a `POST` request containing a JSON object.

<div align="center">

![Payment](/images/deluxe-fraud/payment.png)

</div>

The `paymentMode` indicated that we wanted to pay using our wallet, but since we had no balance, I modified the `paymentMode` to an empty string. After clicking "Forward," I received a success message indicating that we were now a Deluxe Member. This was also verifiable on the website.

<div align="center">

![Result](/images/deluxe-fraud/challenge-solved.png)

</div>

### Conclusion

This challenge was successfully completed by modifying the `POST` request, allowing me to obtain a Deluxe Membership without proper payment.

<div align="center">

![Challenge Accepted](/images/captcha-bypass/challenge-accept.png)

</div>
