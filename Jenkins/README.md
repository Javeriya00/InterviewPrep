# Jenkins Interview Prep

This section contains interview questions and answers related to Jenkins, a popular automation server used for continuous integration and continuous delivery (CI/CD).

## Questions & Answers

### 1. What is the difference between a declarative pipeline and a scripted pipeline in Jenkins?

- **Declarative Pipeline**: It is a simpler, more structured pipeline syntax with best practices for CI/CD workflows. It is easier to use and maintain but less flexible.
- **Scripted Pipeline**: It uses full Groovy scripting, allowing for more flexibility and customization. However, it is harder to maintain and more complex.

### 2. What is a Jenkins pipeline, and what are its types?

A Jenkins pipeline automates the continuous integration/continuous delivery (CI/CD) lifecycle. It can be of two types:
- **Declarative Pipeline**: Easier to use, structured syntax.
- **Scripted Pipeline**: Groovy-based, more flexible but complex.

### 3. How would you secure a Jenkins server?

- Use **SSL encryption** for secure communication.
- Implement **role-based access control (RBAC)** to restrict permissions.
- Enable **credentials management** for handling sensitive data securely.
- Use **firewalls/VPNs** for restricted access.

## Further Reading
- [Jenkins Documentation](https://www.jenkins.io/doc/)
