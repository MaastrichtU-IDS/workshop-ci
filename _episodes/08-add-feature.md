---
title: Add a new feature and create new release
teaching: 1
exercises: 1
questions:
- "How do I publish a new version of my package?"
objectives:
- "Increase version number."
- "Create new release."
keypoints:
- "Just do no mess up the version number."
---

Now that you have published a first version of your package you might want to edit it and publish a new version:

* Add new feature
  * Create `WIP` issue, branch and pull request (TODO, Tim?)

* Increase the version number in `setup.py`
  * `0.0.1` > `0.0.2`
  * Push to GitHub
* Create a new release
  * Got to the 🏷️ **Releases** tab
  * Click on **Create a new release** 
  * Provide the same version as used in `setup.py`