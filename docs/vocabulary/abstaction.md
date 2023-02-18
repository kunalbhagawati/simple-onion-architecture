## Abstraction
Throughout this whole journey, we don't use the word abstraction in the context the SOLID or some particular coding style.  

No, here, an abstraction is basically the "level" **along with** "context" of what we are talking about.

An abstraction is basically the answer to the question: How much understanding or scope is enough to explain one particular level of the problem.

# Abstraction Layer

Instead of theory, let's take an example to understand abstraction layers:

Say we want to build the user login flow for some SaaS product.

> Sign-up a new user using some social login (google/facebook).  
> On success: If it's a new user, send them an onboarding email and redirect to the onboarding wizard.  
> If it's an existing user redirect them to their dashboard. 
> On failure: send back to the login screen with an error popup.

Drilling down on each "level" of context & understanding, we get: 

--> These are things the non-engineering people can understand easily. Think of it this way: If your Product Manager has never written code, but can understand surface level engineering, they'll get it.

### Top-most Business / Product rules layer 
1. Check if the user exists with the given credentials.
2. If `yes`, check if onboarding is already done.
   1. If `no`, send an onboarding email and re-direct to the onboarding wizard.
   2. If `yes`, redirect to user's dashboard. 
3. If `no`, try to create a new user and do step 2.1.
4. If that also fails, redirect to login screen and show an error.

### Lower-level Business / Product rules layer
1. [Breaking down 1. above] 
   1. Figure out which data store to fetch the user from. Cache? Primary DB?
   2. Ask the data store to get the user which matches the given credentials.
2. [Breaking down 2.1 above] 
   1. Get the type of user.
   2. Figure out which particular onboarding wizard to show for that type of user.
   3. Get the mail client which we want to use (mailchimp vs sendgrid).
   4. Send an email with an expiry to validate the user 
3. ... (and so on)

--> Beyond this point, only an engineer can understand properly.

### Top-most level of non-business logic
1. [Breaking down 1. above]
   1. Get the user from redis using the redis client that match the key in the hashmap for the identifier given.
2. [Breaking down 2.1 above]
   1. Check the user type.
   2. Check the RBAC tables for the user roles.
   3. Consolidate this information into a `user.type` data structure with sufficient context for the layer above.
3. [Breaking down 2.4 above]
   1. Use the email client to open a new connection.
   2. Send a request to the servers, with a exponential back-off for failures.
4. (... and so on)

### even lower level
1. [Breaking down 1.1. above]
   1. Ask the redis driver for a new connection thread.
   2. Check if the connection has bandwidth.
   3. Send data over the redis protocol for the `HGET` query.
2. (... and so on)

### we can go lower
1. Check if OS has open socket for the process to give on time-sharing basis.
2. (...)

---

**If you notice, each of these levels in the headings is its own flowchart.**  

Each _individual part_ of the flowchart of one layer breaks down into a more complex flowchart somewhere in a lower layer.

At the topmost level is the simplest flowchart, and the lowest level will be the biggest flowchart.

Thus, at the lowest layer, we have a system-of-systems, and at the topmost layer that same thing becomes one system.
