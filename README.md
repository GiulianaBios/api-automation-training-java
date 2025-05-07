# API Automation Training

Welcome to the API Automation Training! This repository serves as the foundation for the training, providing a base API Automation Framework and step-by-step guidance for participants to build their API automation skills.

Find the API Framework documentation here.

The training is designed for participants to fork this repository, develop their tests for a mock API, and create Pull Requests (PRs) for feedback and review. Mentors will review PRs regularly, providing feedback and guidance to ensure learning and progress.
Training Objectives

---

1.  **Learn the basics of Java:**
    Understand the fundamental features of Java, including classes, inheritance, etc. These concepts will help you write better, more maintainable code for API automation.

2.  **Understand the Base Framework:**
    Familiarize yourself with the provided Java API Automation Framework using Maven for test execution, Rest Assured for HTTP requests, and JUnit 5 for assertions. Learn how the framework is structured and how to extend it for your testing needs.

3.  **Learn API Automation Concepts:**
    Grasp core concepts like service modeling (encapsulating API endpoints), organizing test cases, setting up environments with .env files, and strategies for functional and non-functional API testing.

4.  **Implement Test Automation:**
    Use the base framework to write tests for real-world scenarios using the Booking API. Implement robust, maintainable test scripts for CRUD operations and edge cases.

5.  **Collaborate Effectively:**
    Develop skills in using Git workflows for version control. Create feature branches, submit Pull Requests (PRs), and respond to feedback from mentors. Learn best practices for working in an asynchronous environment while maintaining high-quality contributions.

---

## Workflow and Guidelines

1.    **Fork the Repository:** Fork this repo to your GitHub account and create a local clone.
2.    **Add collaborators:** Add your mentors as collaborators to the repo.
3.    **Branching:** Use feature branches (e.g., feature/milestone-1) for your changes.
4.    **Pull Requests:** Create PRs for each milestone. Include a description of your changes and any challenges faced. Add your mentor as a reviewer.
5.    **Code Reviews:** Ask someone to review your PRs on demand, providing feedback.
6.    **Feedback:** Address feedback promptly and resubmit your PR.

---

## Training Milestones

Before starting each milestone, create a feature branch with the name of the milestone, e.g.: feature/milestone-1 Follow each Milestone without reading the next one.

## **Milestone 1: Setup and Explore. Service model creation and first tests**

**Objective**:Set up the framework and understand its structure. Create a service model with methods for the Store service.

1. Move to the framework folder:
   ```bash
    cd framework
    ```

2. Install dependencies and set up your environment:

    ```bash
    mvn install
    copy example.env .env
    ```

    **Note:** If the execution does not work because you do not have Maven installed, go to https://maven.apache.org/ and follow the download and install instructions

3. Update .env with the test API base URL:
    ```yaml
    BASEURL=https://restful-booker.herokuapp.com
    ```
