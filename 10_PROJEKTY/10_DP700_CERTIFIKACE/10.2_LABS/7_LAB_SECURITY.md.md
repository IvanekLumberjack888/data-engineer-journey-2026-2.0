# 7️⃣ LAB: SECURITY & RBAC

## Cíl

Nastavit role-based access control a row-level security.

---

## Praxe - Krok za krokem

### Krok 1: Workspace Roles

```
1. Workspace settings
2. Manage access
3. Add member
4. User: [colleague email]
5. Role: Member (can create/edit)
   OR Contributor (can edit only)
6. Save
```

- [ ] Uživatel přidán

### Krok 2: Item-Level Permissions

```
1. Lakehouse → Sales_DW
2. Share
3. Add people
4. Role: Viewer (read-only)
5. Share
```

- [ ] Item permissiony nastaveny

### Krok 3: Create SQL Role

V Data Warehouse:

```sql
CREATE ROLE SalesAnalystRole
```

- [ ] SQL role vytvořena

### Krok 4: Row-Level Security (RLS)

```sql
CREATE ROLE SalesNorthOnly

-- Security Predicate: Show only North region
ALTER TABLE Sales ADD FILTER (Region = 'North')
  FOR ROLE SalesNorthOnly
```

- [ ] RLS rule vytvořena

### Krok 5: Assign Role to User

```sql
ALTER ROLE SalesNorthOnly ADD MEMBER [user@company.com]
```

- [ ] Uživatel přidán do role

### Krok 6: Test RLS

Login jako ten uživatel:

```sql
SELECT * FROM Sales
-- Měly by vidět jen North region
```

- [ ] RLS funguje (vidí jen North)

### Krok 7: Audit

```
1. Go to Workspace
2. Usage metrics
3. View who accessed what and when
```

- [ ] Audit log viditelný

---

## Pozorování

- Jaké jsou RLS výhody?
- Kolik uživatelů má přístup?

---

## Hotovo s Labs! 🎉

Teď máš praktické zkušenosti se všemi core Fabric features.

Příště: Case studies + exam prep.