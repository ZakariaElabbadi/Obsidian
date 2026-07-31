# Salesforce Summary

## Object Relationships & Flow Traversal

### Golden Rule of Parent-Child Relationships
*   The object that **contains** the Lookup field is the **Child**.
*   The object **referenced** by the Lookup field is the **Parent**.
    *   **Example:** In a `Contact` record, `AccountId` is a Lookup field.
        *   Child = `Contact`
        *   Parent = `Account`

### Traversing Relationships in Salesforce Flows

#### Child → Parent (Direct Traversal)
*   Access parent record fields directly from the child record.
*   **No "Get Records" element or Loop required.**
*   **Examples:**
    *   `$Record.Account.Name` (to get the Account Name from a Contact or Opportunity)
    *   `$Record.Owner.Email` (to get the Owner's Email from any record)

#### Parent → Children (Requires "Get Records" + Loop)
*   To retrieve related child records from a parent, you need to:
    1.  Use a **"Get Records"** element to query for the child records.
    2.  Filter these records based on the parent's ID (e.g., `AccountId = $Record.Id`).
    3.  If "Get Records" returns multiple records (a **Collection**), you must use a **"Loop"** element to process each child record individually.

### Flow Golden Rules and Best Practices
1.  **Child → Parent:** Use direct access (e.g., `$Record.Account.Name`).
2.  **Parent → Child:** Requires "Get Records" + Loop (if a collection is returned).
3.  **Collections:** Are lists of records and always require a Loop to process each record.
4.  **Updating records:** Perform updates on a collection **once** after the loop, not inside it, for bulk efficiency.
5.  **Creating records:** Create records within the loop when processing a collection of new records.
6.  **Avoid unnecessary "Get Records" elements:** Especially for retrieving parent records, as direct traversal is more efficient.
7.  **Use Entry Conditions:** For record-triggered flows to optimize performance.
8.  **Think about relationships:** Before adding Flow elements.

### Common Mistakes to Avoid
*   **Confusing Parent/Child:** e.g., thinking Contact is the parent of Opportunity (they are siblings under Account).
*   **Using "Get Records" for Parent:** Always use direct traversal for parents.
*   **Forgetting to Loop a Collection:** Collections must be looped to process individual records.
*   **Filtering Contacts by OwnerId for an Account:** Use `AccountId = $Record.AccountId` to filter contacts related to a specific account.
*   **Confusing OwnerId with AccountId:** `OwnerId` references a `User` record; `AccountId` references an `Account` record.

### Example Flow Scenario: Opportunity Closed Won
When an Opportunity becomes "Closed Won":
*   Send an email to the Opportunity Owner (direct traversal: `$Record.Owner.Email`).
*   Create one Task for every Contact in the related Account (requires "Get Records" for Contacts, then a Loop to create tasks).
