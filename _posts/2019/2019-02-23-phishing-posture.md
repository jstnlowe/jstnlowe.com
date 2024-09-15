---
layout: post
title: "Three-Pronged Approach to Phishing Emails"
date: 2019-02-23 21:30:40 -0400
categories: security
published: true
---

There has been a dramatic increase in phishing attempts the past few years with the most common tactic being to send out emails with spoofed “from” addresses that contain malicious attachments or instructions. At a glance, the better-crafted emails might seem legitimate and attackers have gotten very good at exploiting human weaknesses. Educating users just is not enough. Authenticating emails is somewhat complex and relies heavily on the sender for proper implementation and the recipient for proper scrutiny.

In its current form, the best authentication approach uses three protocols, but before we go over them it is important to understand why we need them to begin with.

# A Tale of Two Addresses
Email relies on something called the Simple Mail Transfer Protocol (SMTP) which is a standard that allows any computer to transmit an email message to any other computer. SMTP uses two "from" addresses: the "envelope from" and the "header from".

The "envelope from" is hidden in the email header and tells the recipient's mail server where the email should be returned ("bounced") to - like the return address on the outside of a physical piece of mail. The "header from" address is what you see displayed in the "From:" field in your email client - like the header you might see on the letter that was mailed inside an envelope. These two addresses do not have to be the same.

Unfortunately, both of these addresses can be spoofed; a malicious third party can craft an email to a recipient that appears to have come from a legitimate sender. Sometimes it can be difficult for a recipient to determine if the email is legitimate. Together, the three authentication protocols allow the recipient's email server to make that determination and handle the email appropriately.

# Sender Policy Framework (SPF)
SPF is a "path-based" protocolt that allows the recipient to verify that the email is indeed from the domain that it claims to be sent from. This is accomplished through the use of DNS records on the sender's domain that specify a whitelist of IP addresses that are allowed to send mail from that domain. If the email claims to have been sent by user@email.com but the email headers indicate that it was sent from a computer whose IP address does not appear on that whitelist, the recipient can treat the email accordingly. This check is performed before the recipient receives the contents of the email, allowing them to reject malicious emails without being exposed to anything that they might have contained. However, SPF only checks the "envelope from" address, meaning that the "header from" address can still be spoofed.

# DomainKeys Inentified Mail (DKIM)
DKIM is an "identity-based" protocol and forms the second layer. This protocol is a little more complicated. It essentially allows a sender to electronically sign emails in a way that can be verified by the recipient. This is done through the use of an asymmetric cryptographic algorithm and a set of two keys, one of which is known only to the sender (the "private" key) and the other is provided in a DNS record for the recipient to use (the "public" key). The cryptographic process is outside the scope of this article, but it essentially takes the email (the header, the content, or both) and uses the private key to calculate a special value called a "hash" in such a way that there is no way to back-calculate the private key from the hash and the email contents. This hash is sent along with the email. The public key is the other half of this unique key pair which allows the recipient to verify that the email was indeed sent by someone who holds the private key.

# Domain-based Message Authentication, Reporting, and Conformance (DMARC)
DMARC is the final piece of this process and uses something called "alignment" to close any holes in the SPF and DKIM authentications. DMARC alignment checks that the "header from" domain matches the "envelope from" domain used by SPF and that the "header from" domain matches the domain name used by the DKIM signature. This also means that an email has to pass both SPF and DKIM. DMARC also allows senders to tell email providers how to handle anything that fails authentication - to allow the email through (monitor), to send the email to a spam folder (quarantine), or to refuse delivery entirely (reject). DMARC also has a reporting piece which allows email providers to send reports back to the owner of a domain that provide aggregation and forensic information about the emails the provider received claiming to be sent from that domain