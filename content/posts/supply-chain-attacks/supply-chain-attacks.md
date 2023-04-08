---
title: "What are Supply Chain Attacks and how to mitigate them"
date: 2023-04-08T15:59:06+02:00
draft: false
---

# What's a Supply Chain Attack?

Basically it's when a malicious actor swaps one of the software components with a compromised one.

Nowadays, the great majority of consumer-facing software, such as webapps or mobile apps, make use of third party software components in the form of libraries.

Consider the following image as an example. 
It depicts a standard app which makes use of components such as `Searcher`, `Monitoring`, `Math`, etc.

![A compromised app](/images/supply-chain-compomised-lib.png)

These components are created and maintained, by third party organizations, often by individuals from the open source community. Usually with benevolent intent.

Once the third party is ready to ship this component, it will upload it to a package manager, where other users will download it.

# Enter the world of package managers

A package manager is a centralized code repository, where these components reside. These components may be public or private, depending on what the original author intends.

In order to upload any given component, the author will require a standard user account, so that only he/she is the rightful owner of the component's distribution.

Regardless of how popular the component is, the author is handed a huge responsibility.

If the package manager access happened to be compromised by a malicious actor, it would mean big trouble for whoever makes use of the software component.

These components are then downloaded by other developers who want to leverage the pre-existing functional code.
**Code-reuse** is, more often than not, beneficial and safe, since reusing open source code that has been peer-reviewed many times *usually* translates to reliable components.

I always perform a **code review** before including any given component into my project.

# How to be protected against Supply Chain Attacks?

Code-reuse saves developers and organizations precious time, but they also introduce **Dependency Risk**.

## Is there a way to eliminate Dependency Risk?

Obviously, the best way to be protected is to avoid unnecessary dependencies altogether.

However, keeping external dependencies to 0 is extremely hard for any complex application. That's why we need to control the amount external dependencies, to an acceptable number, thus controlling **Dependency Risk**.

## How can we reduce Dependency Risk?

Fortunately, we can leverage cryptographic hashes to perform integrity checks, making sure that the component has not been tampered with.

Package managers already support this and it's our responsibility to verify that the component's hash corresponds to the non-malicious version.
Once verified, we need to explictly reference the hash we have verified in our dependency manifest.

This is called **Dependency Pinning**.


# Takeaways

- Perform **Code Reviews** on the external component's source code, especially when upgrading versions. 
- Control **Dependency Risk** by reducing the number of external dependencies
- Use **Dependency Pinning** to only include the exact components you want. 

