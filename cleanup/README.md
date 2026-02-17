# Cleanup

This folder contains scripts and documentation for cleaning up Azure resources after the capstone project.

## Purpose

Proper cleanup ensures:
- No unexpected Azure charges
- Clean environment for future projects
- Verification that all resources are removed

## Cleanup Steps

1. Delete resource groups in reverse order of creation
2. Verify no orphaned resources remain
3. Check Azure Cost Management for any remaining charges
4. Document cleanup with screenshots

## Deliverables

- [ ] Cleanup scripts created
- [ ] All resources deleted
- [ ] Verification screenshots added
- [ ] Final cost report documented

## Verification Checklist

- [ ] All resource groups deleted
- [ ] No orphaned disks or NICs
- [ ] No remaining public IPs
- [ ] Azure Advisor shows no resources