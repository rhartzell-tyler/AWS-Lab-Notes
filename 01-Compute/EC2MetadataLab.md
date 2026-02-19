# 🧪 EC2 Lab Notes: Accessing Instance Metadata Service v2 (IMDSv2)

This guide walks through retrieving metadata from an EC2 instance using the Instance Metadata Service v2 (IMDSv2). IMDSv2 adds an extra layer of protection by requiring a session token.

---

## 🛠️ Step 1: Fetch a Metadata Session Token

Run the following command from within the EC2 instance:

```bash
TOKEN=$(curl -X PUT "http://169.254.169.254/latest/api/token" \
  -H "X-aws-ec2-metadata-token-ttl-seconds: 21600")
```

## 📥 Step 2: Use the Token to Get Metadata

Example: To list the top-level metadata keys:

```bash
curl -H "X-aws-ec2-metadata-token: $TOKEN" \
  http://169.254.169.254/latest/meta-data/
```
Example: To retrieve the instance ID:
```bash
for path in $(curl -s -H "X-aws-ec2-metadata-token: $TOKEN" \
  http://169.254.169.254/latest/meta-data/); do
  echo "🔹 $path"
  curl -s -H "X-aws-ec2-metadata-token: $TOKEN" \
    http://169.254.169.254/latest/meta-data/$path
  echo -e "\n"
done
```

## 🧪 Optional: Recursively List Metadata Values

This script loops through top-level keys:

```bash
for path in $(curl -s -H "X-aws-ec2-metadata-token: $TOKEN" \
  http://169.254.169.254/latest/meta-data/); do
  echo "🔹 $path"
  curl -s -H "X-aws-ec2-metadata-token: $TOKEN" \
    http://169.254.169.254/latest/meta-data/$path
  echo -e "\n"
done
```

## 🧠 Notes
- Metadata IP is always: 169.254.169.254
- Token is required for all requests in IMDSv2.
- Output is plain text — easy to parse with tools like jq, grep, or shell logic.

## ✅ Bonus Tip: Export Token for Reuse
```bash
export EC2_TOKEN=$(curl -X PUT "http://169.254.169.254/latest/api/token" \
  -H "X-aws-ec2-metadata-token-ttl-seconds: 21600")
```

## 🔚 Summary
You can now:

- Securely authenticate to IMDSv2
- Retrieve EC2 metadata like instance ID, AMI ID, public key, and more
- Script or automate metadata queries for bootstrapping and configuration