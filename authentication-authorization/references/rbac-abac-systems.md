# RBAC and ABAC Access Control Systems

Design and implement role-based and attribute-based access control for fine-grained authorization.

---

## Role-Based Access Control (RBAC)

### Core Concepts

RBAC assigns permissions to roles, and roles to users. Users inherit permissions from their assigned roles.

**RBAC Components:**
| Component | Description | Example |
|-----------|-------------|---------|
| User | Entity requesting access | `john@example.com` |
| Role | Named collection of permissions | `editor`, `admin` |
| Permission | Specific allowed action | `posts:write`, `users:read` |
| Resource | Object being accessed | `blog_post`, `user_profile` |

### Role Hierarchy Design

```
Super Admin
  └── Admin
       ├── Manager
       │    ├── Editor
       │    │    └── Viewer
       │    └── Moderator
       └── Analyst
            └── Viewer
```

**Inheritance Rules:**
- Higher roles inherit all permissions of lower roles
- A user can have multiple roles (union of permissions)
- Deny overrides allow in conflict resolution

### Permission Naming Convention

Use `resource:action` format for clarity:
- `users:read` — View user profiles
- `users:write` — Create/update users
- `users:delete` — Remove users
- `posts:publish` — Publish draft posts
- `billing:manage` — Manage billing settings
- `*:*` — Superadmin (all resources, all actions)

### Database Schema for RBAC

```sql
-- Core tables
CREATE TABLE roles (
    id UUID PRIMARY KEY,
    name VARCHAR(100) UNIQUE NOT NULL,
    description TEXT,
    parent_role_id UUID REFERENCES roles(id)
);

CREATE TABLE permissions (
    id UUID PRIMARY KEY,
    resource VARCHAR(100) NOT NULL,
    action VARCHAR(50) NOT NULL,
    UNIQUE(resource, action)
);

CREATE TABLE role_permissions (
    role_id UUID REFERENCES roles(id),
    permission_id UUID REFERENCES permissions(id),
    PRIMARY KEY (role_id, permission_id)
);

CREATE TABLE user_roles (
    user_id UUID REFERENCES users(id),
    role_id UUID REFERENCES roles(id),
    org_id UUID REFERENCES organizations(id),
    PRIMARY KEY (user_id, role_id, org_id)
);
```

---

## Attribute-Based Access Control (ABAC)

### Core Concepts

ABAC makes access decisions based on attributes of the user, resource, action, and environment.

**Attribute Categories:**
| Category | Examples |
|----------|---------|
| Subject (User) | Department, clearance level, location, role |
| Resource | Owner, classification, creation date, type |
| Action | Read, write, delete, approve |
| Environment | Time of day, IP address, device type |

### Policy Structure

ABAC policies follow the pattern: **IF (conditions on attributes) THEN (allow/deny)**

**Example Policies:**
1. "Doctors can view patient records in their department during business hours"
2. "Managers can approve expenses under $10,000 for their direct reports"
3. "Users can edit documents they own or that are shared with their team"

### Policy Decision Point (PDP) Architecture

```
Request → Policy Enforcement Point (PEP)
              ↓
         Policy Decision Point (PDP)
              ↓
         Policy Information Point (PIP)
              ↓
         Policy Store
```

- **PEP**: Intercepts request, enforces decision
- **PDP**: Evaluates policies against attributes
- **PIP**: Retrieves attribute values from data sources
- **Policy Store**: Repository of access control policies

---

## RBAC vs ABAC Decision Guide

| Factor | RBAC | ABAC |
|--------|------|------|
| Complexity | Simple to moderate | Moderate to high |
| Flexibility | Limited to role definitions | Highly flexible, context-aware |
| Scalability | Role explosion with many combinations | Scales with policy rules |
| Audit | Easy — check role assignments | Complex — evaluate policy traces |
| Best for | Clear organizational hierarchies | Dynamic, context-dependent access |
| Implementation effort | Low | High |

**Recommendation:** Start with RBAC. Add ABAC policies when you need context-dependent decisions that RBAC cannot express without role explosion.

---

## Multi-Tenant Authorization

### Tenant Isolation Strategies

| Strategy | Description | Complexity |
|----------|-------------|------------|
| Tenant-scoped roles | Same roles, scoped per tenant | Low |
| Custom roles per tenant | Tenants define own roles | Medium |
| Policy per tenant | Full ABAC policy customization | High |

### Implementation Pattern
- Include `org_id` or `tenant_id` in every permission check
- Roles are assigned per-tenant (user can be admin in Org A, viewer in Org B)
- Resource queries always filter by tenant context
- API middleware extracts tenant from JWT claims or subdomain

---

## Best Practices

- **Principle of least privilege**: Grant minimum permissions needed
- **Regular access reviews**: Quarterly audit of role assignments
- **Separation of duties**: Critical actions require multiple roles
- **Default deny**: Explicitly grant access; deny everything else
- **Centralize authorization logic**: Single service for policy decisions
- **Log all access decisions**: Enable audit trails for compliance
- **Test authorization thoroughly**: Unit test every permission boundary
