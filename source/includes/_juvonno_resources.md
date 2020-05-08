# Juvonno Resources

Each Resource represents an actual Juvonno Business Object, which can be accessed through a collection of URLs.

For example, /api/customers is the URL responsible for all operations on the "Customer Resource", which in turn is a "Customer Object" in our backend server.

Each object / resource will always have a unique **Juvonno ID**. It is up to users to choose to store our IDs into their application.  

> An example Customer Resource:

```json
{
  "customer": {
    "id": 21,
    "num": {
      "chart": "CHART1234"
    },
    "first_name": "John",
    "last_name": "Doe"
  }
}
```

### Additional Mapping Fields

Sometimes we also allow an additional field which users can use to match up against their own IDs in their system. 
For example, the Customer Resource on the right has a **Juvonno ID** of **21** and an additional identifier **chart > num** of **"CHART1234"** (which can represent the Customer's ID in your system).

It is not always the case that we provide an additional mapping field. One example is the "Appointment" Resource. "Appointment" does not have a "number" or a "name". The only way to distinguish between unique appointments in Juvonno is based on theirs Juvonno ID.
Hence in some cases it relies totally on the Juvonno ID in order for a resource to be able to get retrieved or modified. Therefore, though it is not mandatory, but we do **recommend storing this ID field into your own system**.

### Communication Between Resources
Resources in Juvonno communicate with each other through their <b>unique identifier(s)</b>. You can always guarantee communication between resources using their  **Juvonno ID**.

#### Example
If we want to assign Branch "Brandon Clinic" to Staff Member "Jane Doe", we can use the branch's Juvonno ID in the customer's update request body like this: 
<code>
{
    "branch_id": 1
}
</code>
