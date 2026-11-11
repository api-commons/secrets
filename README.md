# Secrets Management

The common secrets vocabulary -- the secrets an application stores, the versions each one keeps, the stores and vaults that hold them and the encryption keys that protect them -- distilled from the APIs that already exist. Part of [Schema Commons](https://github.com/api-commons/schema-commons),
published by the [API Commons](https://apicommons.org).

Built from the providers tagged Secrets Management, Key Management, Password Management, Vault, Secrets, Encryption, KMS, Password Manager in [APIs.io](https://apis.io) that
publish their own OpenAPI. Only harvested contracts count -- nothing API Evangelist
generated. Every number below is a count of providers.

## What the market already agrees on

<!-- commons:summary -->
| Concept | Expose it | Readable schema | Core properties (share) | Collection named |
| --- | ---: | ---: | --- | --- |
| secret | 9 | 9 | metadata 89%, created_at 78%, id 78%, name 67%, type 67%, updated_at 56% | secrets 8, items 1, secret 1 |
| secret_store | 4 | 4 | id 100%, name 100% | vaults 2, vault 1, environments 1 |
| encryption_key | 3 | 3 | name 100% | keys 2, keyrings 1 |

Cohort: 46 providers with harvested OpenAPI, 11 crosswalks. Of the providers exposing a secret: 78% create, 100% list, 67% fetch, 67% update, 78% delete. Generated 2026-11-11 by build.py.
<!-- /commons:summary -->

Shares are of the providers with a readable resource schema for that concept. The
extended tier and the long tail of every concept are in [profile.yml](profile.yml).

## What the measurement shows

- A secret agrees on name, type, id and timestamps -- and never on its value: providers return secret metadata on the resource and the value through a separate read, so the value does not reach core anywhere.
- Secrets management publishes thinly (46 providers in the cohort, 12 mapped): the cloud providers' secret managers dominate the market and several are absent as OpenAPI.

## Artifacts

- [openapi.yml](openapi.yml) -- OpenAPI 3.1 of the shared operations. No one serves it; it
  is the shape to map to. Lints clean against the
  [naming ruleset](https://github.com/api-commons/schema-commons/blob/main/ruleset/schema-commons-naming.yaml).
- [schema/](schema) -- JSON Schema 2020-12 per concept; each property carries
  `x-commons-tier`, `x-commons-share`, `x-commons-providers` and the spellings seen.
- [crosswalk/](crosswalk) -- one per provider, common name -> their name, with the harvested
  spec and operations each mapping was read from.
- [adopters.yml](adopters.yml) -- who exposes which concept, linked to their APIs.io page.
- [concepts.yml](concepts.yml) -- the only hand-written input: concepts, path segments and
  their qualifiers, aliases, reviewed exclusions, merged duplicates, and the decisions below.
- [census/](census) -- the cohort and the raw census the profile is built from.

## Decisions

These are calls, not measurements, recorded so they can be revisited as the method matures.

- Password-manager items in a vault, credentials and passwords beneath a vault, KV paths and parameter-store parameters are secrets.
- Vaults, safes and secret environments are `/secret-stores`: crypto custody owns the bare word vault in the crypto-wallets context.
- Encryption keys are `/encryption-keys` and count only beneath a KMS, key ring, vault or transit path: identity owns API keys.
- Secret versions were measured and dropped (2 providers).
- Duplicates merged: HVault into HashiCorp Vault.

## Rebuild

```bash
../schema-commons/scripts/run.sh .
```

## License

Artifacts CC BY-NC-SA 4.0 ([LICENSE](LICENSE)); code Apache 2.0 ([LICENSE-CODE](LICENSE-CODE)).
