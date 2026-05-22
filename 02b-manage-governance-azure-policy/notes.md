# Notes

## Key concepts
- Tags provide metadata for Azure resources
- Azure Policy enforces organizational standards automatically
- Policies can deny, audit, or modify resources
- Resource Locks help prevent accidental deletion or modification
- Governance becomes critical as cloud environments scale

## Tags
- Resource Group tag:
  - Cost Center = 000
- Tags improve:
  - Cost tracking
  - Ownership visibility
  - Resource organization
  - Reporting

## Azure Policy
### Policy used
- Require a tag and its value on resources
  - Effect: Deny
  - Prevented resource creation without required tag

### Inheritance Policy
- Inherit a tag from the resource group if missing
  - Effect: Modify
  - Automatically applied tags to child resources

## Resource Locks
### Lock configuration
- Lock Name: rg-lock
- Lock Type: Delete

### Result
- Prevented accidental deletion of the Resource Group

## Key insight
- Azure governance combines tags, policies, and locks to improve operational control and security in enterprise environments.