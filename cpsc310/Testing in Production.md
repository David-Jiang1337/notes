When software is being used by a large population of real users, the behavior of the software can be tested in ways that were not possible pre-release. The practice of testing in production seeks to discover bugs or gauge user acceptance of features in a way that is not possible with [[Continuous Integration|CI/CD]] alone. 

# Feature Flags
Feature flags are boolean values that programs use to dynamically enable or disable certain features for certain users. Features are localized and independent behavior. A key property of feature flags is that they can be toggled in an actively running environment without making changes to the code, often via a configuration file.

# Canary Releases
Canary releases are a process where developers present new changes to a small proportion of the user base, tracking telemetry to see how the changes affect the performance or other characteristics of the program. Typically, canary releases are designed to revert automatically should they detect that the release significantly degrades behavior.

# Chaos Engineering
Chaos engineering seeks to validate the reliability of a system by simulating failures and monitoring the behavior of the system under these simulated failures. For instance, chaos engineering might include inducing failures in a production instance or artificially increasing latency to see how the system responds.

# A/B Testing
A/B testing typically implements alternative versions of a system via feature flags or separate deployments that the router chooses between for individual users. By separating users into groups and providing each group with a different version of the system, developers can monitor and compare telemetry and outcomes between different ideas they may have.