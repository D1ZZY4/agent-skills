# Commit Signing

How to handle signed commits when a repository requires them, from inspection through
verification before push.

## When signing applies

Signed commits are repository-specific policy, not a portable default. Check the repository's
Git configuration before assuming:

```bash
git config --get commit.gpgSign
git config --get gpg.format
git config --get user.signingkey
```

- `commit.gpgSign` true means new commits are signed automatically.
- If repository policy requires a signature for your commits, pass `-S` on the commit.
- If the repository does not require signing, leave signing alone. Do not add it as a default.

## Signing mechanics

- Keep the environment's signing setup intact. If the host resolves gpg through a wrapper,
  `GNUPGHOME`, or a specific `gpg.program`, use that same tool for both signing and
  verification. Switching to a different keyring only makes the key look missing.
- Preserve the repository's configured `user.signingkey`. Never sign with an invented key or
  substitute your own key unless the user explicitly configures it.

## Verify before push

```bash
git log --show-signature -1
```

- Report "Good signature" with the actual key when it verifies.
- Report the real failure when it does not. Never invent a trust model or a signature result.
- Only push a signed commit whose signature reports a good result, unless the user explicitly
  accepts an unsigned or failed-signature push after being told how the repository is
  configured.

## Safety boundary

Changing signing configuration (identity, keys, `gpg.program`, `commit.gpgSign`, credentials)
is a separate mutation. Explain the change, confirm the target, and get explicit approval
first. Never change global config to satisfy a local policy. See `policy-configuration.md` for
where signing fits in the policy precedence order.
