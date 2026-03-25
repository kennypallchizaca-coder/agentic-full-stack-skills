# Relationship Decision Guide

Use this guide to choose the correct relationship type between any two entities or records.

## Decision table

| Scenario | Type | Reference location |
|----------|------|--------------------|
| One `{A}` has many `{B}`. Each `{B}` belongs to one `{A}`. | `1:N` | Reference or foreign key in `{B}` |
| One `{A}` has exactly one `{B}`. Each `{B}` belongs to one `{A}`. | `1:1` | Reference in the dependent side |
| Many `{A}` associate with many `{B}`. | `N:N` | Join table / relation collection / linking document |
| The relation itself has fields (for example timestamp, status, actor). | Relation as first-class entity | Model the link as its own record |

---

## Strategy checklist

- [ ] Defined which side owns the reference or foreign key
- [ ] Named the join structure explicitly when a separate relation record exists
- [ ] Chosen a load strategy that fits the access pattern
- [ ] Added repository queries that load related data intentionally instead of navigating everything by default
- [ ] Reviewed query count or explain plans to avoid accidental N+1 behavior

---

## Load strategy options

| Strategy | When to use |
|----------|-------------|
| On-demand loading | Related data is not always needed and should load only when requested |
| Joined or eager loading | Related data is required in nearly every read path |
| Batched loading | Multiple records need the same related data and the platform supports batching efficiently |

> Rule: if a relation is always loaded eagerly, document why that cost is justified.

---

## Propagation rules

| Propagation choice | Meaning | Use when |
|--------------------|---------|---------|
| Propagate create | Creating the parent should also create the child/link | Child cannot exist without parent |
| Propagate update | Parent updates always carry related changes | The related record is managed as one unit |
| Propagate delete | Deleting the parent should remove or archive dependents | Dependents are lifecycle-owned by parent |
| No propagation | Each side is managed independently | Most peer or loosely coupled relations |

If the chosen ORM uses names like `LAZY`, `EAGER`, `PERSIST`, `MERGE`, or `REMOVE`, map those provider-specific terms to the neutral decisions above instead of assuming they are universal.
