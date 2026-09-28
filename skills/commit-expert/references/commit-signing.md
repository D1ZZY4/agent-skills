# Commit Signing

Signed commits are repository-specific requirements. Do not turn signing into a universal default.

## When signing applies

Inspect the effective configuration before assuming how commits are signed:

```bash
git config --show-origin --get commit.gpgSign
git config --show-origin --get gpg.format
git config --show-origin --get user.signingkey
```

When relevant to the configured signing format, inspect additional signer configuration without
changing it.

Interpretation:

- `commit.gpgSign=true` enables signing for new commits by default
- a repository policy may require signing even when that boolean is not set
- `-S` requests signing for a particular commit
- do not add signing merely because the skill can sign

## Preserve the existing signer

Do not replace:

- `user.signingkey`
- `gpg.format`
- `gpg.program`
- SSH signing configuration
- signer environment variables or keyrings

merely to make a commit succeed.

If the configured signer cannot produce a valid signature:

1. report the actual failure
2. do not silently substitute another key
3. obtain explicit authorization before changing signing configuration

## Keyring and program consistency

Use the same signing environment for signing and verification.

For example, if the environment depends on a configured GPG program, SSH signer, keyring, or
`GNUPGHOME`, do not switch to a different environment just for verification.

## Verify before push

For the commit or commit range that will be pushed:

```bash
git log --show-signature --oneline <range>
```

For a single latest commit:

```bash
git log --show-signature -1
```

A successful local signature check proves that Git could verify the cryptographic signature under the
active environment. It does not by itself guarantee that a hosting provider will display a "verified"
badge under its own account or trust rules.

Report the actual result. Never invent a key, trust relationship, or provider verification state.

## Unsigned or failed signatures

If repository policy requires valid signatures, do not push an unsigned or locally failed commit
unless the user explicitly authorizes the exception after being told what is wrong.

That exception does not change the repository policy.

## Configuration changes

Changing signer identity, signing keys, `gpg.program`, `commit.gpgSign`, credentials, or related
configuration is a separate mutation.

Explain the intended change, confirm the target, and obtain explicit authorization before changing it.

Never change global configuration merely to satisfy a repository-local requirement.
