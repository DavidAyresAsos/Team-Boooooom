# Evaluation of Requirements

The initial brief of the Solution covered of many different requirements spread across a larger document. Below we call out the key requirements we have collated from the document and what we deem to be the deliverables for them with high level acceptance criteria.

## Primary Goals

The Primary Goals help ground the Solution Design to what the client ultimately wants and the top level business metrics the performance of the system would evaluated against. If we can't evidence how the Solution meets these goals, then as Architects we have failed the client.

**[PG1]** Develop relationships betweeen engaged customers and nurture those relationships.

**[PG2]** Convert transactional customers to engaged customers.

**[PG3]** Generate analytical data from medical informatio to demonstrate the benefits of Farmacy Foods.

These goals have been given reference values that will be used throughout the Solution Design to highlight how we ultimately tie back to these goals.

## Requirements

The Requirements have been tagged with a code in the same way the Primary Goals have to help highlight which parts of the Solution Design relates to them.

**[RQ1]** Add a new system to manage customer profiles, allowing community engagement, personalization around preferences and dietary needs.

*Design Approach:* Follow the current design ethos for Farmacy Food but keep the User Profile Domain Model in it's own isolated data store. Consideration needs to be given to user changes to their profile and how this affects consumers of their data.

**[RQ2]** Support geographical trend analysis to hone Farmacy Family’s ability to optimize the foods delivered to fridges (an additional integration point TO Farmacy Foods).

*Design Approach:* Geogrpahical data will need to form part of the User Profile Domain Model. We will need to offload data in an anonymised format into a location where analysis can be performed abstracted from the operation of the customer facing application.

**[RQ3]** Support both push and pull models for community engagement. In other words, Farmacy Family will manage forums, emails, and create connections between similar demographics. Farmacy Family needs transactional member information for outreach purposes. The engagement model includes subscriptions, forums, reference material, class information, and other media that supports Food-as-medicine.

*Design Approach:* Identify what we should build and what Farmacy Family should "buy" (including Open Source). Need to consider the fine grained user profile requirements. Trasnactional member information hints towards Event Sourcing as per the Farmacy Food design.

**[RQ4]** eDietian has access customer profile to improve advice and monitoring of customers. Additionally, the customer and dietitian can interact via messages.

*Design Approach:* eDietitian will require their own role/area within the ecosystem. Need to consider user's preferences around what data they do/don't want to share. We need to think about protecting client data foremost and perhaps share data in an anonymous way.

**[RQ5]** Farmacy Family wants to improve the distribution and potential food waste from having the wrong mix of foods in a particular fridge.

*Design Approach:* This would be a background process which would need data from Family Foods to support. It would ultimately be a geographical breakdown trend analysis on meals sold/soiled. A solid Analytics approach, with a suitable data lake and ETL tool would provide the tools for a Data Scientist to mine.

**[RQ6]** Farmacy Family will include medical profile information and the ability to share information with medical service providers.

*Design Approach:* Without being experts within the medical service provider field, a user driven business process could deliver this functionality.

**[RQ7]** Farmacy Family customers can customize how much profile information they want to allow the community to see, at a finegrained level.

*Design Approach:* Discussed above across other requirements but any SaaS/Open Source solution we use has to adhere to this complex matrix of data permissions. This is key to the customer centric approach that needs to be applied. Any mistakes here would impact the credibility of Family Foods which we have to avoid. All data access needs to constantly hook into the real time view of this data.

**[RQ8]** Farmacy Family has relationships with third party providers (clinics, doctors, etc) that have access to more analytical data to improve engagement (for example, regional dietary observations).

*Design Approach:* These users should either have their own portal or access to reporting tools that cover a subset of data in a Data Lake. IAM is integral to this so the right providers can only access the correct data. Links into [RQ7].

**[RQ9]** Add Farmacy Family user interface to existing Foods interface, which is currently a Reactive monolith. Create a holistic UX for both food and Farmacy Family to support engagement model.

*Design Approach:* Follow the ethos from Farmacy Foods and extend where allowed. Business logic around user data should be abstracted away from this into Farmacy Foods specific capabilities so that consumers of the data simply need to retrieve data and not perform anything on the data while accessing it. The UX screams web components.

## Non-Functional Requirements

The Non-Functional Requirements are contained with the document but are called out more as footnotes. These need to be considered as part of the design, so are being listed here as NFRs. These don't follow the traditional design ethos of Performance, Thorugh-Put and Load due to the nature of the Kata.

**[NFR1]** The new system must seamlessly incorporate into Farmacy Foods.

*Design Approach:* Utilise assets that Farmacy Foods already has established, making them cross cutting technologies. Design with the assumption that changes to Farmacy Foods should be at a minimum and heavy lifting will sit within Farmacy Family. UX should have the same look and feel to the point where customers should be able to seamlessly transverse the applications without noticing they've moved between Farmacy Family and Farmacy Friends.

**[NFR2]** Improved use of analytics driven through the new integration of Farmacy Family will help gather new investors and prove better dietary outcomes in member communities.

*Design Approach:* This forms a concrete reporting requirement. We need to be able to evidence key metrics and undertsand the baseline data Farmacy Family will need to report on this.
