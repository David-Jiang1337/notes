Continuous delivery and continuous deployment are very similar in principle, with the only key difference being that in continuous delivery, deployment of updated software must be done manually, whereas continuous deployment is where deployment is also automated.

In both continuous delivery and continuous deployment, developers deploy incremental changes to the codebase via escalating automated tests:
- **Build & Unit Tests** are automatically run when developers push changes.
- **Platform Tests** then ensure that the changes are compatible with all tested platforms.
- **Acceptance Tests** are then conducted to ensure that the changes align with key stakeholder (i.e. business or user) goals.
- **Post-Deploy Tests** ensure the software is working as intended once real users start using the updated software.
Should tests fail at any of these stages, the changes may be pushed back for revision or reevaluation.