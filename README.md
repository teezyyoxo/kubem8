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
   `chmod +x klog kdesc`
3.	Move them to a directory in your $PATH:
   `sudo mv klog kdesc /usr/local/bin/`
## Usage
   # Show logs for pods matching "pia"
   klog pia

   # Describe pods matching "cache"
   kdesc cache

   # If you run without arguments, it will prompt:
   klog
   kdesc

### Example
   $ klog pia
   Multiple matches found:
   1) bigid-pia-6d6fbb774b-chdp8
   Select a pod number: 1
   Showing logs for: bigid-pia-6d6fbb774b-chdp8
   [logs output...]

## Notes
	•	These scripts default to your current Kubernetes context and namespace.
   •	Supports **partial substring** matches for pod names.
	•	You can hardcode a namespace by modifying the NAMESPACE_ARG variable inside the scripts. (for now)

## Contributions
Feel free to open issues or pull requests for improvements!