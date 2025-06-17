# klog / kdescribe

These are simple Bash helpers for working with `kubectl` without needing to manually copy full pod names every time.
FYI, each script has the flag definitions in the code themselves.

---

## 🧰 Features
•🔍 Search pods and deployments by name substring.
•🧾 View pod logs with klog, nicely colorized for JSON-formatted log lines (INFO/ERROR/TRACE), including multi-line stack traces.
•📄 Describe pods and deployments with kdescribe, showing detailed info and rich metadata.
•🗑️ Delete pods and deployments safely with kdel, including interactive selection and confirmation prompts.
•🚀 Interactive prompt if multiple matches found, to pick the exact resource.
•🧭 Optional -n / --namespace flag support for all commands; defaults to the default namespace if not specified.
•➡️ Optional -t / --type flag support for all commands; defaults to "pod" if not specified.
•🧼 Clean, readable output formatting with colors and aligned columns—no extra dependencies like jq required.
---
## 📦 Installation
Copy both scripts to a directory in your `$PATH` (e.g., `/usr/local/bin/`):
   sudo cp klog /usr/local/bin/
   sudo cp kdescribe /usr/local/bin/
   sudo cp kdel /usr/local/bin
   sudo chmod +x /usr/local/bin/klog /usr/local/bin/kdescribe /usr/local/bin/kdel
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
or...
   # Describe deployment with 'web' in the name in namespace 'prod'
   kdescribe -n prod web
   # Delete pod with 'cache' in the name in namespace 'staging'
   kdel -n staging cache
or...
   kscale get system-web-ui -n dev
   # => Deployment bigid-ui in namespace 'bigid' has 1 replicas configured.

   kscale some-random-pod 2
   # => Interactively matches and confirms scaling to 2

### 🚫 No Dependencies
	•	Does not require jq or any third-party tools
	•	Works with Bash and kubectl

## Notes
	•	These scripts default to your current Kubernetes context and namespace and assume kubectl is installed, configured, and has access to your cluster.
   •	Supports **partial substring** matches for pod names.
	•	You can hardcode a namespace by modifying the NAMESPACE_ARG variable inside the scripts. (for now)
   •	Works best with reasonably short and unique search strings to avoid large result sets.

## Contributions
Feel free to open issues or pull requests for improvements!