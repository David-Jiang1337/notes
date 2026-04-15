Information security (InfoSec) encompasses a wide swath of software design, from preventing software exploits to mitigating the effect of social engineering, but the essential goal of information security is that we want our system to do what we intended it to do, and to be incapable of doing what we do not wish it to do. More concretely, information security usually involves deciding rules around who may access what information (e.g. user data or the source code) and making sure people cannot get around those rules in practice. This includes preventing malicious actors from acquiring sensitive data, but also to preventing untrained users accidentally undermining the system.

# Requirements
Information security can be split into four high-level requirements:
- **Confidentiality**: the only people who should be able to access a certain piece of data are the people we intend to access that data (i.e. only a system administrator and the user themselves, and nobody else, should be able to see a user's password).
- **Integrity**: data should only be able to be modified by the people we intend and only in the ways we intend.
- **Availability**: data should be accessible to intended parties whenever we intended for it to be (i.e. we must prevent DDOS attacks which stop people from accessing data they should be able to).
- **Accountability**: the developers of a system should be how and when people are interacting with sensitive data, and who is doing so.
# Steps of Enforcing Security
and the process of ensuring these four requirements are met is done through four high-level stages:
- **Understanding**: information security is based on enforcing intended patterns of data access, so the first step to securing a system is for us, the developers, to fully understand just what we intended for our system to do, and what we don't intend our system to do.
- **Analysis**: once we understand just what we intend for our system to do, we must consider what kinds of people might wish to undermine our infosec, which parts of our system they may wish to target, and the legal, economic, and safety risks we may incur if they succeed.
- **Mitigation**: once we have analyzed where our system needs to be hardened to attack, we must actually implement our system in a way that is resistant to the attack vectors we came up with. A common method of mitigation is to reduce the possibility space of how a user is able to interact with our system, while still ensuring intended functionality stays intact.
- **Validation**: finally, once we have hardened our system against attack, we need to test our security systems by simulating attacks and conducting security reviews to ensure our mitigation steps have been successful.

# STRIDE Analysis
To describe the various ways in which an attack might take place, Microslop developed a threat model acronym called STRIDE:
- **Spoofing**: an attacker may pretend to be another subject by using their authentication credentials (violate accountability).
- **Tampering**: an attacker may seek to modify data they are not allowed to modify like persistent data or network data (e.g. rowhammering readonly data) (violate integrity).
- **Repudiation**: an attacker may seek to leave other parties unable to prove that they performed an attack by preventing themselves from being traced (violate accountability).
- **Information disclosure**: an attacker may seek to read information they are not allowed to access (e.g. read packets on a network that were not intended for them)(violate confidentiality).
- **Denial of service**: an attacker may seek to remove access to the service by users (e.g. overloading servers with fake requests) (violate availability).
- **Escalation of privilege**: an attacker may seek to become trusted by a system so that they may compromise the system (e.g. becoming a trusted contributor to an open source project so that their backdoor can be merged into the codebase) (basically violates any and all four principles).

# Defense Principles
To defend against the attack vectors described above, developers have come up with several security principles that help mitigate the risk of attack:
- **Defense in depth**: security should be implemented at every level of the system, so that a small violation in security does not make it easier for attackers to commit more significant violations.
- **Least privilege**: access permissions should be fine-grained to permit the exact types of accesses intended by a system and nothing else, this is done by carefully implementing roles and access control lists, which is only possible if developers have a clear understanding of what their system should and should not do.
- **Separation of duties**: a single authorized user should not have access to too many sensitive/critical actions, and critical roles should be split among many individuals or teams. This is especially important to minimize the amount of damage a disgruntled employee can do to a system.
- **Strong authentication**: authorized users should have robust authentication that is not easily spoofed by malicious actors. Strong authentication often includes multi-factor authentication (MFA), so that a single leaked credential like a password does not lead to sensitive permissions falling into the wrong hands.
- **Non-repudiation**: a system should closely track sensitive actions made by users and make it as difficult as possible for users to not leave a trace when performing important tasks. However, non-repudiation also means that the system needs to be more secure in the other defense principles, as having detailed logs of sensitive actions can itself be a form of sensitive information that needs to be protected.