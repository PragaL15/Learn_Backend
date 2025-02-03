
**Storing as BYTEA**	-> Easier to manage and secure	Increases database size, reduces performance
**Storing Image URL** ->	Scales better, reduces DB size	Needs external storage (file system, cloud)
- Recommended: Store images on cloud (AWS S3, Google Cloud Storage) and save only the URL in PostgreSQL.