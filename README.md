# ollama-granite-ocp

Demo for running Granite LLM on OpenShift using [Ollama](https://ollama.com) and accessing it via [Open WebUI](https://github.com/open-webui/open-webui).

## Overview

This demo:
- Deploys a Large Language Model (LLM) using Ollama on OpenShift
- Exposes the model through Open WebUI
- Supports running a single model or preloading multiple models

> ⚠️ **Note:**  
> This was built and tested on OpenShift running on AWS using an `mx6a.4xlarge` EC2 instance. It is resource-intensive, especially in terms of memory.  
> If you're deploying in a different environment or using a non-`gp3-csi` storage class, update the `PersistentVolumeClaim` definitions accordingly.

---

## 🛠 Deploy to OpenShift

### Option 1: Deploy a single-model Ollama stack

To deploy with the default model (`granite3.3:8b`), run:

```bash
oc apply -k k8/base
```
This deploys the ollama service in the `ollama-granite-demo` namespace and preloads the model defined in config-ollama.yaml.

To change the model, update the `MODEL_NAME` in `k8/base/config-ollama.yaml`.

---

### Option 2: Deploy a multi-model Ollama stack

To preload multiple models (`granite3.3:8b`, `mistral`, `llama3`), run:

```bash
oc apply -k k8/overlays/multi-model
```

This deploys the `ollama` service in the `multi-model` namespace and preloads the models defined in `config-ollama.yaml`.

---

## 🌐 Accessing the Web UI

Once deployed, get the Open WebUI route:

```bash
oc get routes
```

Example output:
```bash
NAME         HOST/PORT
open-webui   open-webui-ollama-granite-demo.apps.<your-domain>
```

Open that URL in your browser. The first time you access it, you'll be prompted to create an admin account.

---

## 🔄 Customization

- **Change default model**: edit the `MODEL_NAME` value in the ConfigMap (`k8/base/config-ollama.yaml`)
- **Add more models**: update the `MODELS` key in the ConfigMap in `k8/overlays/multi-model/config-ollama.yaml`
