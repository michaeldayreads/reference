### Principles

#### Defense In Depth
Even the best firewall can be defeated by social engineering.

Must be balanced against Simplicity Principle

#### Positive Security Model
Whitelist what is allowed very specifically, deny everything else.

#### Fail Securely
Remember Exceptions in addition to allow / disallow. Failure should follow the same path as disallow.

Follow a policy of least privilege. (Create users with properly limited permissions, no root, etc.)

#### Avoid Security By Obscurity
It should not be necessary to keep the algorithm secret, keeping the key secret should be sufficient.

Uncommon ports.

Closed Source.

#### Keep Security Simple
Verifiable, economy of mechanism.

Prefer clear code over clever code.

#### Detect Intrusions
Log events
Monitor logs
Clear response procedure


#### Don't Trust Infrastructure
Distrust internal requests, servers etc. Leverage what they have, but do not rely on it exclusively.


#### Don't Trust Services
Be skeptical of what services provide. Validate it as best as possible, think about irregular patterns, negative information. 


#### Establish Secure Defaults
Admins must *opt out* rather than *opt in* to the more secure option.