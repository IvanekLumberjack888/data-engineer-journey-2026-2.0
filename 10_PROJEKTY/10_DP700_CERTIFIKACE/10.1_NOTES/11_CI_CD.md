# 1️⃣1️⃣ CI/CD & DEPLOYMENT

**Cíl:** Deployment automatizace a version control

---

## 📖 TEORIE

### Git Integration

Fabric + GitHub/Azure Repos.

**Workflow:**
- Code changes v Git
- Auto-sync do Fabric
- Version tracking
- Rollback možný

### Deployment Pipelines

MultiStage deployment.

**Stages:**
- Dev (development)
- Test (testing)
- Prod (production)

**Process:**
1. Vytvořit v Dev
2. Test v Test
3. Deploy do Prod

### CI/CD Principles

**Continuous Integration:**
- Auto build
- Auto test
- Merge frequently

**Continuous Deployment:**
- Auto deploy na test
- Auto deploy na prod (s approval)
- Rollback mechanisms

### Release Process

**Types:**
- Manual deployment
- Scheduled deployment
- Automated (na Git push)

### Best Practices

1. **Version Control** — Všechno v Git
2. **Environment Separation** — Dev/Test/Prod
3. **Testing** — Automated tests
4. **Approval Process** — Code review
5. **Documentation** — What changed

---

## 🛠️ PRAXE

- [ ] Create deployment pipeline
- [ ] Configure 3 stages (Dev/Test/Prod)
- [ ] Link Git repository
- [ ] Deploy content from Dev → Test
- [ ] Deploy from Test → Prod
- [ ] Test rollback
- [ ] Monitor deployments
---

## 🔗 EXTERNÍ LINKY

- Deployment Pipelines: https://learn.microsoft.com/fabric/cicd/deployment-pipelines-overview
- Git Integration: https://learn.microsoft.com/fabric/cicd/git-integration-overview
- CI/CD Best Practices: https://learn.microsoft.com/en-us/azure/architecture/devops/

---

## NEXT → [[12_ADMINISTRACE]]