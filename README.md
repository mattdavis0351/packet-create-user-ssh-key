# GitHub Actions for creating user SSH keys on Packet.com

## Automate your access

This GitHub Action will store a new user level SSH key on [packet.com](https://packet.com). SSH keys grant you access to resources such as deployed servers within a project.

# Creating projects

With this action you can automate your workflow by adding user level SSH keys using the [packet.com api](https://api.packet.net).

To use this action you will first need an [authentication token](https://www.packet.com/developers/api/authentication/) which can be generated through the [Packet Portal](https://app.packet.net/login?redirect=%2F%3F__woopraid%3DjUPDKi0tqtym).

You will also need a public/private key pair. [Learn how to generate keys](https://www.packet.com/developers/docs/servers/key-features/ssh-keys/).

**NEVER share your private key with anyone!**

**Packet.com is NOT a free service, so you will be asked to provide billing information. This action will NOT have access to that information.**

## Sample workflow that uses the packet-create-user-ssh-key action

```yaml
# File: .github/workflows/workflow.yml

on: [push]

name: Packet Project Sample

jobs:
  store-new-public-key:
    runs-on: ubuntu-latest
    name: Store new user level SSH key
    steps:
      - uses: mattdavis0351/packet-create-user-ssh-key@v1
        id: key
        with:
          API_key: ${{ secrets.PACKET_API_KEY }}
          key_label: our-admin
          public_key: ${{ secrets.PACKET_PUBLIC_KEY }}
```

## Available Inputs

| Input        | Description                                        | Default                     | Required           |
| ------------ | -------------------------------------------------- | --------------------------- | ------------------ |
| `API_key`    | Packet.com API authorization token                 | No key supplied             | :white_check_mark: |
| `key_label`  | Desired label for users SSH key                    | Generated by GitHub Actions | :white_check_mark: |
| `public_key` | Public key for user stored in as repository secret | No key supplied             | :white_check_mark: |

## Outputs from action

This action supplies the following outputs which can be consumed by subsequent actions in the current job.

| Output      | Description                                            |
| ----------- | ------------------------------------------------------ |
| `key_id`    | ID of the newly stored SSH key returned as a string    |
| `key_owner` | Owner of the newly stored SSH key returned as a string |
