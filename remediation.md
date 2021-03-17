## Remediation - Putting Nodes into a Safe State

At it's core, remediation (aka. fencing) turns a question _Can our peer cause
data corruption?_ into an answer _no_ by isolating it both from incoming
requests and persistent storage.

Only after this is achieved do we become concerned with restoring cluster
capacity.

In cloud environments, where replacing a whole machine takes seconds, the most
common apprpoach is to use something like [Machine API]() to deprovision the
failed node and replace it with a new one.

However not all k8s clusters come with the Machine API configured, and adding it
retrospecitvely is both complicated and not always possible and/or desirable.

Additionally, physical machines can't pop into existance via an API call and
take much longer to provision.

It is therefor clear that there is no one-size-fits-all solution for
remediation.  For this reason, the [ExternalRemediation API]() was established to
allow remediation mechanisms to exist, even within a single cluster, without
creating conflicts.
