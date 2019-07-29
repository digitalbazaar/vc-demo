# Verifiable Credentials Demo

Demonstrates how to issue and verify Verifiable Credentials.

WARNING: No part of this demo should be used in production systems.
         Generated private keys are not encrypted by default.

## System Requirements

- A 64-bit system
- git >= v2.x
- docker >= 18.x

## Getting Started

Running this demo consists of:

1. Cloning the repository.
2. Getting a GitHub Personal Access Token.
3. Generating a public/private keypair.
4. Issuing a Verifiable Credential.
5. Verifying the Verifiable Credential.

### Cloning the Repository

```
git clone git@github.com:digitalbazaar/vc-demo.git
cd vc-demo
```

The rest of this demo assumes that you have created the following command
line alias:

```
alias vc="docker run digitalbazaar/vc-js-cli"
```

### Getting a GitHub Personal Access Token

This demo will publish newly generated key and controller documents as a gists
under your GitHub account. This requires a
[GitHub Personal Access Token](https://help.github.com/en/articles/creating-a-personal-access-token-for-the-command-line)
with *only* the `gist` scope enabled.

### Generate a keypair

You will need to generate a public-private keypair to run this demo.
Once the keypair is created, the public key will be published to
a gist under your GitHub account using the GitHub Personal Access
Token you created in the previous step. The private key information
as well as where the public key was published will be saved locally
as `my-key.json`.

#### Generate an Ed25519 keypair
```
vc keygen --key-type ed25519 --git-hub-token YOUR_GITHUB_TOKEN
```
#### Generate a Secp256k1 keypair
```
vc keygen --key-type secp256k1 --git-hub-token YOUR_GITHUB_TOKEN
```

### Issue a Verifiable Credential

Once your keypair has been generated and the public information
has been published, you can use it to issue Verifiable Credentials.

The `credentials` directory stores a number of template credentials
that can be used with the `issue` command. To issue a
Verifiable Credential, you can execute the following command:

```
vc issue --key my-key.json < credentials/alumni.jsonld > alumni-signed.jsonld
```

The command above will create a file called `alumni-signed.jsonld`,
consisting of the issued Verifiable Credential.

### Verify a Verifiable Credential

To verify a Verifiable Credential, the following command can be used:

```
vc verify --verbose < alumni-signed.jsonld
```

The verification result will be printed to the screen.
