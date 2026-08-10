Change the **Quick Facts** section:

```markdown
| Mainline | Not confirmed |
| linux-next | ✅ Applied |
| Current State | v2 applied in linux-next |
```

Then replace the final status section with:

```markdown
## Final Outcome

| Item | Status |
|------|--------|
| Final Revision | v2 |
| Patch Count | 1 |
| Mainline | Not yet confirmed |
| linux-next | ✅ Applied |
| linux-next Commit | `967d066f5334740f656577bc51c381a1bb707b61` |
| Final State | Applied in linux-next |
| Stable Handling | `Cc: stable@vger.kernel.org` included |
```

Add the commit under **References**:

```markdown
### linux-next

- [967d066f5334740f656577bc51c381a1bb707b61](https://git.kernel.org/pub/scm/linux/kernel/git/next/linux-next.git/commit/?id=967d066f5334740f656577bc51c381a1bb707b61)
```
