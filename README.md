# klog / kdescribe

These are simple Bash helpers for working with `kubectl` without needing to manually copy full pod names every time.

---

## 🧰 Features

- 🔍 Search pods by name substring.
- 🧾 View logs with `klog`, nicely colorized for JSON-formatted log lines (INFO/ERROR/etc).
- 📄 Describe pods with `kdescribe`.
- 🚀 Interactive prompt if multiple matches found.
- 🧭 Optional `-n` / `--namespace` flag support. Defaults to `default` namespace if not specified.
- 🧼 Clean output formatting, no extra dependencies like `jq`.

---

## 📦 Installation
Copy both scripts to a directory in your `$PATH` (e.g., `/usr/local/bin/`):
   sudo cp klog /usr/local/bin/
   sudo cp kdescribe /usr/local/bin/
   sudo chmod +x /usr/local/bin/klog /usr/local/bin/kdescribe
## 🛠️ Usage
   klog pod-substring                 # searches in 'default' namespace
   klog -n your-namespace pod-name    # searches in given namespace
   ###############
   kdescribe pod-substring
   kdescribe -n your-namespace pod-name
*If multiple matches are found, you’ll be prompted to choose.*



### Example
   ubuntu@host:~$ klog iam
   Multiple matches found:
   1) iama-pod-6fbd544566-h9bm9
   2) iama-pod-6fbd544566-vf2kg
   Select a pod number: 2
   Showing logs for: iama-pod-6fbd544566-vf2kg
   Namespace: default

   [2025-06-17T14:29:21.604Z] INFO - Starting application...
   {"name":"pod","level":"INFO","msg":"Starting application...","time":"2025-06-17T14:29:21.604Z"}

   [2025-06-17T14:29:51.653Z] INFO - Fetching system token by refresh token
   {"name":"pod","level":"INFO","msg":"Fetching system token by refresh token","time":"2025-06-17T14:29:51.653Z"}

   MongoServerSelectionError: getaddrinfo ENOTFOUND some-dependency
      at Timeout._onTimeout (...)
### 🚫 No Dependencies
	•	Does not require jq or any third-party tools
	•	Works with Bash and kubectl

## Notes
	•	These scripts default to your current Kubernetes context and namespace.
   •	Supports **partial substring** matches for pod names.
	•	You can hardcode a namespace by modifying the NAMESPACE_ARG variable inside the scripts. (for now)

## Contributions
Feel free to open issues or pull requests for improvements!