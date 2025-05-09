# ollama-granite-ocp
Demo for running Granite LLM on OpenShift with Ollama and accessing it via Open WebUI

Notes:
- Demo was built on OpenShift running on AWS.
- If you are running this in a non-AWS environment, or have a storage class, other than `gp3-csi`, update the PVC resource definitions
-  Tested on single node OpenShift on an `mx6a.4xlarge` EC2 instance and is a resource hog (espsecially memory)  
- To change the LLM being used, update `MODEL_NAME` in `config-ollama.yaml` (`granite3.3:8b` is the current value) 


## To deploy in OpenShift
To deploy in OpenShift using Kustomize, run the command:
```bash
oc apply -k k8/base  
```

There aren't any overlays at the moment, so you can run `oc apply -f k8/base` instead if you choose.

