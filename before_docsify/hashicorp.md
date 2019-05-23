# HashiCorp
HashiCorp is a company that built a set of tools for provisioning, securing,
connecting, and running infrastructure as code.

Learning platform: https://learn.hashicorp.com/

## Vault
- dynamic secrets. Time-bounded.
- works for db credentials, smtp creds, api keys, etc
- An interesting feature coming soon is the vault advisor: monitor which
  clients are consuming which secrets, recommend policy/configuration
  improvements.

## Nomad
- compared with kubernetes, but simpler. When you need a container scheduler
  without a complete container infrastructure.
- Schedule jobs to execute somewhere in the client pool (infrastructure)

## Consul
- service discovery (Consul dns), configuration (Consul k/v), and segmentation (Consul connect)
- Segmentation:
  * which service can communicate with which service (service access graph)
  * Mutual TLS / trust

## Terraform
- provisioning
- works like a state machine
- allows you to manage resources through declarative code
- different "providers" allow you to manage different types of resources

## Packer
- automation of machine image building
