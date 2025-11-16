# 🔟 SECURITY & GOVERNANCE

**Cíl:** Zabezpečit data a implementovat governance

---

## 📖 TEORIE

### Multi-Layer Security

**Vrstvy:**
1. Authentication (kdo si)
2. Authorization (co můžeš)
3. Encryption (bezpečnost)
4. Auditing (co se stalo)

### Authentication

**Metody:**
- Entra ID (Azure AD)
- Service Principal
- Managed Identity
- PAT (Personal Access Token)

### Authorization (RBAC)

**Workspace Roles:**
- Admin (full control)
- Member (create/edit)
- Contributor (edit only)
- Viewer (read-only)

**Item-Level Permissions:**
- Granular per item
- Share with users/groups
- Specific roles

### Row-Level Security (RLS)

Filter rows based na user.

```sql
ALTER TABLE Sales ADD FILTER (Region = 'North')
  FOR ROLE SalesNorthRole
```

### Column-Level Security (CLS)

Skryt sloupce od určitých uživatelů.

```sql
ALTER TABLE Sales DENY SELECT ON Amount TO SalesViewerRole
```

### Encryption

**Layers:**
- Transport (HTTPS/TLS)
- At-rest (Azure managed keys)
- Customer-managed keys (optional)

### Data Classification & Labeling

Označit data dle sensitivity.

**Levels:**
- Public
- Internal
- Confidential
- Restricted

### Governance Features

**Microsoft Purview:**
- Data lineage
- Metadata scanning
- Data discovery
- Compliance

**Endorsement:**
- Promotion (internal validation)
- Certification (official approval)
- Trust badges

---

## 🛠️ PRAXE

- [ ] Setup workspace roles
- [ ] Add user with permissions
- [ ] Create RLS rule
- [ ] Test RLS (login as user)
- [ ] Column masking
- [ ] Audit logs review
- [ ] Data classification
- [ ] Explore Purview
---

## 🔗 EXTERNÍ LINKY

- Security Overview: https://learn.microsoft.com/fabric/security/security-overview
- RBAC: https://learn.microsoft.com/fabric/admin/roles
- RLS: https://learn.microsoft.com/en-us/sql/relational-databases/security/row-level-security
- Purview: https://learn.microsoft.com/purview/

---

## NEXT →  [[11_CI_CD.md]]