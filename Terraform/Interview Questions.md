1. What are Terraform Modules?

Answer:
Terraform modules are reusable pieces of Terraform code that help organize infrastructure as code. Instead of writing the same configuration repeatedly, you can put it inside a module and use it multiple times across different projects.

Example: If you need to create multiple EC2 instances with similar configurations, you can create an "EC2 Module" and reuse it instead of copying the same code.

Memory Trigger: "Reusable building blocks of Terraform."

2. What is a Terraform State File or Remote State or Terraform Backend?

Answer:
Terraform maintains a state file (terraform.tfstate) to track the real-world infrastructure. This state helps Terraform understand what resources exist and what needs to change.

Local State: Stored on your machine (default).

Remote State: Stored in a backend (like AWS S3, Azure Storage, or Terraform Cloud) for team collaboration.

Terraform Backend: A storage system where Terraform saves its state remotely.

Example: Using AWS S3 + DynamoDB as a backend helps multiple developers work safely without conflicts.

Memory Trigger: "State file = Infrastructure tracker, Backend = Remote storage."

3. What is a Terraform Workspace?

Answer:
Terraform Workspaces allow you to maintain multiple states for the same configuration. Instead of creating separate folders for dev, staging, and prod, you can switch between environments using workspaces.

Example:

terraform workspace new dev (creates a new workspace for development)

terraform workspace select dev (switches to the dev workspace)

Memory Trigger: "Workspaces = Multiple states in one config."

4. How do you handle secrets in Terraform?

Answer:
Terraform stores everything, including secrets, in the state file, which can be a security risk. To handle secrets securely:

Use environment variables: Pass secrets using TF_VAR_secret_name instead of hardcoding.

Use Terraform Vault Provider: Store secrets in HashiCorp Vault.

Use AWS Secrets Manager / Azure Key Vault: Fetch secrets securely at runtime.

Use sensitive variables: Mark variables as sensitive = true to prevent them from being printed.

Memory Trigger: "Never hardcode, always secure secrets."

5. What is Terraform Taint?

Answer:
Terraform taint marks a resource for recreation in the next terraform apply. It is useful when a resource is corrupted or needs a fresh deployment.

Command:

terraform taint aws_instance.example (marks an EC2 instance for recreation)

terraform apply (destroys and recreates the tainted resource)

Memory Trigger: "Taint = Force recreate a resource."

6. What are the major issues you faced in Terraform?

Answer:

State file conflicts: When multiple people edit the state file at the same time. (Solution: Use a remote state with locking, like S3 + DynamoDB).

Secrets in state files: Terraform saves sensitive data in plain text. (Solution: Use Vault or Secrets Manager).

Drift issues: When someone changes infrastructure outside Terraform, it causes a state mismatch. (Solution: Use terraform refresh to sync state).

Provider version conflicts: Different team members use different Terraform versions. (Solution: Lock provider versions in terraform.required_providers).

Memory Trigger: "State conflicts, secrets, drift, and versions."

7. What is Terraform Import, and when do we use it?

Answer:
Terraform import is used to bring an already existing cloud resource into Terraform’s state file. However, it does not generate Terraform code automatically—you must write the code manually.

Example: If an EC2 instance was created manually, you can import it into Terraform like this:

```terraform import aws_instance.my_ec2 i-1234567890abcdef0```

Memory Trigger: "Import = Bring existing resources into Terraform."
