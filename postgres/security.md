##### SSL Mode role on security

`sslmode` is a parameter used in database configurations (especially in PostgreSQL) to determine how SSL/TLS encryption is handled when connecting to a database server. It defines the level of security for the connection.
`disable` – No SSL encryption; the connection is in plaintext.
`allow` – Uses an SSL connection if available, but falls back to an unencrypted connection if SSL is not supported.
`prefer` – Prefers an SSL connection but allows unencrypted if SSL is unavailable.
`require` – Always uses SSL but does not verify the certificate.
`verify-ca` – Uses SSL and verifies the certificate authority (CA).
