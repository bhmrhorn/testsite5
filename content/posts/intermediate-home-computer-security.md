---
title: "Intermediate home computer security"
date: 2023-03-18T22:35:47-04:00
draft: false
---

This is the third in a series of posts that explain the need to properly secure your home computer and that provide recommendations to do so. My post on [Basic home computer security](/wp/posts/basic-home-computer-security/) presents non-technical recommendations that you can follow to enhance the security of your computer. Those recommendations focus on altering behavior that attackers can take advantage of to compromise your computer. This post presents technical recommendations and assumes that you have a moderate level of technical proficiency.

## What technical steps can I take to make my computer more secure?

To trick your computer (as opposed to you) into running a program, an attacker must identify and exploit a problem with a program that you’re already running. The types of programs below are commonly targeted.

- Web browsers (such as Chrome, Safari, Firefox, Edge, Internet Explorer)
- Operating systems (such as Microsoft Windows and macOS)
- Office software (such as Microsoft Office and OpenOffice)</li>
- Programs that interact with web content (such as Adobe Acrobat Reader and Apple Quicktime Player)

Most attacks against home computers are targeted at broad groups, such as all computers that are running Adobe Reader 8.1. Unless you are a high value target, it is unlikely that attackers will individually target you or your computer. Many automated attacks rely on finding your computer by searching for it from the internet. You can easily make your computer invisible to random searches by connecting it to the internet through a router, instead of directly to a modem. Many manufacturers, such as Linksys (now owned by Cisco), make home routers that are offered at moderate costs by many retailers.

A malicious program can do much less harm if it is run by a user account with limited privileges (such as a User account in Windows) than if it is run by an account with full access to the computer (such as an Administrator account in Windows). You should setup and use an account with limited privileges for most activities. Switch to an account with full access only when you need to install or update software.

Many games require greater privileges than web browsers and productivity software. The same is often true of older software and software that was not written to conform to established standards. If you find that certain programs will not run with limited privileges, you should consider running them on a separate computer that is only connected to the internet as needed. If this is not possible, at least limit your use of highly privileged accounts to when it is actually necessary.

Most automated attacks target old versions of programs that have well known problems. You should ensure that you are running updated versions of any software that uses data from the internet. Many popular programs automatically update themselves without user interaction. Software that automatically updates itself can dramatically reduce the vulnerability of your computer.

If you are using Microsoft Windows as your operating system, enable the automatic update feature. Auto update is enabled by default in recent versions of Windows. Google's Chrome web browser updates itself automatically even for users with limited privileges. Chrome also includes a PDF reader that is updated automatically. Since many exploits target the operating system, browser, or the PDF reader it is extremely beneficial to have all of these updated frequently.

## What can I do if I am not technically proficient enough to implement the recommendations?

Regardless of your level of technical proficiency, your use of a computer exposes you and others to risks. If you cannot manage these risks by properly securing your computer, you should consider obtaining assistance from a technically proficient individual. Ignoring the issue of security will not prevent your computer from being compromised.