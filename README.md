# Atlantis on Google Compute Engine

This Terraform module deploys various resources to run Atlantis on Google Compute Engine.

- [Example Usage](#example-usage)
    - [Basic](examples/basic)
    - [Complete](examples/complete)
    - [Secured Environment Variables](examples/secured-env-vars)
- [Feature highlights](#feature-highlights)
- [FAQ](#faq)
- [Requirements](#requirements)

## Example Usage

See the [`examples`](https://github.com/bschaatsbergen/atlantis-on-gcp-vm/tree/master/examples/basic) directory.

## Feature highlights

- **Container-Optimized OS** - Atlantis runs as a Docker container on a container optimized VM.

- **Managed Instance Group** - The VM instance is part of a MIG (Managed Instance Group), this ensures that Atlantis is always up and running.

- **External HTTPS Load Balancer** - A Layer 7 load balancer is created together with a managed SSL certificate for the provided domain.

- **Custom port for Atlantis** - This module features the ability to run Atlantis on a custom port, simply set the `ATLANTIS_PORT` environment variable.

- **Separate Persistent Data Disk** - The VM instance has a separate attached persistent data disk attached to it to ensure that Atlantis data is persisted and not lost if the VM is deleted or terminated.

- **Shielded VM** - A Shielded VM is a VM that's hardened by a set of security controls that help defend against rootkits and bootkits. Using a Shielded VM helps protect enterprise workloads from threats like remote attacks, privilege escalation, and malicious insiders.

## FAQ

### My Virtual Machine (VM) experienced an outage and is taking some time to restart

It may take up to three minutes for the Managed Instance Group to safely shut down and recreate the VM before it is considered healthy again.

### Even though the apply function worked correctly, I am receiving an ERR_SSL_VERSION_OR_CIPHER_MISMATCH error.

This error indicates that the Google Cloud Managed SSL certificate is not yet fully provisioned. 
If all configurations are correct, it may take up to 25 minutes for the certificate to be provisioned. 
You can check the status of the certificate in the Google Cloud Console.

<!-- BEGINNING OF PRE-COMMIT-TERRAFORM DOCS HOOK -->

## Requirements

No requirements.

## Providers

| Name                                                      | Version |
| --------------------------------------------------------- | ------- |
| <a name="provider_google"></a> [google](#provider_google) | 4.47.0  |

## Modules

| Name                                                        | Source                                       | Version |
| ----------------------------------------------------------- | -------------------------------------------- | ------- |
| <a name="module_atlantis"></a> [atlantis](#module_atlantis) | terraform-google-modules/container-vm/google | ~> 2.0  |

## Resources

| Name                                                                                                                                                              | Type        |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------- |
| [google_compute_backend_service.atlantis](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/compute_backend_service)                 | resource    |
| [google_compute_firewall.atlantis_lb_health_check](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/compute_firewall)               | resource    |
| [google_compute_global_address.atlantis](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/compute_global_address)                   | resource    |
| [google_compute_global_forwarding_rule.https](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/compute_global_forwarding_rule)      | resource    |
| [google_compute_health_check.atlantis](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/compute_health_check)                       | resource    |
| [google_compute_instance_group_manager.atlantis](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/compute_instance_group_manager)   | resource    |
| [google_compute_instance_template.atlantis](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/compute_instance_template)             | resource    |
| [google_compute_managed_ssl_certificate.atlantis](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/compute_managed_ssl_certificate) | resource    |
| [google_compute_route.public_internet](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/compute_route)                              | resource    |
| [google_compute_target_https_proxy.atlantis](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/compute_target_https_proxy)           | resource    |
| [google_compute_url_map.atlantis](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/compute_url_map)                                 | resource    |
| [google_compute_image.cos](https://registry.terraform.io/providers/hashicorp/google/latest/docs/data-sources/compute_image)                                       | data source |

## Inputs

| Name                                                                                                   | Description                                                                                                                             | Type                                                                     | Default                                                                       | Required |
| ------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------ | ----------------------------------------------------------------------------- | :------: |
| <a name="input_block_project_ssh_keys"></a> [block_project_ssh_keys](#input_block_project_ssh_keys)    | Blocks the use of project-wide publich SSH keys                                                                                         | `bool`                                                                   | `false`                                                                       |    no    |
| <a name="input_disk_kms_key_self_link"></a> [disk_kms_key_self_link](#input_disk_kms_key_self_link)    | The self link of the encryption key that is stored in Google Cloud KMS                                                                  | `string`                                                                 | `null`                                                                        |    no    |
| <a name="input_domain"></a> [domain](#input_domain)                                                    | Domain to associate Atlantis with and to request a managed SSL certificate for. Without `https://`                                      | `string`                                                                 | n/a                                                                           |   yes    |
| <a name="input_env_vars"></a> [env_vars](#input_env_vars)                                              | Key-value pairs representing environment variables and their respective values                                                          | `map(any)`                                                               | n/a                                                                           |   yes    |
| <a name="input_image"></a> [image](#input_image)                                                       | Docker image. This is most often a reference to a container located in a container registry.                                            | `string`                                                                 | `"ghcr.io/runatlantis/atlantis:latest"`                                       |    no    |
| <a name="input_machine_type"></a> [machine_type](#input_machine_type)                                  | The machine type to run Atlantis on                                                                                                     | `string`                                                                 | `"n2-standard-2"`                                                             |    no    |
| <a name="input_name"></a> [name](#input_name)                                                          | Custom name that's used during resource creation                                                                                        | `string`                                                                 | n/a                                                                           |   yes    |
| <a name="input_network"></a> [network](#input_network)                                                 | Name of the network                                                                                                                     | `string`                                                                 | n/a                                                                           |   yes    |
| <a name="input_persistent_disk_size_gb"></a> [persistent_disk_size_gb](#input_persistent_disk_size_gb) | The size of the persistent disk that Atlantis uses to store its data on                                                                 | `number`                                                                 | `50`                                                                          |    no    |
| <a name="input_project"></a> [project](#input_project)                                                 | The ID of the project in which the resource belongs.                                                                                    | `string`                                                                 | `null`                                                                        |    no    |
| <a name="input_region"></a> [region](#input_region)                                                    | The region that resources should be created in                                                                                          | `string`                                                                 | n/a                                                                           |   yes    |
| <a name="input_service_account"></a> [service_account](#input_service_account)                         | Service account to attach to the instance running Atlantis                                                                              | <pre>object({<br> email = string,<br> scopes = list(string)<br> })</pre> | <pre>{<br> "email": "",<br> "scopes": [<br> "cloud-platform"<br> ]<br>}</pre> |    no    |
| <a name="input_subnetwork"></a> [subnetwork](#input_subnetwork)                                        | Name of the subnetwork to attach a network interface to                                                                                 | `string`                                                                 | n/a                                                                           |   yes    |
| <a name="input_use_spot_machine"></a> [use_spot_machine](#input_use_spot_machine)                      | A Spot VM is discounted Compute Engine capacity that may be preemptively stopped or deleted by Compute Engine if the capacity is needed | `bool`                                                                   | `false`                                                                       |    no    |
| <a name="input_zone"></a> [zone](#input_zone)                                                          | The zone that instances should be created in                                                                                            | `string`                                                                 | n/a                                                                           |   yes    |

## Outputs

| Name                                                              | Description                           |
| ----------------------------------------------------------------- | ------------------------------------- |
| <a name="output_ip_address"></a> [ip_address](#output_ip_address) | The IPv4 address of the load balancer |

<!-- END OF PRE-COMMIT-TERRAFORM DOCS HOOK -->
