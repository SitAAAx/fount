# FOUNT :fountain:

The goal of _FOUNT_ is to set up a _cloud native_ and _vendor neutral_ platform in a simple way.
It starts with a _bare metal_ machine and aims at a full fledged cluster configuration.
The aim is also to make the setup simple and modular in order to support the familiarization and understanding of _Kubernetes_.

## Prerequisites

In order to be able to experiment with _FOUNT_, the following hardware requirements are needed:

- Debian based (e.g. Ubuntu) machine with at least 1GB of ram and one core - for _Gitlab_ **4 cores** and **4GB of memory** are recommended.
- A _DNS_ record that points to the public _IP_ address of the machine.
- A _SSH_ connection to the machine - preferably using _Public Key Authentication_.

Additionally _FOUNT_ uses _Ansible_ for the setup and configuration.
If _Python 3_ is installed you can easily install _Ansible_ via _Pip_.
This is shown in the following script:

```shell script
$ python -m venv .venv
$ source .venv/bin/activate
$ pip install --upgrade pip
$ pip install ansible
```

## Setup the Cluster

The minimal setup of the _k3s_ cluster on the machine is defined in the _Ansible_ playbook `playbooks/setup-k3s-cluster.yml`.

> :warning: The setup runs a retrieved script! **This is potentially malicious and should be checked in advance.**

Before the playbook can be executed the `playbooks/hosts.yml` has to be adapted.
Please replace _k3s.l4b.space_ with your _DNS_ record.
You may also want to customize the _SSH_ user and port.

After that navigate into the `playbooks` directory and run: `ansible-playbook setup-k3s-cluster.yml`

If everything went fine something similar to

<pre>PLAY RECAP ******************************************************************************************************************
<font color="#C4A000">1-single-dev.node.k3s</font>      : <font color="#4E9A06">ok=6   </font> <font color="#C4A000">changed=5   </font> unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
</pre>

should be shown at the end of the log after the play finished.

Although the playbook already does it, you can check the status fo the cluster node by executing: `kubectl get nodes`
If the node reached the _Ready_ status your cluster is up and running :tada:

## Sources and further information

- [K3s setup guide](https://rancher.com/docs/k3s/latest/en/installation/install-options/)
