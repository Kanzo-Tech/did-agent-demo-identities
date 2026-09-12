# did-agent-demo-identities

Public identity resources, service descriptors and Verifiable Credentials used by the `did:agent` technical demonstrator.

The implementation of the method and its resolver is available in [`Kanzo-Tech/did-agent-poc`](https://github.com/Kanzo-Tech/did-agent-poc).

## Demonstration agent

- Agent identifier: `planner-01`
- DID: `did:agent:web:raw.githubusercontent.com:Kanzo-Tech:did-agent-poc:main:demo:controller:planner-01`
- Controller: `did:web:raw.githubusercontent.com:Kanzo-Tech:did-agent-poc:main:demo:controller`
- Operational profile: `basic`
- Lifecycle status: `active`

## Repository contents

The repository contains:

- The public DID Document of `planner-01`.
- Its P-256 operational public key.
- Interaction, credential and contract service descriptors.
- Two controller-issued Verifiable Credentials.
- The compact JWS representations of those credentials.

No private keys are stored in this repository.

## Verifiable Credentials

The controller has issued two demonstration credentials for the agent.

### AgentRegistrationCredential

This credential asserts that `planner-01`:

- Is governed by the declared controller.
- Uses the `basic` agent profile.
- Has an active registration status.

Files:

```text
agents/planner-01/credentials/agent-registration.vc.json
agents/planner-01/credentials/agent-registration.vc.jwt
```

### AgentCapabilityCredential

This credential asserts that `planner-01` has the task-planning capability and associates the `plan` action with its interaction service.

Files:

```text
agents/planner-01/credentials/agent-capability.vc.json
agents/planner-01/credentials/agent-capability.vc.jwt
```

## Credential discovery

The agent DID Document declares an `AgentCredentialService` whose endpoint resolves to:

```text
agents/planner-01/services/credentials.json
```

This index publishes the credential identifiers, types, issuer, format and locations of their readable and signed representations.

## Security model

The credentials conform to the Verifiable Credentials Data Model v2.0 and are secured as compact JWS documents using `ES256`.

Their protected `kid` header references:

```text
did:web:raw.githubusercontent.com:Kanzo-Tech:did-agent-poc:main:demo:controller#controller-key-1
```

The corresponding public JWK is published in the controller DID Document and authorized through `assertionMethod`. The private signing key remains encrypted and outside version control.

These resources form part of an experimental proof of concept and are not intended for production use.