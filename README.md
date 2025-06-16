# Kubernetes Pod Quick Access Scripts

Simple CLI wrappers to speed up common `kubectl` pod commands by letting you search for pods by substring and select from multiple matches.

---

## Scripts

### `klog`

Fetch logs from a pod matching a search string.

- If one pod matches, it shows logs directly.
- If multiple pods match, prompts to select one.
- If no match, notifies and exits.

### `kdesc`

Describe a pod matching a search string.

Same behavior as `klog`, but runs `kubectl describe pod`.

---

## Installation

1. Save the script files (`klog`, `kdesc`) to your machine.
2. Make them executable:

   ```bash
   chmod +x klog kdesc