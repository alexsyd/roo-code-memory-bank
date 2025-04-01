# Living Documentation

## Introduction

Living Documentation is an approach to software documentation that ensures documentation remains accurate and up-to-date by evolving naturally with the software it describes. Unlike traditional documentation that quickly becomes outdated, Living Documentation is tightly integrated with the development process and often generated automatically from executable specifications or the codebase itself.

At Smartphonekey, we use Living Documentation to reduce the documentation burden while ensuring that all stakeholders have access to accurate and current information about our systems.

## Core Principles

### Documentation as a Product

We treat documentation as a first-class product that provides value to its users:
- It has defined audiences with specific needs
- It is designed with usability in mind
- It evolves based on feedback
- It is maintained and improved over time

### Single Source of Truth

All documentation should have a single source of truth:
- Code is the ultimate source of truth for technical details
- Tests document behavior
- Requirements are captured as executable specifications
- Avoid duplication that leads to inconsistencies

### Documentation is a Team Responsibility

Documentation is not the sole responsibility of a dedicated technical writer:
- Developers document their code and APIs
- QA documents test cases and scenarios
- Product owners document requirements and business rules
- Everyone contributes to keeping documentation current

### Automation Over Manual Maintenance

Wherever possible, we automate the creation and maintenance of documentation:
- Generate API documentation from code
- Create behavior documentation from tests
- Extract diagrams from architecture definitions
- Use tools that maintain documentation as code changes

## Types of Living Documentation

### Executable Specifications

Executable specifications serve as both tests and documentation, bridging the gap between business requirements and technical implementation:

#### Behavior-Driven Development (BDD)

We use BDD frameworks like Cucumber to create executable specifications that:
- Are written in a business-readable language (Gherkin)
- Act as automated tests verifying system behavior
- Provide documentation of how the system works
- Are updated whenever behavior changes

Example Gherkin specification:

```gherkin
Feature: Credit card payment

  Business need: As an online shopper
  I want to pay with my credit card
  So that I can complete my purchase immediately

  Scenario: Successful payment with a valid credit card
    Given the user has items in their shopping cart
    And the user has entered valid credit card details
    When the user confirms their purchase
    Then the order should be placed successfully
    And a confirmation email should be sent to the user
    And the user's credit card should be charged the correct amount
```

#### Specification by Example

Based on Gojko Adzic's approach, we use concrete examples to clarify requirements:
- Examples are created collaboratively by business and technical team members
- Examples form the basis of automated tests
- Tests generate documentation showing how the system behaves
- Documentation remains current because tests must pass for delivery

### Automated API Documentation

For our APIs, we maintain documentation that is automatically generated from the codebase:

- OpenAPI/Swagger specifications for REST APIs
- GraphQL schema documentation for GraphQL APIs
- Auto-generated client libraries for different programming languages

This ensures that API documentation is always accurate and reflects the current state of the implementation.

### Code Documentation

We maintain high-quality code documentation by:

- Using meaningful names for variables, functions, and classes
- Writing clear, concise comments explaining "why" rather than "what" 
- Adding documentation comments that can be extracted into reference documentation
- Creating reference documentation with tools like JSDoc, Javadoc, or Swagger

### Architecture Documentation

We use tooling that keeps architecture documentation in sync with the actual system:

- Architecture Decision Records (ADRs) to document key decisions
- C4 model diagrams generated or validated from code
- Database schema visualizations created from the actual database

## Tools We Use

At Smartphonekey, we utilize several tools to implement Living Documentation:

### BDD and Testing Tools

- **Cucumber**: For executable specifications and behavior documentation
- **Serenity BDD**: For enhanced reporting and living documentation from tests
- **JUnit/Jest**: For code-level specifications and examples

### API Documentation

- **Swagger/OpenAPI**: For REST API documentation
- **GraphQL Playground/GraphiQL**: For interactive GraphQL documentation

### Code Documentation

- **JSDoc/Javadoc**: For code-level documentation
- **Markdown**: For general documentation that lives alongside code

### Visualization Tools

- **PlantUML/Mermaid**: For diagrams as code
- **C4-PlantUML**: For architecture visualization

## Implementation Process

### 1. Collaborative Specification

Before development begins:
- Business stakeholders, developers, and QA collaborate to define requirements
- The team creates examples that illustrate the desired behavior
- Examples are formalized in Gherkin or another executable specification format

### 2. Test-First Development

During development:
- Developers implement features guided by executable specifications
- Specifications act as automated tests that verify implementation
- Tests and documentation evolve together as understanding improves

### 3. Continuous Documentation

As part of our CI/CD pipeline:
- Executable specifications are run with each build
- Documentation is automatically generated from passing tests
- API documentation is updated based on code changes
- Reports highlight areas where documentation is incomplete or tests are failing

### 4. Review and Feedback

After features are implemented:
- Stakeholders review the generated living documentation
- Feedback leads to improvements in both code and documentation
- Documentation gaps are identified and addressed

## Best Practices for AI Agent Interaction

When AI agents assist with code and documentation, follow these guidelines:

### For AI Agents

- Check existing documentation patterns before creating new ones
- Follow established documentation structures and formats
- Generate both code and its associated documentation
- Include examples in documentation to clarify usage
- Ensure generated documentation reflects actual implementation

### For Developers Working with AI Agents

- Provide context about existing documentation practices
- Review AI-generated documentation for accuracy and completeness
- Use AI to help maintain consistency across documentation
- Ask AI to generate documentation in multiple formats when needed

## Benefits of Living Documentation

- **Reduced Documentation Burden**: Documentation becomes a natural byproduct of development activities
- **Always Up-to-Date**: Documentation is automatically updated as code changes
- **Improved Collaboration**: Shared understanding between business and technical teams
- **Better Onboarding**: New team members can understand system behavior quickly
- **Enhanced Quality**: Tests that serve as documentation ensure system behavior is verified
- **Streamlined Compliance**: Living documentation provides evidence for audits and regulatory requirements

## Challenges and Solutions

### Challenge: Initial Setup Investment

**Solution**: Start small with one project or area, demonstrate the value, then expand incrementally.

### Challenge: Changing Team Habits

**Solution**: Provide training and mentoring on new practices, celebrate successes, and demonstrate time saved.

### Challenge: Tool Integration

**Solution**: Choose tools that integrate well with existing development workflow and CI/CD pipeline.

### Challenge: Maintaining Quality

**Solution**: Include documentation quality in code reviews and define clear standards for what good documentation looks like.

## Conclusion

Living Documentation represents a fundamental shift in how we approach documentation at Smartphonekey. By making documentation an integral part of our development process rather than an afterthought, we ensure that our documentation remains accurate, useful, and maintainable. This approach not only improves the quality of our documentation but also enhances collaboration, reduces waste, and helps us deliver better software more efficiently.