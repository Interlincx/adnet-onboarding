# Initiating a New Project

This document serves as a comprehensive guide to initiating a new project. Please follow the steps outlined below to ensure a smooth start to the project.

## Reading Documentations

- Thoroughly review all available documentation in Readme.
- Search & go through slack conversations related to the project.
- Review test cases thoroughly as they can be a great source of documentation.

## Understanding the Product

- Use the product from an end-user's perspective to gain a comprehensive understanding of its features.
- Review the test cases for each feature, as they can serve as an excellent source of documentation.

## Understanding Codebases

- For back-end repositories, familiarize yourself with the APIs by making calls and understanding the request and response structure.
- For front-end repositories, run the corresponding back-end repositories and understand the features through their interaction with each other.

## Creating a Data Flow Diagram

Develop a Data Flow Diagram of the application based on your understanding of the system and discuss it with other team members. it should contain the following elements:

- User interactions
- Data sources
- Data processing
- Data storage
- Data retrieval
- Data presentation

## Addressing Unknowns

There are parts of the system that are unclear, focus on the known elements first. Identify the developers who have worked on the unclear parts of the system and ask them for clarification.

### Clarifying Questions

- Ensure you have the necessary permissions to accomplish the requested tasks.
- Verify that you have all the resources required to perform the task and inquire about any missing elements.
- Confirm access to all test and production environments. If test environments are unavailable, ask for permission to post to production for debugging purposes.

### Discussion Threads

Initiate discussion threads and ask specific questions with [code references](https://docs.github.com/en/repositories/working-with-files/using-files/getting-permanent-links-to-files). 

Questions should include specific contexts in the following order:
  - The problem
  - Why it’s a problem
  - What you’ve done to attempt to solve it
  - What you think could solve it
  - What you are asking to do

## Creating Repositories

- Evaluate the need for immediate repository setup or if it can wait until some tasks are completed. Choose a suitable repository name and ensure proper organizational access.
- Assess if Dev Ops setup is urgent or can be deferred without affecting progress. For minor changes, notify all about production changes and request a later Dev Ops setup to avoid delays.
- Create a new repository with the following naming convention: 
  - Front-end: `adnet-$projectName-static`
  - Back-end: `adnet-$projectName`

  ## Follow Principles

  See [Effective Engineering](/docs/guides/effective-engineering.md) & follow the principles mentioned in the document.

  ## Planning Document

  Create a planning document before delving into working [Planning Document](/docs/planning/0001-dev-planning-docs.md) & follow the structure mentioned in the document.
