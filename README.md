# Real-time Generative AI

## 1. Deploy Kafka Locally

To deploy Kafka in KRaft mode, all the controllers and brokers must have an unique cluster ID. It can be generated with the Kafka script `kafka-storage.sh random-uuid` or with the commands below:

- For Ubuntu:

```bash
cat /proc/sys/kernel/random/uuid | tr -d '-' | base64 | cut -b 1-22 > cluster_id.txt
```

- For MacOS:

```bash
uuidgen | tr -d '-' | base64 | cut -b 1-22
```

Once the cluster ID was assigned to `cluster_id` in `ansible/brokers_conf.yml`, the playbook can be executed with the command below. The result are two directories (`opt` and `data`) that contain all necessary files to deploy Kafka locally.

```bash
ansible-playbook brokers_conf.yml -i hosts --ask-become-pass
```

For information of how to deploy Kafka on Cloud, check my [repo](https://github.com/roniepaolo/kafka-platform) about Kafka in KRaft mode using Terraform and Ansible.

## 2. Deploy Schema Registry Locally

After generated the necessary files and folders for Kafka Deployment, the Schema Registry playbook can be executed. The result are two directories inside `opt` and `data` that contain all necessary files to deploy the Schema Registry locally.

```bash
ansible-playbook sr_conf.yml -i hosts --ask-become-pass
```

For information of how to deploy Schema Registry on Cloud, check my [repo](https://github.com/roniepaolo/kafka-platform) about Kafka in KRaft mode using Terraform and Ansible.
