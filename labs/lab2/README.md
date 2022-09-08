# Install Dynatrace OneAgent Operator for Kubernetes (Containerd)

Before running the Oneagent Operator, please make sure that deep monitoring for Containerd Monitoring is enabled

Go to <b>Settings -> Processes and Container -> Container Monitoring</b>

![GKE-CLI-Indentation](https://github.com/Nodnarboen/HOT-k8s/blob/master/assets/Picture6.1.png)

Download codebase from Git repository

``` bash
git clone https://github.com/christopherchai/HOT-k8s.git
```

Install OneAgent Operator

``` bash
cd HOT-k8s 
./install-oneagent-operator-v2.sh
```

1. Locate your Tenant ID from your Dynatrace environment. 
It can be found in this format https://<b>TenantID</b>.live.dynatrace.com
2. Enter your Tenant ID to the screen prompt.
3. Get an API token for the Dynatrace API with the scope Access problem and event feed, metrics, and topology. 
You can find it from <b>Settings</b> -> <b>Integration</b> -> <b>Dynatrace API</b> 
4. Enter your API token to the screen prompt.
5. Get a Platform-as-a-Service token. You can find it from <b>Settings</b> -> <b>Integration</b> -> <b>Platform as a Service</b>
6. Enter your PaaS token to the screen prompt.

That's it! Dynatrace is now monitoring your GKE Environment!

```install-oneagent-operator-v2.sh``` basically automated the steps from our [official documentation page](https://www.dynatrace.com/support/help/technology-support/cloud-platforms/google-cloud-platform/google-kubernetes-engine/deploy-oneagent-on-google-kubernetes-engine-clusters/)

<b>Note:</b> If you already have an Environment ActiveGate and you would like to leverage on that, please use the the steps listed in the link above instead of the automated steps. Your apiUrl should be ``` https://<ACTIVE_GATE_IP OR HOSTNAME>:9999/e/<TenantID>/api``` for both SaaS and Managed.

![GKE-CLI-Indentation](https://github.com/Nodnarboen/HOT-k8s/blob/master/assets/Picture7.png)

### Pointers / Troubleshooting Tips:

1. When editing the cr.yml, make sure the the <b>indentation alignment</b> are correct.

2. Take note of <b>not swapping</b> the declaration of the API and PaaS token in the secret. 

3. If you need got an error regarding the token, you can use <b>kubectl replace -f secret oneagent</b> to remove the current secret

4. If needed, run <b>kubectl delete --all pods --namespace=dynatrace</b> to delete all pods. This will cycle through the pods and you will have new pod instances.

Official troubleshooting page could be found [here](https://www.dynatrace.com/support/help/technology-support/cloud-platforms/google-cloud-platform/google-kubernetes-engine/installation-and-operation/full-stack/troubleshoot-oneagent-on-google-kubernetes-engine/)

If everything is working, you will see the hosts appearing under Hosts from clicking Hosts under the left navigation bar.

![GKE-Hosts](https://github.com/Nodnarboen/HOT-k8s/blob/master/assets/Picture7.1.png)

:arrow_up: [Back to TOC](/README.md) :arrow_left: [Prev](../lab1/README.md)   :arrow_right: [Next](../lab3/README.md)  

