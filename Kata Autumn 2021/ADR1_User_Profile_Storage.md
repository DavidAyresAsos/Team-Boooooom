# [ADR1] - User Profile Storage

## Status: Proposed | Accepted | Superseeded

## Context:

A user within the system can have 3 different states:

- Transactional Customer: Farmacy Foods user.
- Engaged Customer: Farmacy Family and Farmacy Foods.
- Community User: Farmacy Family Foods.

As such, a user needs to "exist" within at least one of the systems but could in theory be in both. This runs the risk of having split user profiles across the applications.

There will naturally be shared attributes between the systems (Name, Address, Email, etc.) but Farmacy Foods and Farmacy Family will have attributes only specific to their contexts.

Having these split user profiles presents a design challenge where a user needs to have a consistent login across both systems [RQ9] but we don't want orphan user profiles where they cannot access the other system.

On top of this, the Farmacy Foods user profile data has very granular profile customisation [RQ7] which is only relevant to Farmacy Family.

## Decision:

All users, when registering through Farmacy Family, will need to be added into Farmacy Foods. That will be their base user account. Farmacy Family will then hold user profile data within it's own scope in a dedicated data store. This allows them to log into both systems with one single account (feeding into the current IAM design). [RQ9] will then be delivered with a very abstract API for this data, where the business logic for sharing and handling this data sits within Farmacy Family modules. The end concrete implementation of this could sit within AWS Cognito although it's limit of 25 custom user attributes could be limiting although this is a technical implementation concern and the application will be designed so that it's not focused on the underlying implementation.

## Consequences: 

We run the risk of having user profile data split between AWS Cognito and a custom data store. This could present an issue where user data could become orphaned if a user is deleted in Farmacy Foods but not Farmacy Family so reconiliation needs to be considered, or "User Deleted" type events need to start being sent (which impacts the Farmacy Foods implementation). We accept that going down this approach increases the complexity of the Farmacy Family implementation but should be isolated in the Farmacy Family domain so data consumerssimply need to query and trust the data they receive.

This then gives Farmacy Family control over the cache of the data where "all" queries to the user profile settings from Farmacy Family need to be real time, or against a calculated table with the latest view of the data so any user changes are immediately populated on direct queries while background tasks tidy up any calculated/cached data stores. This event driven approach is only the concern of the  Farmacy Family domain.
