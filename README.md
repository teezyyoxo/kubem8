# kubem8 - Kubernetes Administration for Newbies 🛳️
*Your friendly kube-mate for managing pods, logs, scaling, and more — without the yak shaving*. ;)

These are simple Bash helpers for working with `kubectl` without needing to manually copy full pod names every time. It is one of my biggest pet peeves of using Kubernetes, and there's no way I'd willingly continue to subject myself to such torture, lol.

**IMPORTANT**: By using these tools, it is assumed that you are using Bash **and** have kubectl installed, with a cluster **that is online**.

Each script has the option/flag definitions in the code themselves.

---

## 🧰 Features
🔍 Search pods and deployments by name substring.

🧾 View pod logs with klog, nicely colorized for JSON-formatted log lines (INFO/ERROR/TRACE), including multi-line stack traces.

📄 Describe pods and deployments with kdescribe, showing detailed info and rich metadata.

🗑️ Delete pods and deployments safely with kdel, including interactive selection and confirmation prompts.

🚀 Interactive prompt if multiple matches found, to pick the exact resource.

🧭 Optional `-n` / `--namespace` flag support for all commands; defaults to the default namespace if not specified.

➡️ Optional `-t` / `--type` flag support for all commands; defaults to "pod" if not specified.

🧼 Clean, readable output formatting with colors and aligned columns—no extra dependencies like jq required.

🚫 Does not require jq or any third-party tools (except kubectl).

---
## 📦 Installation
1. Download and copy the script(s) that you need to a directory in your `$PATH` (e.g., `/usr/local/bin/`).
2. Make them executable with `chmod +x <path/to/script>`.
3. 🏃🏽‍♂️💨
```
## Example installation
sudo cp klog /usr/local/bin/
sudo cp kdescribe /usr/local/bin/
sudo cp kdel /usr/local/bin
sudo chmod +x /usr/local/bin/klog /usr/local/bin/kdescribe /usr/local/bin/kdel <--- this will make the script executable
```
_Using `/usr/local/bin/` is easiest, as you will then be able to immediately run them without having to `source` your `.bashrc`_.

## 🛠️ Usage
```
klog <pod-string>                     # searches in 'default' namespace
kdescribe <pod-string>                # searhces in 'default' namespace
klog -n <namespace> <pod-string>      # searches in the specified namespace
kdescribe -n <namespace> <pod-string> # searches in the specified namespace
etc...
```
*If multiple matches are found, you’ll be prompted to select the one you want.*

### More Examples
```
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
```
or...
```
# Describe deployment with 'web' in the name in namespace 'prod'
kdescribe -n prod web
# Delete pod with 'cache' in the name in namespace 'staging'
kdel -n staging cache
```
or...
```
kscale get system-web-ui -n dev
# => Deployment system-web-ui in namespace 'dev' has 1 replicas configured.

kscale some-random-pod 2
# =>  Please confirm the following change:
      Resource:   system-web-ui [Deployment]
      Namespace:  default
      Current:    1 replica(s)
      Requested:  0 replica(s)

      Proceed with scaling? [y/N]: y
      Scaling system-web-ui to 0 replicas...
      deployment.apps/system-web-ui scaled
```
---
## Notes
- These scripts default to your current Kubernetes context and namespace and assume kubectl is installed, configured, and has access to your cluster
- Supports **partial substring** matches for pod names.
- You may hardcode a namespace by modifying the NAMESPACE_ARG variable inside the scripts.
- Works best with reasonably short and unique search strings to avoid large result sets.

## Future Plans 💡
- Package each script into one binary (i.e., kubem8) for easier application and deployment.
- Prettier output
- Potential rebuild with Python, to leverage and include jq for more efficient log parsing

## Contributions
Feel free to open issues or pull requests for improvements!
