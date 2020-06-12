---
title: Run application locally
teaching: 1
exercises: 1
questions:
- "How do I develop my application locally before starting with CI/CD?"
objectives:
- "Testing the application before trying to run it in Docker."
- "Continuous improvement of the readme.md"
keypoints:
- "Write an appropriate amount of tests for your purpose."
- "Make sure to update your readme.md intermittently during development."
---

## Running the Python application

Before starting with CI/CD we will first check the application works correctly locally. The Python template comes with a setup.py file which allows an easy pip install of our application. Since performing '''bash pip3 install .''' each time we make a change can be tiresome, the -e argument can be added to pip install, to automatically reflect any change you make to the application directly in the environment.

In our setup.py, a good practice is to use requirements.txt to keep track of the dependencies of our application that need to be installed. These can then be installed using the setup.py or manually running ```bash pip3 install -r requirements.txt```. Another quick way of listing the dependencies is to use ```bash find_packages()```.

> ## Running the application
>
> * Run ```bash pip3 install -e .  ```
> * Run ```bash workshop_ci hello-world --help  ``` to see how to run your application.
> * Run the application with the correct inputs.
>
{: .challenge}

## Writing and running tests

There are many different kinds of tests which can be run for your application. Two of the most important are functional testing and unit testing. Functional testing is relatively straightforward. The application is assumed to be a black box, and the desired output is checked based on various inputs. Unit testing tests whether a 'unit' of code behaves as expected. When the code is divided up functionally into small methods, we can test these individually to see if they output the correct values for a number of inputs. Whenever someone makes a change to the method (or anything the method relies on), the unit test can be run to check everything is still as expected.

It is important to realize that no amount of testing or covering your code with unit tests will guarantee that it works. It is only possible to get some degree of confidence. How many tests you write is dependent on the required quality, the number of people working on your project and how much long term development you expect will be done. A large enterprise application developed by a company will require much more testing than a prototype created by a single developer. 

In almost all cases, tests are run automatically during the CI/CD process. If you should want them locally you can do so by performing the following steps.

> ## Testing the application
>
> *   ```bash pip3 install pytest ```
> *   ```bash pytest tests/``` 
>
{: .challenge}

## Adding documentation

Continuousy adding documentation is vital for others to make sense of your code. At IDS, we prefer to use the README.md for development related documentation. Open features and bugs can be added to GitHub issues. For more general information on the software the GitHub wiki can be utilized. Project documentation is done in the IDS teams folder on Google Drive.

> ## Adding documentation
>
> *   Add the steps to run and test the application to the README.md.
>
{: .challenge}

{% include links.md %}