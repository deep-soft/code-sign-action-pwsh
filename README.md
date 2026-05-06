# File Sign Action (pwsh Set-AuthenticodeSignature)
Author: acornbytes (https://github.com/acornbytes/pwsh-sign-action)
This action will sign files matching provided globs, using the Set-AuthenticodeSignature pwsh cmdlet with a password-protected PFX certificate.

All sensitive inputs should be stored using GitHub secrets.

# Inputs

| Key                | Description                                                                         | Required                                                                                                       |
| ------------------ | ----------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------- |
| `cert_base64`      | A Base64 encoded string for the byte content of a **PFX** code signing certificate. | This **or** `cert_path` must be provided.                                                                      |
| `cert_path`        | The absolute path to a **PFX** code signing certificate.                            | This **or** `cert_base64` must be provided - if `cert_path` is provided then it takes priority and must exist. |
| `cert_password`    | The password to the associated PFX certificate                                      | Yes                                                                                                            |
| `sign_globs`       | A comma-separated collection of globs to sign. e.g. `bin/release/*.dll,dist/*js`    | Yes                                                                                                            |
| `hash`             | The code signing hashing algorithm to use - defaults to `SHA256` if omitted.        | No                                                                                                             |
| `timestamp_server` | The timestamp server to use for signing. Defaults to `http://timestamp.sectigo.com` | No                                                                                                             |

# Example

> [!IMPORTANT]  
> This action must be executed on a windows runner.

```
runs-on: windows-latest
steps:
  uses: acornbytes/pwsh-sign-action@1.0
  with:
    cert_path: ${{ github.workspace }}/certificate.pfx
    cert-password: ${{ secrets.CERT_PWD }}
    sign_globs: '*.exe,*dll,release/*.exe'
    hash: SHA256
    timestamp-server: http://timestamp.sectigo.com
```

# Licence

This project is released under the [MIT License](LICENSE)
