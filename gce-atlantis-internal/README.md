# Atlantis on Google Compute Engine - Internal

<!-- BEGIN_TF_DOCS -->
## Requirements

| Name | Version |
|------|---------|
| <a name="requirement_terraform"></a> [terraform](#requirement\_terraform) | >= 0.13.0 |
| <a name="requirement_cloudinit"></a> [cloudinit](#requirement\_cloudinit) | >=2.2.0 |
| <a name="requirement_google"></a> [google](#requirement\_google) | >=4.79.0 |
| <a name="requirement_google-beta"></a> [google-beta](#requirement\_google-beta) | >=4.79.0 |
| <a name="requirement_random"></a> [random](#requirement\_random) | >=3.4.3 |

## Providers

| Name | Version |
|------|---------|
| <a name="provider_cloudinit"></a> [cloudinit](#provider\_cloudinit) | >=2.2.0 |
| <a name="provider_google"></a> [google](#provider\_google) | >=4.79.0 |
| <a name="provider_google-beta"></a> [google-beta](#provider\_google-beta) | >=4.79.0 |
| <a name="provider_random"></a> [random](#provider\_random) | >=3.4.3 |

## Modules

| Name | Source | Version |
|------|--------|---------|
| <a name="module_container"></a> [container](#module\_container) | terraform-google-modules/container-vm/google | 3.1.1 |

## Resources

| Name | Type |
|------|------|
| [google-beta_google_compute_backend_service.iap_external](https://registry.terraform.io/providers/hashicorp/google-beta/latest/docs/resources/google_compute_backend_service) | resource |
| [google-beta_google_compute_instance_group_manager.default](https://registry.terraform.io/providers/hashicorp/google-beta/latest/docs/resources/google_compute_instance_group_manager) | resource |
| [google-beta_google_compute_region_backend_service.default](https://registry.terraform.io/providers/hashicorp/google-beta/latest/docs/resources/google_compute_region_backend_service) | resource |
| [google-beta_google_compute_region_backend_service.iap_internal](https://registry.terraform.io/providers/hashicorp/google-beta/latest/docs/resources/google_compute_region_backend_service) | resource |
| [google_compute_firewall.lb_health_check](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/compute_firewall) | resource |
| [google_compute_forwarding_rule.https_internal](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/compute_forwarding_rule) | resource |
| [google_compute_global_address.default](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/compute_global_address) | resource |
| [google_compute_global_forwarding_rule.https_external](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/compute_global_forwarding_rule) | resource |
| [google_compute_health_check.default](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/compute_health_check) | resource |
| [google_compute_health_check.default_instance_group_manager](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/compute_health_check) | resource |
| [google_compute_instance_template.default](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/compute_instance_template) | resource |
| [google_compute_managed_ssl_certificate.default](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/compute_managed_ssl_certificate) | resource |
| [google_compute_region_target_https_proxy.default_internal](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/compute_region_target_https_proxy) | resource |
| [google_compute_region_url_map.default_internal](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/compute_region_url_map) | resource |
| [google_compute_route.public_internet](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/compute_route) | resource |
| [google_compute_target_https_proxy.default_external](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/compute_target_https_proxy) | resource |
| [google_compute_url_map.default_external](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/compute_url_map) | resource |
| [random_string.random](https://registry.terraform.io/providers/hashicorp/random/latest/docs/resources/string) | resource |
| [cloudinit_config.config](https://registry.terraform.io/providers/hashicorp/cloudinit/latest/docs/data-sources/config) | data source |
| [google_compute_image.cos](https://registry.terraform.io/providers/hashicorp/google/latest/docs/data-sources/compute_image) | data source |
| [google_netblock_ip_ranges.this](https://registry.terraform.io/providers/hashicorp/google/latest/docs/data-sources/netblock_ip_ranges) | data source |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| <a name="input_block_project_ssh_keys_enabled"></a> [block\_project\_ssh\_keys\_enabled](#input\_block\_project\_ssh\_keys\_enabled) | Blocks the use of project-wide publich SSH keys | `bool` | `false` | no |
| <a name="input_default_backend_security_policy"></a> [default\_backend\_security\_policy](#input\_default\_backend\_security\_policy) | Name of the security policy to apply to the default backend service | `string` | `null` | no |
| <a name="input_disk_kms_key_self_link"></a> [disk\_kms\_key\_self\_link](#input\_disk\_kms\_key\_self\_link) | The self link of the encryption key that is stored in Google Cloud KMS | `string` | `null` | no |
| <a name="input_domain"></a> [domain](#input\_domain) | Domain to associate Atlantis with and to request a managed SSL certificate for. Without `https://` | `string` | n/a | yes |
| <a name="input_enable_confidential_vm"></a> [enable\_confidential\_vm](#input\_enable\_confidential\_vm) | Enable Confidential VM. If true, on host maintenance will be set to TERMINATE | `bool` | `false` | no |
| <a name="input_enable_external_load_balancer"></a> [enable\_external\_load\_balancer](#input\_enable\_external\_load\_balancer) | Enables external Load Balancer to allow external connection to the Atlantis UI. IAP has to be configured to use this option. | `bool` | `false` | no |
| <a name="input_enable_oslogin"></a> [enable\_oslogin](#input\_enable\_oslogin) | Enables OS Login service on the VM | `bool` | `false` | no |
| <a name="input_env_vars"></a> [env\_vars](#input\_env\_vars) | Key-value pairs representing environment variables and their respective values | `map(any)` | n/a | yes |
| <a name="input_expose_healthz_publicly"></a> [expose\_healthz\_publicly](#input\_expose\_healthz\_publicly) | Exposes the /healthz endpoint publicly even if Atlantis is protected by IAP | `bool` | `false` | no |
| <a name="input_expose_metrics_publicly"></a> [expose\_metrics\_publicly](#input\_expose\_metrics\_publicly) | Exposes the /metrics endpoint publicly even if Atlantis is protected by IAP | `bool` | `false` | no |
| <a name="input_google_logging_enabled"></a> [google\_logging\_enabled](#input\_google\_logging\_enabled) | Enable Google Cloud Logging | `bool` | `true` | no |
| <a name="input_google_logging_use_fluentbit"></a> [google\_logging\_use\_fluentbit](#input\_google\_logging\_use\_fluentbit) | Enable Google Cloud Logging using Fluent Bit | `bool` | `false` | no |
| <a name="input_google_monitoring_enabled"></a> [google\_monitoring\_enabled](#input\_google\_monitoring\_enabled) | Enable Google Cloud Monitoring | `bool` | `true` | no |
| <a name="input_iap"></a> [iap](#input\_iap) | Settings for enabling Cloud Identity Aware Proxy to protect the Atlantis UI | <pre>object({<br>    oauth2_client_id     = string<br>    oauth2_client_secret = string<br>  })</pre> | `null` | no |
| <a name="input_iap_backend_security_policy"></a> [iap\_backend\_security\_policy](#input\_iap\_backend\_security\_policy) | Name of the security policy to apply to the IAP backend service | `string` | `null` | no |
| <a name="input_image"></a> [image](#input\_image) | Docker image. This is most often a reference to a container located in a container registry | `string` | `"ghcr.io/runatlantis/atlantis:latest"` | no |
| <a name="input_labels"></a> [labels](#input\_labels) | Key-value pairs representing labels attaching to instance & instance template | `map(any)` | `{}` | no |
| <a name="input_machine_image"></a> [machine\_image](#input\_machine\_image) | The machine image to create VMs with, if not specified, latest cos\_cloud/cos\_stable is used | `string` | `null` | no |
| <a name="input_machine_type"></a> [machine\_type](#input\_machine\_type) | The machine type to run Atlantis on | `string` | `"n2-standard-2"` | no |
| <a name="input_name"></a> [name](#input\_name) | Custom name that's used during resource creation | `string` | n/a | yes |
| <a name="input_network"></a> [network](#input\_network) | Name of the network | `string` | n/a | yes |
| <a name="input_persistent_disk_size_gb"></a> [persistent\_disk\_size\_gb](#input\_persistent\_disk\_size\_gb) | The size of the persistent disk that Atlantis uses to store its data on | `number` | `50` | no |
| <a name="input_persistent_disk_type"></a> [persistent\_disk\_type](#input\_persistent\_disk\_type) | The type of persistent disk that Atlantis uses to store its data on | `string` | `"pd-ssd"` | no |
| <a name="input_project"></a> [project](#input\_project) | The ID of the project in which the resource belongs | `string` | `null` | no |
| <a name="input_region"></a> [region](#input\_region) | The region that resources should be created in | `string` | n/a | yes |
| <a name="input_service_account"></a> [service\_account](#input\_service\_account) | Service account to attach to the instance running Atlantis | <pre>object({<br>    email  = string,<br>    scopes = list(string)<br>  })</pre> | <pre>{<br>  "email": "",<br>  "scopes": [<br>    "cloud-platform"<br>  ]<br>}</pre> | no |
| <a name="input_shared_vpc"></a> [shared\_vpc](#input\_shared\_vpc) | Whether to deploy within a shared VPC | <pre>object({<br>    host_project_id = string<br>  })</pre> | `null` | no |
| <a name="input_shielded_instance_config"></a> [shielded\_instance\_config](#input\_shielded\_instance\_config) | Shielded VM provides verifiable integrity to prevent against malware and rootkits | <pre>object({<br>    enable_integrity_monitoring = optional(bool)<br>    enable_vtpm                 = optional(bool)<br>    enable_secure_boot          = optional(bool)<br>  })</pre> | <pre>{<br>  "enable_integrity_monitoring": true,<br>  "enable_secure_boot": true,<br>  "enable_vtpm": true<br>}</pre> | no |
| <a name="input_spot_machine_enabled"></a> [spot\_machine\_enabled](#input\_spot\_machine\_enabled) | A Spot VM is discounted Compute Engine capacity that may be preemptively stopped or deleted by Compute Engine if the capacity is needed | `bool` | `false` | no |
| <a name="input_ssl_policy"></a> [ssl\_policy](#input\_ssl\_policy) | The SSL policy name that the certificate must follow | `string` | `null` | no |
| <a name="input_startup_script"></a> [startup\_script](#input\_startup\_script) | A startup script that runs during the boot cycle when you first launch an instance | `string` | `null` | no |
| <a name="input_subnetwork"></a> [subnetwork](#input\_subnetwork) | Name of the subnetwork to attach a network interface to | `string` | n/a | yes |
| <a name="input_tags"></a> [tags](#input\_tags) | Tags to attach to the instance running Atlantis | `list(string)` | `[]` | no |
| <a name="input_zone"></a> [zone](#input\_zone) | The zone that instances should be created in | `string` | n/a | yes |

## Outputs

| Name | Description |
|------|-------------|
| <a name="output_cos_image_id"></a> [cos\_image\_id](#output\_cos\_image\_id) | The unique identifier of the Container-Optimized OS image used to create the Compute Engine instance. |
| <a name="output_iap_backend_service_name"></a> [iap\_backend\_service\_name](#output\_iap\_backend\_service\_name) | Name of the optional IAP-enabled backend service |
| <a name="output_ip_address"></a> [ip\_address](#output\_ip\_address) | The IPv4 address of the load balancer |
| <a name="output_managed_ssl_certificate_certificate_id"></a> [managed\_ssl\_certificate\_certificate\_id](#output\_managed\_ssl\_certificate\_certificate\_id) | The unique identifier of the Google Managed SSL certificate |
| <a name="output_managed_ssl_certificate_expire_time"></a> [managed\_ssl\_certificate\_expire\_time](#output\_managed\_ssl\_certificate\_expire\_time) | Expire time of the Google Managed SSL certificate |
<!-- END_TF_DOCS -->