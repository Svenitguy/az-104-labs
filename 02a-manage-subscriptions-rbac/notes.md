# Notes

## Key concepts
- RBAC controls access to Azure resources
- Management Groups organize subscriptions
- Roles should be assigned to groups instead of users
- Custom roles allow least privilege access

## Custom role
- Cloned from: Support Request Contributor
- Removed permission: Microsoft.Support/register/action
- Scope: Management Group level

## Key insight
- Assigning roles to groups improves scalability and security
- Least privilege reduces risk in production environments