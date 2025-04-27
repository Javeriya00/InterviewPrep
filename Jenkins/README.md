# Jenkins Interview Prep

This repository contains interview questions and answers related to Jenkins, a popular automation server used for continuous integration and continuous delivery (CI/CD).

## Questions & Answers

### 1. What is the difference between a declarative pipeline and a scripted pipeline in Jenkins?

- **Declarative Pipeline**: A simpler, more structured pipeline syntax that is easier to use and maintain. It enforces best practices and is less flexible.
- **Scripted Pipeline**: Fully Groovy-based, providing full flexibility and control over the pipeline's flow. It allows for more complex logic but is harder to maintain and debug.

### 2. What is a Jenkins pipeline, and what are its types?

A Jenkins pipeline automates the CI/CD lifecycle and can be of two types:
- **Declarative Pipeline**: A structured and user-friendly syntax, recommended for most Jenkins setups.
- **Scripted Pipeline**: Groovy-based, offering greater flexibility but requires more expertise in scripting.

### 3. How would you secure a Jenkins server?

- Use **SSL encryption** for secure communication.
- Implement **role-based access control (RBAC)** to restrict permissions.
- Enable **credentials management** to securely handle sensitive data.
- Use **firewalls/VPNs** to restrict access.

### 4. How do you manage sensitive data (e.g., passwords) in Jenkins?

Use the **Jenkins Credentials Plugin** to securely store and manage sensitive data (API keys, passwords, etc.). You can also utilize environment variables or credentials binding during pipeline execution.

### 5. How would you handle a scenario where multiple microservices need to be deployed through the same Jenkins pipeline, but each microservice uses a different tech stack?

To handle multiple tech stacks in a single pipeline, I would:
1. Separate common tasks (e.g., code checkout, unit tests) from tech-stack-specific tasks.
2. Use conditional stages or jobs for each tech stack (e.g., `npm install` for Node.js, `mvn clean install` for Java, `pip install` for Python).
3. Modularize the pipeline with reusable steps or templates (e.g., Jenkins Shared Libraries) to avoid duplication and improve scalability.

### 6. How would you handle a scenario where a Jenkins pipeline job fails due to a specific service not being available?

For service failures, I would:
1. Inspect the logs to identify the root cause (e.g., deployment issues, configuration errors).
2. Use Kubernetes commands like `kubectl describe pod <pod-name>` to check the health of the service.
3. Consider retry logic or rolling back to a stable version if the issue persists.
4. Implement post-build actions in Jenkins for retries and notifications to address the failure without halting the pipeline.

### 7. How would you ensure that a Jenkins job is triggered only when changes are made to the repository?

To trigger Jenkins jobs only when changes are made:
1. Set up webhooks in the repository (e.g., GitHub or GitLab) to send push or pull request events to Jenkins.
2. Configure Jenkins to use Git SCM as the source repository and optionally enable Poll SCM to check periodically for changes.

### 8. What is a Shared Library in Jenkins?

A **Shared Library** is a set of reusable Groovy scripts, jobs, or functions stored in a Git repository. It allows you to reduce duplication and reuse common functionality across multiple Jenkins pipelines.

### 9. Use of try-catch-finally in Jenkins pipelines?

The **try-catch-finally** block in Jenkins is used for error handling:
- **try**: Defines code to attempt.
- **catch**: Handles failures or exceptions.
- **finally**: Executes cleanup actions, regardless of whether an error occurred.

## Further Reading

- [Jenkins Documentation](https://www.jenkins.io/doc/)
