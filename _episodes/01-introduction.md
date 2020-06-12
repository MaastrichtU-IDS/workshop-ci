---
title: Introduction
teaching: 3
exercises: 0
questions:
- "What is CI/CD?"
- "Why is CI/CD useful for me?"
objectives:
- "Know what CI/CD is"
- "Understand the benefits of using CI/CD."
keypoints:
- "CI/CD automates as much as possible outside of core development tasks."
- "CI/CD allows for a more iterative way of testing, using and working on your application."
---

## CI/CD

Leaving documentation and testing for a 'finished' product is generally a bad idea. Development could be seen more as gardening than creating a building; it is never finished. This means development should be done in small increments; develop small features, document and test them and commit these small changes each time. In most cases it is also beneficial to *release* code many times and allow users to work with and give feedback to your changes often. 
Developing in such a way would be time consuming if we had to manually test, build and deploy the application each time. This is why CI/CD is important. CI/CD stands for Continuous Integration / Continuous Deployment (or Delivery depending on who you ask). The goal of CI/CD is to automate all these processes so that apps can be continuously tested, built and deployed without any manual effort. This ensures that the code is constantly in a state where it is documented, tested and available for others to review and use.