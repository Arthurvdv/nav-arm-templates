# Business Central/NAV ARM Templates

In order to deploy ARM templates from this repository (or your fork), use the standard Azure portal deployment URL:
`https://portal.azure.com/#create/Microsoft.Template/uri/<url-encoded-template-url>`

Where `<url-encoded-template-url>` is the URL-encoded raw URL of the template, e.g. the URL-encoded form of
`https://raw.githubusercontent.com/<githubusername>/nav-arm-templates/<branch>/<template>.json`

Where
- `<githubusername>` is the GitHub user name (use `microsoft` for the original templates, or your own user name for a fork)
- `<branch>` is the branch you want to deploy from
- `<template>` is the name of the template to use

## Available templates

| Name | Description |
|---|---|
| getbc | Get Azure VM with Business Central on Docker with standard questionnaire |
| getbcext | Get Azure VM with Business Central on Docker with extended questionnaire |
| buildagent | Get Azure VM pre-configured as Build Agent for GitHub or Azure DevOps |
| getnav | Get Azure VM with NAV on Docker with standard questionnaire |
| getnavext | Get Azure VM with NAV on Docker with extended questionnaire |

**Note:** After opening the deployment URL, the Azure portal will prompt you for the values of the fields in the ARM template.

## VM generation, OS and sizes

- **Windows Server 2025** and **2022** deploy Gen2 images with **Trusted Launch** (Secure Boot + vTPM). **Windows Server 2019** stays on a Gen1 image.
- The VM size list only contains current 4, 8 and 16 vCPU sizes (Dsv5, Dasv5, Dsv6, Dasv6, Dsv7, Dasv7, Esv5, Esv6, Easv6 and Easv7). The default is `Standard_D4s_v6`; `Standard_E4as_v6` (4 vCPU / 32 GB) gives more headroom. Not every size is available in every region.
- v6/v7 sizes are Gen2 only and use an NVMe disk controller (set automatically). **Windows Server 2019 requires a v5 size.**
- The extension command line, including passwords and keys, is passed via `protectedSettings`, so it is no longer readable from the VM's extension settings.

getbcext only:
- `StorageAccountType` now selects the OS disk type: `StandardSSD_LRS` (default), `Premium_LRS` or `Standard_LRS` (HDD).
- `OsDiskSizeGB` sets the OS disk size (128 or 256 GB).
- Accelerated networking and managed boot diagnostics are enabled, and the unused `storage<uniqueString>` storage account is no longer created.
- Deleting the VM still leaves the OS disk, NIC and public IP behind (delete option Detach).

## Examples
- getbc -> https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmicrosoft%2Fnav-arm-templates%2Fmaster%2Fgetbc.json
- buildagent -> https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmicrosoft%2Fnav-arm-templates%2Fmaster%2Fbuildagent.json

# Contributing

This project welcomes contributions and suggestions.  Most contributions require you to agree to a
Contributor License Agreement (CLA) declaring that you have the right to, and actually do, grant us
the rights to use your contribution. For details, visit https://cla.microsoft.com.

When you submit a pull request, a CLA-bot will automatically determine whether you need to provide
a CLA and decorate the PR appropriately (e.g., label, comment). Simply follow the instructions
provided by the bot. You will only need to do this once across all repos using our CLA.

This project has adopted the [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct/).
For more information see the [Code of Conduct FAQ](https://opensource.microsoft.com/codeofconduct/faq/) or
contact [opencode@microsoft.com](mailto:opencode@microsoft.com) with any additional questions or comments.
