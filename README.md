## RACKSPACE HEAT KUBERNETES

This thing help you to author a Kubernetes cluster on Rackspace using their Orchestration facility. It does the two things in order:

   1. Compiles the HEAT template based on your settings using `heatit` tool
   2. Submits the HEAT template to Rackspace using Rackspace's `rack` tool

It is based up on cloud-config files from Kubernetes project, see their [Getting Started folder for configs](https://github.com/kubernetes/kubernetes/tree/release-1.1/docs/getting-started-guides/coreos/cloud-configs)

### Software needed to execute these:

The `Heatit` tool. A cross-platform tool that helps you to maintain HEAT templates as a bunch of re-usable pieces. You can get more information for `heatit` [here](https://github.com/pavlo/heatit) or download it from [here](https://github.com/pavlo/heatit/releases).

The `Rack` tool. A cross-platform tool maintained by Rackspace that allows you to automate various tasks. Here we use it's "Create Stack" facility. You can read more and download the tool [here](https://github.com/rackspace/rack).

### Configure the cluster

First off you edit `params.yaml` file to suit your needs. There, among others, you specify the version on Kubernetes to use to deploy the cluster, CoreOS image ID etc. Once parameters look good, you compile the template:

     > heatit process --source=kubernetes.heatit.yaml --params=params.yaml --destination=heat-final.yaml

### Build the cluster

Here you submit the HEAT template generated above to Rackspace. This is going to be a Rackspace Stack in the end of the day:

     > rack orchestration stack create --name=kubernetes-stack --template-file=heat-final.yaml
