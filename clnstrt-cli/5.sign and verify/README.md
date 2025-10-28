Sign images for authenticity and verify their integrity.
For image signing and verification, both a public key and a private key are required.

#### sign - Image Signing

What it does: Cryptographically signs an image to attest integrity and provenance.

```bash
# Sign image (requires key file)
clnstrt sign -k private.key image:tag
# Sign with config
clnstrt sign -k private.key -c sign-config.yaml image:tag
```

Purpose: Signs the container image to provide authenticity and ensure it can be verified using the corresponding public key.
How It Works: The clnstrt sign command uses the provided private key (private-key.pem) to create a cryptographic signature for the specified image (test-image:latest). This signature is embedded with the image's metadata. Signing an image allows users or systems to later verify its authenticity and integrity with the matching public key.
Outcome: The image is signed successfully, and the signature is attached to it. This signature can later be verified using the clnstrt verify command and the corresponding public key.


#### verify - Image Verification

What it does: Verifies an image’s signature using a public key to ensure trust.

```bash
# Verify image signature (requires public key)
clnstrt verify -k public.key image:tag
# Verify with config
clnstrt verify -k public.key -c verify-config.yaml image:tag
```

Required: Public key file for verification.


Purpose: Verifies the authenticity and integrity of the image using a provided public key.
How It Works: The clnstrt verify command takes the specified image (test-image:latest) and checks its signature against the provided public key (public-key.pem). This process confirms that the image was signed with the corresponding private key and ensures that the image has not been tampered with or altered after signing.
Outcome: The command outputs a verification status indicating whether the signature is valid and if the image is intact. If successful, it confirms that the image's integrity is maintained.