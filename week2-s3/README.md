# 📦 Week 2 - Amazon S3 (Simple Storage Service)

![Status](https://img.shields.io/badge/Status-Completed-brightgreen)
![Topic](https://img.shields.io/badge/Topic-S3%20Storage-blue)

## 🎯 Overview
This week I did a deep dive into Amazon S3 — AWS's core object storage 
service. I explored its architecture, storage classes, security model, 
versioning, and static website hosting capabilities through hands-on practice.

---

## 📖 What I Learned

### 🪣 1. What is Amazon S3?
S3 (Simple Storage Service) is a highly scalable, durable object storage 
service. Unlike traditional file systems (which use folders/directories), 
S3 stores data as **objects** inside flat containers called **buckets**. 
It offers **99.999999999% (11 nines) durability**, meaning your data is 
extremely unlikely to be lost.

S3 is used for:
- Backup and disaster recovery
- Static website hosting
- Data lakes and big data analytics
- Storing media files (images, videos)
- Software delivery and application data storage

### 📁 2. Core Concepts

| Term | Meaning |
|------|---------|
| **Bucket** | A globally unique-named container that holds objects |
| **Object** | The actual file + its metadata (size, type, last modified, etc.) |
| **Key** | The unique identifier (like a file path) for an object within a bucket |
| **Region** | The physical AWS location where a bucket's data resides |
| **ARN** | Amazon Resource Name — a unique identifier for the bucket/object across AWS |

**Important:** Bucket names must be **globally unique** across all AWS 
accounts (not just your own), since S3 uses a shared global namespace.

### 🗂️ 3. Storage Classes (Cost vs Access Trade-off)
S3 offers multiple storage tiers optimized for different access patterns 
and cost requirements:

| Storage Class | Best For | Retrieval Time |
|----------------|----------|-----------------|
| **S3 Standard** | Frequently accessed data | Milliseconds |
| **S3 Intelligent-Tiering** | Unknown/changing access patterns | Automatic |
| **S3 Standard-IA** | Infrequent access, but needed quickly | Milliseconds |
| **S3 One Zone-IA** | Infrequent, non-critical data (single AZ) | Milliseconds |
| **S3 Glacier Instant Retrieval** | Archive data needing instant access | Milliseconds |
| **S3 Glacier Flexible Retrieval** | Archival, retrieved a few times a year | Minutes to hours |
| **S3 Glacier Deep Archive** | Long-term archival (7-10 years), cheapest | Hours |

Choosing the right class helps optimize storage costs significantly for 
large-scale applications.

### 🔐 4. Security & Access Control
S3 buckets are **private by default**. Access is controlled through 
multiple layers:

- **Bucket Policies** - JSON-based resource policies attached directly 
  to a bucket, defining who can perform which actions
- **IAM Policies** - Attached to IAM users/roles, controlling their 
  access to S3 resources
- **Access Control Lists (ACLs)** - Legacy method for granting basic 
  read/write permissions (AWS now recommends Bucket Policies instead)
- **Block Public Access** - An account/bucket-level setting that 
  prevents accidental public exposure, even if a policy allows it
- **Pre-signed URLs** - Temporary URLs that grant time-limited access 
  to a specific object without making the bucket public

### 🔄 5. Versioning
S3 Versioning keeps multiple versions of an object in the same bucket. 
When enabled:
- Every update creates a new version instead of overwriting the old one
- Accidental deletes only add a "delete marker" — the previous version 
  can still be restored
- Useful for protecting against accidental overwrites or deletions

### 🌐 6. Static Website Hosting
S3 can host static websites (HTML, CSS, JS) directly without needing a 
traditional web server:
- Requires enabling "Static website hosting" in bucket properties
- Needs an **index document** (e.g. `index.html`) and optionally an 
  **error document** (e.g. `error.html`)
- The bucket must be made public (via bucket policy) for visitors to 
  access the site
- Often paired with **CloudFront** (CDN) for faster global delivery, 
  HTTPS support, and custom domain names

### ⚡ 7. Lifecycle Policies
Lifecycle rules automate moving objects between storage classes or 
deleting them after a set period — e.g., automatically moving logs 
older than 30 days to Glacier, or deleting temp files after 7 days. 
This helps reduce storage costs without manual intervention.

### 🧩 8. S3 and Other AWS Services
S3 integrates closely with other services I've been learning about:
- **CloudFront** - CDN that caches S3 content at edge locations
- **IAM** - Controls who can access S3 resources
- **Lambda** - Can be triggered automatically when objects are 
  uploaded/deleted in a bucket (event-driven architecture)

---

## 🛠️ Hands-on Steps I Practiced
- [x] Created an S3 bucket with a globally unique name
- [x] Uploaded and organized files (objects) inside the bucket
- [x] Enabled Static Website Hosting and set index/error documents
- [x] Configured a Bucket Policy to allow public read access for the website
- [x] Tested Block Public Access settings
- [x] Enabled Versioning and tested restoring a previous file version
- [x] Explored different storage classes while uploading objects

---

## ❓ Doubts / Things to Explore Further
- How Lifecycle rules interact with Versioning (transitioning old versions)
- Setting up CloudFront in front of an S3 static website for HTTPS + custom domain
- Writing more complex, fine-grained bucket policies (conditions, IP restrictions)

---

## 📚 Resources Used
- AWS Official Documentation (S3 User Guide)
- YouTube tutorials on S3 fundamentals and static website hosting

---

## ➡️ Next Steps
- [ ] Learn **EC2** (compute service) next week
- [ ] Connect S3 static website with **CloudFront** for HTTPS access
