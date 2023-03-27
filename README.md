# eda-scripts

This collections hosts a set of scripts used to use the Ansible Validated Content Collection [cloud.aws_ops](https://github.com/ansible-collections/cloud.aws_ops) with togerther with the [Event-driven Ansible initiative](https://github.com/ansible/event-driven-ansible).

For part of the contenf of this repository has been opened a Pull Request against the `cloud.aws_ops` collection https://github.com/redhat-cop/cloud.aws_ops/pull/29.

`manage_playbook.yml` is a management playbook that allows to deploy the AWS infrastructure and to introduce different drift situations into the system. In addition, it allows to choose the drift action we may want to introduce into the system by setting the operation parameter to one of the following values as an extra variable.
1. `disable_encryption`: Disables trail encryption.
2. `delete_trail`: Deletes the AWS CloudTrail.
3. `disable_key`: Disable the KMS key used to encrypt the S3 bucket.
4. `delete_key`: Deletes the KMS key used to encrypt the S3 bucket.

The AWS infrastructure can be rolled up with the following command:

```
ansible-playbook manage_trail_encryption_play.yml --extra-vars operation=deploy
```

In you want to introduce different drift into the system just set the values for the `operation` parameter, for example:

```
ansible-playbook manage_trail_encryption_play.yml --extra-vars operation=disable_encryption
```