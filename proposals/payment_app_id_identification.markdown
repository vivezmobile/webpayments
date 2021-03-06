#1. Payment app authenticity management
***
##1.1 Problem statement

The payment app spec should provide mechanism to ensure the authenticity of the payment app. This includes several aspects:

* Problem 1: The payment app should be the one as it claims to be.
* Problem 2: How to prevent fake/malicious payment app to do evil things, for example, fishing etc.
    

#2 Solution proposal
##2.1 Problem analyze
Draft [Payment Method Identifiers](https://github.com/w3c/webpayments/blob/gh-pages/proposals/zach-pmi.md) discusses the identifiers of payment apps. For the proprietary systems, the draft proposes to use URL as the identifier of the payment app. Origin is used to ensure the authenticity of the payment app. However, origin based authenticity management can only solve problem 1 and can not solve problem 2.

For example, let us assume AlicePay.com is a famous payment service provider, AlicePay1.com is a fake one of AlicePay.com, the hacker may hack the merchant website and insert AlicePay1.com in the merchant website. Using origin based authenticity can not solve the problem.

##2.2 Solution

In this proposal, a verification file which contains the digital signature of the payment app identifier is used for the authenticity management of payment app. 

The verification file is located at a specific path in the payment app website. The path is generated by the browser based on the payment app name and identifier.


For example, in the use case as discussed in section 2.1, a verification file named verify.sign is located in the path [AlicePay.com/pay/verify/](AlicePay.com/pay/verify/), the browser will verify the signature information in addition to origin check. 

This solution can solve both problem 1 and problem 2 as described in section 1.1.

	File verify.sign:
	{
	   name: 'AlicePay',
	   identifier: ['https://AlicePay.com/pay'],
	   certificate: '.....',
	   signature: '...'
	 }

	

