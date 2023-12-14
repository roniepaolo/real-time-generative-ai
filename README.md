# Real-time Generative AI

## 1. Deploy Kafka Locally

To deploy Kafka in KRaft mode, all the controllers and brokers must have an unique cluster ID. You can generate it with the Kafka script `kafka-storage.sh random-uuid` or with the commands below:

- For Ubuntu:

```bash
cat /proc/sys/kernel/random/uuid | tr -d '-' | base64 | cut -b 1-22 > cluster_id.txt
```

- For MacOS:

```bash
uuidgen | tr -d '-' | base64 | cut -b 1-22
```

The cluster ID is one of some necessary variables to execute the Ansible playbook correctly. The list of variables for Kafka deployment are described below:

- In `ansible/brokers_conf.yml`:

  - **cluster_id**. The generated UUID.

- In `ansible/brokers_vars.yml`:

  - **app_src**. Kafka source directory. Here is located the docker-compose template.
  - **build_src**. Here is located the Kafka Dockerfile.
  - **app_dir**. Target directory of Kafka. Here will be copied the docker-compose.
  - **build_dir**. Target directory of Kafka Dockerfile.
  - **storage_dir**. Target directory where data will be stored for different platforms (e.g. Kafka, Schema Registry).
  - **kafka_data_dir**. Target directory Where Kafka data will be stored.
  - **log_dir**. Target directory where Kafka logs will be stored.
  - **config_dir**. Target directory Where Kafka configuration will be generated.
  - **target_user**: User that you are using.
  - **target_group**: Group that your user belongs.

Once the cluster ID and all the other variables were set, you can execute the playbook with the command below. The result are two directories (`opt` and `data`) that contain all necessary files to deploy Kafka locally.

```bash
ansible-playbook brokers_conf.yml -i hosts --ask-become-pass
```

For information of how to deploy Kafka on Cloud, check my [repo](https://github.com/roniepaolo/kafka-platform) about Kafka in KRaft mode using Terraform and Ansible.

## 2. Deploy Schema Registry Locally

The Schema Registry Ansible playbook also needs some additional variables to execute correctly. These are described below:

- In `ansible/brokers_vars.yml`:

  - **app_src**. Schema Registry source directory. Here is located the docker-compose template.
  - **app_dir**. Target directory of Schema Registry. Here will be copied the docker-compose.
  - **build_dir**. Target directory of Schema Registry Dockerfile.
  - **storage_dir**. Target directory where data will be stored for different platforms (e.g. Kafka, Schema Registry).
  - **log_dir**. Target directory where Schema Registry logs will be stored.
  - **target_user**: User that you are using.
  - **target_group**: Group that your user belongs.

Once the cluster ID and all the other variables were set, you can execute the playbook with the command below. The result are two directories (`opt` and `data`) that contain all necessary files to deploy Kafka locally.

```bash
ansible-playbook sr_conf.yml -i hosts --ask-become-pass
```

For information of how to deploy Schema Registry on Cloud, check my [repo](https://github.com/roniepaolo/kafka-platform) about Kafka in KRaft mode using Terraform and Ansible.
