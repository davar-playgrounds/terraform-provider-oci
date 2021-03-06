---
subcategory: "Kms"
layout: "oci"
page_title: "Oracle Cloud Infrastructure: oci_kms_verify"
sidebar_current: "docs-oci-resource-kms-verify"
description: |-
  Provides the Verify resource in Oracle Cloud Infrastructure Kms service
---

# oci_kms_verify
This resource provides the Verify resource in Oracle Cloud Infrastructure Kms service.

Verifies a digital signature that was generated by the Sign operation using the public key in the same asymmetric key.
You can also verify the digital signature by using the public key in the asymmetric key outside of KMS


## Example Usage

```hcl
resource "oci_kms_verify" "test_verify" {
	#Required
  crypto_endpoint = var.verify_message_crypto_endpoint
	key_id = oci_kms_key.test_key.id
	key_version_id = oci_kms_key_version.test_key_version.id
	message = var.verify_message
	signature = var.verify_signature
	signing_algorithm = var.verify_signing_algorithm

	#Optional
	message_type = var.verify_message_type
}
```

## Argument Reference

The following arguments are supported:

* `crypto_endpoint` - (Required) The service endpoint to perform cryptographic operations against. Cryptographic operations include 'Encrypt,' 'Decrypt,', 'GenerateDataEncryptionKey', 'Sign' and 'Verify' operations. see Vault Crypto endpoint.
* `key_id` - (Required) The OCID of the key used to sign the message
* `key_version_id` - (Required) The OCID of the keyVersion used to sign the message
* `message` - (Required) The Base64-encoded binary data object denoting the message or message digest to be signed. Message can be upto 4096 size in bytes. To sign a larger message, provide the message digest.
* `message_type` - (Optional) Denotes whether the value of the message parameter is a raw message or a message digest. The default value, RAW, indicates a message. To indicate a message digest, enter DIGEST.
* `signature` - (Required) The Base64-encoded binary data object denoting the cryptographic signature that was generated for the message. 
* `signing_algorithm` - (Required) The algorithm to be used for signing the message or message digest For RSA keys, there are two supported Signature Schemes: PKCS1 and PSS along with  different Hashing algorithms.  For ECDSA keys, ECDSA is the supported signature scheme with different hashing algorithms. In case of passing digest for signing, make sure the same hashing algorithm is  specified as used for created for digest.       


** IMPORTANT **
Any change to a property that does not support update will force the destruction and recreation of the resource with the new property values

## Attributes Reference

The following attributes are exported:

* `is_signature_valid` - A Boolean value that indicates whether the signature was verified.

## Import

Verify can be imported using the `id`, e.g.

```
$ terraform import oci_kms_verify.test_verify "id"
```

