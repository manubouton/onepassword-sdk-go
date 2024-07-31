<p align="center">
  <a href="https://1password.com">
      <h1 align="center">1Password Go SDK (beta)</h1>
  </a>
</p>

<p align="center">
 <h4 align="center"> ❗ The 1Password SDK project is in beta. Future iterations may bring backwards-incompatible changes.</h4>
</p>

<p align="center">
  <a href="https://developer.1password.com/docs/sdks/">Documentation</a> | <a href="https://github.com/1Password/onepassword-sdk-go/tree/main/example">Examples</a>
<br/>

---

## Supported Functionality

1Password SDKs are in active development. We're keen to hear what you'd like to see next. Let us know by [upvoting](https://github.com/1Password/onepassword-sdk-go/issues) or [filing](https://github.com/1Password/onepassword-sdk-go/issues/new/choose) an issue.

### Item Management
Operations:
- [x] [Retrieve secrets](https://developer.1password.com/docs/sdks/load-secrets)
- [x] [Retrieve Items](https://developer.1password.com/docs/sdks/manage-items#get-an-item)
- [x] [Create Items](https://developer.1password.com/docs/sdks/manage-items#create-an-item)
- [x] [Update Items](https://developer.1password.com/docs/sdks/manage-items#edit-an-item)
- [x] [Delete Items](https://developer.1password.com/docs/sdks/manage-items#delete-an-item)
- [ ] List Items
- [ ] Add & Update tags on items ([#86](https://github.com/1Password/onepassword-sdk-go/issues/86))

Item/field Types:
- [x] API Keys
- [x] Passwords
- [x] Logins
- [x] Notes
- [x] SSH Private Keys
- [ ] SSH Public Keys
- [ ] TOTP codes ([#93](https://github.com/1Password/onepassword-sdk-go/issues/93))
- [ ] Files / Documents ([#108](https://github.com/1Password/onepassword-sdk-go/issues/108))
- [x] URLs
- [x] Credit card number & type
- [x] Phone numbers

### Vault Management
- [ ] Retrieve Vaults
- [ ] Create Vaults
- [ ] Update Vaults
- [ ] Delete Vaults
- [ ] List Vaults

### User & Access Management
- [ ] Provision Users
- [ ] Retrieve Users
- [ ] List Users
- [ ] Suspend Users
- [ ] Create Groups
- [ ] Update Group Membership
- [ ] Update Vault Access & Permissions

### Compliance & Reporting
- [ ] WatchTower Insights
- [ ] Travel Mode
- [ ] Events. For now, check out using [1Password Events Reporting API](https://developer.1password.com/docs/events-api/) directly.

### Authentication

- [x] [1Password Service Accounts](https://developer.1password.com/docs/service-accounts/get-started/)
- [ ] User Authentication
- [ ] 1Password Connect. For now, use [1Password/connect-sdk-go](https://github.com/1Password/connect-sdk-go)

## 🚀 Get started

To use the 1Password Go SDK in your project:

1. [Create a service account](https://my.1password.com/developer-tools/infrastructure-secrets/serviceaccount/) and give it the appropriate permissions in the vaults where the items you want to use with the SDK are saved.
2. Provision your service account token. We recommend provisioning your token from the environment. For example, to export your token to the `OP_SERVICE_ACCOUNT_TOKEN` environment variable:

   **macOS or Linux**

   ```bash
   export OP_SERVICE_ACCOUNT_TOKEN=<your-service-account-token>
   ```

   **Windows**

   ```powershell
   $Env:OP_SERVICE_ACCOUNT_TOKEN = "<your-service-account-token>"
   ```

3. Install the 1Password Go SDK in your project:

   ```bash
   go get github.com/1password/onepassword-sdk-go
   ```

4. Use the Go SDK in your project:

```go
import (
    "context"
    "os"

    "github.com/1password/onepassword-sdk-go"
)

func main() {
    token := os.Getenv("OP_SERVICE_ACCOUNT_TOKEN")

    client, err := onepassword.NewClient(
                context.TODO(),
                onepassword.WithServiceAccountToken(token),
                // TODO: Set the following to your own integration name and version.
                onepassword.WithIntegrationInfo("My 1Password Integration", "v1.0.0"),
    )
    if err != nil {
	// handle err
    }
    secret, err := client.Secrets.Resolve(context.TODO(), "op://vault/item/field")
    if err != nil {
        // handle err
    }
    // do something with the secret
}
```

Make sure to use [secret reference URIs](https://developer.1password.com/docs/cli/secrets-reference-syntax/) with the syntax `op://vault/item/field` to securely load secrets from 1Password into your code.

## 📖 Learn more

- [Load secrets with 1Password SDKs](https://developer.1password.com/docs/sdks/load-secrets)
- [Manage items with 1Password SDKs](https://developer.1password.com/docs/sdks/manage-items)
- [1Password SDK concepts](https://developer.1password.com/docs/sdks/concepts)