4. Explore the framework:
    - Read the [API Automation Framework](https://github.com/GiuliBentancor/api-automation-training-java/blob/main/framework/README.md) Readme.
    - Understand the `ServiceBase` class and its usage in service models.

5. Create a new `BookingService` extending `ServiceBase`.
6. Implement methods in `BookingService` for the following operations:
    - `GET /booking`
    - `POST /booking`
    - `PUT /booking/{bookingId}`
    - `GET /booking/{bookingId}`
    - `PATCH /booking/{bookingId}`
    - `DELETE /booking/{bookingId}`
7. Add request and response models where appropriate.
8. Write the **first test** for the following main scenario:
    - Create a booking and validate the response (`POST /booking`).


**Deliverable**:

- Create a PR with the change, adding a short description of your implementation process.

### Milestone 2: CI/CD Pipeline

**Objective**: Configure and understand the GitHub Action to run tests on each PR and merge to `main`.

1. If you are not familiar with GitHub Actions, do some research to understand the basics, such as workflows, jobs, and steps. Refer to the [GitHub Actions Documentation](https://docs.github.com/en/actions).
2. Explore the `.github/workflows/main.yml` file to understand the workflow triggers and steps.
3. Based on the research you did on GitHub Actions and your experience running the tests in IntelliJ, adjust the Maven line in the main.yml file so the tests are run in the pipeline.
4. Create a new environment called "Testing" in **Settings** > **Environments** > **New environment**
5. Configure the `BASEURL` as an environment variable with value: `https://restful-booker.herokuapp.com`

**Deliverable**:

- Create a PR with a summary of what you learned and confirm that the workflow ran successfully in the Actions tab.

---

### **Milestone 3: Complete the Create Order Suite**

**Objective**: Write tests for the rest of the Create Booking test Suite.

1. Write additional tests for the Create Order (`POST /booking`) endpoint.
2. Include positive and negative tests.
3. Use tags like `@Tag("Smoke")` or `@Tag("Regression")` for test categorization. `@Tag("Smoke")` tests should be the ones that are absolutely required to pass.

**Deliverable**:

- Create a PR with the tests and a brief summary of the scenarios covered.

---

### **Milestone 4: Verify the booking was created**

**Objective**: Make a request to the get booking endpoint to verify the booking was actually created.

**Note**: when testing a POST endpoint you normally don't send the ID (it is generated automatically and returned to you in the response).

1. For your positive tests, after the response assertions, obtain the created booking ID from the response
2. Make a request to the `GET /booking/{bookingId}` endpoint with the booking ID
3. Verify the response of the Get booking endpoint is 200, hence, the booking was created successfully.
4. Since the test where you didn't provide the ID for the POST in the first place should now be failing, follow steps in Milestone 6 for handling it.

**Deliverable**:

- Create a PR with the tests and a brief summary of the changes.

---

### **Milestone 5: Create Test Suites for the rest of the Booking Service**

**Objective**: Write tests for the rest of the Store service following the practices covered above.

1. Write a test suite for each of the remaining endpoints in the Store Service:
    - `GET /booking`
    - `GET /booking/{bookingId}`
    - `PUT /booking/{bookingId}`
    - `DELETE /booking/{bookingId}`
    - `PATCH /booking/{bookingId}`

**Deliverable**:

- **For each test suite**, create a PR with the tests and a brief summary of the scenarios covered.

---

### **Milestone 6: Pre and Post conditions: BeforeEach and AfterEach**

**Objective**: Write Before for pre-conditions and After for post-conditions..

1. Write a [before each](https://junit.org/junit5/docs/current/user-guide/#writing-tests-definitions) in the Get booking test suite.
    1. Add a Before function that creates a booking by calling the right method in the BookingService model.
    2. Obtain and store the booking ID (the variable for this must be declared above the before function).
    3. Use the saved booking ID in the Get Booking test.
2. Write an [after each](https://junit.org/junit5/docs/current/user-guide/#writing-tests-definitions) in the Create booking test suite. This is very useful for cleaning up data after a test execution.
    1. Declare an bookingId variable on top of the test suite
    2. After every positive test, update the bookingId variable with the newly created Booking Id.
    3. Add an AfterEach hook that deletes the created booking by calling the right method in the BookingService model.

**Note**: As the name implies, @BeforeEach and @AfterEach functions run before and after any test of the class, so make sure to not create a test in the class that does not need of said functions, or at least that it is affected by them

**Deliverable**:

- Create a PR with the changes and a brief summary.

---

### **Milestone 7: Verify endpoints basic Performance**

**Objective**: Expand the test suite with basic performance test cases.

1. Add performance checks for the endpoints (e.g., response time < 1000ms).

**Deliverable**:

- Create a PR with the new tests and details covered.

---

### **Milestone 8: Extend to Other Services**
**Objective**: Implement automation for additional services (`Auth`) service.

1. Repeat the previous steps for **Auth** service.

**Deliverable**:

- Create a PR with the new tests and details covered.

---

## Tips for Success

1. **Engage Actively**: Reach out for help if you're stuck or need clarification.
2. **Focus on Quality**: Write clean, maintainable code and meaningful tests.
3. **Learn from Feedback**: Incorporate mentor feedback to refine your implementation.

---
