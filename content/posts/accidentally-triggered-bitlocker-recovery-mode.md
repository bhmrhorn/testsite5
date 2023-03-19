---
title: "Accidentally triggered BitLocker recovery mode"
date: 2023-03-18T22:15:52-04:00
draft: false
---

While on a trip to New Orleans, I accidentally triggered recovery mode for the Microsoft BitLocker full disk encryption on my laptop. Once triggered, recovery mode requires that a recovery key be provided before the machine will boot. Recovery mode is intended to protect against a variety of attacks including bootkits. Unfortunately, accidentally triggering recovery mode renders the machine useless until the recovery key is available.

The recovery key can be either a file stored on a USB drive or a long string of numbers. When I enabled BitLocker, I mistakenly guessed that the recovery key would be rarely needed and could be stored in a manner that provided security but not ready access. This mistake cost me the use of my laptop during a trip.

Those considering enabling BitLocker should ensure that the recovery key can be easily accessed without the use of the computer that it is intended to recover. Specifically, the option to use a file on a USB drive as a recovery key requires the ability to access the file and place it on a USB drive. Storing the recovery key on a USB drive that is carried with the machine significantly reduces the security provided by BitLocker. A numeric recovery key can be easily left with a trusted individual to be read over the phone if needed.

I hope this story saves someone from the predicament in which I found myself. For more information about setting up BitLocker, see my post on [how to configure BitLocker](/wp/posts/bitlocker-with-tpm-pin-usb-startupkey/).