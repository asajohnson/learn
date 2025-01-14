Infrastructure as Code (IaC) is the process of managing and provisioning cloud-infrastructure
resources through machine-readable code that's stored in source control. The ability to treat your
infrastructure as you would any other source code is why this practice is called **Infrastructure as
Code**.

IaC is a key component of DevOps, as it allows for the automation of infrastructure configuration
and deployment. This automation reduces the amount of time and effort required to manage and
provision infrastructure, while also ensuring that the infrastructure is configured consistently and
reliably. IaC also helps to ensure that the infrastructure is secure and compliant with
organizational policies. By using IaC, organizations can deploy and manage their infrastructure,
while also ensuring that it's secure and compliant.

## Azure-native vs cloud-agnostic tools

One of the most important factors in choosing an IaC tool is your cloud environment.

- **Azure-native tools:** IaC tools such as the Azure CLI, Azure PowerShell, and Bicep are available
  only on Azure. The benefits of the cloud infrastructure and IaC tool both being provided from the
  same company is reduced time between cloud feature release and support in the tools.

- **Cloud-agnostic tools:** IaC tools such as Terraform allow you to manage infrastructure as code
  across mixed-cloud environments. Depending on the IaC tool, newly released Azure features may not
  be immediately supported.

## Imperative vs declarative IaC tools

There are two types of IaC configuration tools. When using an imperative IaC tool, you write code
that specifies how to configure your infrastructure step by step. Whereas when using a declarative
IaC tool, you write code that specifies the desired state for your infrastructure.

- **Imperative IaC tools:** An imperative tool, or language, is one where the code explicitly
  specifies what's to be done and how. The code you write performs actions in a specific order, one
  step at a time to configure your infrastructure. Most imperative IaC tools aren't idempotent
  because the configuration is performed step by step.

  Imperative IaC tools to manage and provision resources in Azure include:

  - The Azure CLI
  - Azure PowerShell

- **Declarative IaC tools:** A declarative tool, or language, allows you to specify the desired
  outcome rather than how you want each step accomplished. Most declarative IaC tools adhere to a
  common pattern. Once you create the definition of your infrastructure, you run a command to
  provision what you've defined. Declarative IaC tools are idempotent as the configuration can be
  applied multiple times regardless of the state of the infrastructure's configuration. This allows
  you to prevent configuration drift by bringing non-compliant infrastructure back into compliance.

  Declarative IaC tools to manage and provision resources in Azure include:

  - Bicep
  - Terraform

## Recommendations

- Adopt an IaC approach to deploying, managing, governing, and supporting Azure deployments.
- Use Azure native tools for IaC in the following scenarios:
  - You want to use only Azure native tools. Your organization has prior ARM template deployment
    experience.
  - Your organization wants to have immediate support for all preview and GA versions of Azure services.
- Use non-native tools for IaC in the following scenarios:
  - Your organization manages infrastructure across mixed-cloud environments.
  - Your organization doesn't need to have immediate support for all preview and GA versions of
    Azure services.
