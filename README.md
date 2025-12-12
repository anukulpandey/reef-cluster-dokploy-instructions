# 🌊 **Reef Cluster – Dokploy Deployment Guide**

A Reef validator cluster can be deployed in **two different ways** on Dokploy:

### 🟢 **[Method 1: Single Template (Full Cluster Setup)](#method-1-single-template---full-cluster-setup)**

A single deployment handles bootnode + all validators + RPC.

### 🔵 **[Method 2: Multiple Templates (Bootstrap + Individual Validators)](#method-2-multiple-templates---bootstrap--validators)**

You deploy bootstrap + validators separately for more control.

---

# 📑 **Table of Contents**

1. [Method 1 – Single Template](#method-1-single-template---full-cluster-setup)

   * [1. Generate Validator Keys](#step-1-generate-validator-keys)
   * [2. Deploy Spec Generator](#step-2-deploy-custom-spec-generator)
   * [3. Deploy Full Cluster](#step-3-deploy-the-complete-cluster)
   * [4. Adding More Validators](#adding-more-validators)
   * [5. Deploy ETH RPC](#deploy-ethereum-rpc)

2. [Method 2 – Multiple Templates](#method-2-multiple-templates---bootstrap--validators)

   * [1. Generate Validator Keys](#step-1-generate-validator-keys-method-2)
   * [2. Deploy Bootnode Validator](#step-2-deploy-bootnode-validator)
   * [3. Deploy Individual Validators](#step-3-deploy-additional-validators)
   * [4. Deploy ETH RPC](#deploy-eth-rpc-method-2)

---

---

# 🟢 **Method 1: Single Template – Full Cluster Setup**

---

## **Step 1: Generate Validator Keys**

1. Go to **Create Service**

   <img width="1348" height="767" src="https://github.com/user-attachments/assets/61ffc1b3-7601-4fa0-a8c9-37dd91fe5f0c">

2. Select **Template** from the menu.

3. Add template repo URL at the top-right:

   ```
   https://d1633d6c.templates-70k.pages.dev/
   ```

4. Search for **“Reef”**

   <img width="1345" height="760" src="https://github.com/user-attachments/assets/0a73fe6e-7e5d-4553-bcd7-0dca6fc2a831">

5. Click **Create** on **Reef Chain – Keys Generator**, then confirm.

   <img width="1352" height="768" src="https://github.com/user-attachments/assets/2a8cae47-6ad4-4d82-aa79-3f7dfb9599ff">

6. Deploy the service.

   <img width="1352" height="760" src="https://github.com/user-attachments/assets/82aa445a-c1b7-46de-aa20-abbecc5b79ba">

7. The logs will show generated validator keypairs.

   <img width="1352" height="803" src="https://github.com/user-attachments/assets/6566a708-3d07-4c90-8dba-26a123dc8514">

8. Copy all **address + seed pairs**, they will be needed later.

   <img width="1352" height="805" src="https://github.com/user-attachments/assets/1efb99f2-aa24-4ff4-8326-da8a79104afd">

---

## **Step 2: Deploy Custom Spec Generator**

1. Go to Templates and search for:

### **Reef Chain – Custom Spec Generator**

<img width="1352" height="808" src="https://github.com/user-attachments/assets/990a8521-7a7e-43ae-aaa1-72b1ac253a13">

2. Deploy it.

3. It runs on port **8000** by default:

   ```
   http://reef.host:8000
   ```

4. You can change the port in environment variables if needed.

This service is used by the validators to automatically fetch the **custom chain spec**.

---

## **Step 3: Deploy the Complete Cluster**

1. From templates, search for:

### **Reef Chain – Dev Cluster**

<img width="1352" height="762" src="https://github.com/user-attachments/assets/33337aa2-a40e-4d91-9b4a-a77881844222">

2. Open the environment tab and paste your seeds & addresses:

<img width="1352" height="767" src="https://github.com/user-attachments/assets/7c05a2e1-ec86-48c2-8015-9909fa44b0fc">

3. You may configure:

   * `specgenurl` → URL of your custom spec generator
   * default: `http://reef.host:8000`

4. Deploy the service.

5. Logs should show successful bootnode + 3 validators starting:

<img width="1352" height="765" src="https://github.com/user-attachments/assets/dabf1beb-900b-4627-a656-78d94cb2771b">

🎉 **The cluster is now running!**

---

## **Adding More Validators**

Generate more validators using **Reef Chain – Keys Generator**.

Then deploy:

### **Reef Chain – Validator**

<img width="1347" height="754" src="https://github.com/user-attachments/assets/68568d1f-8ee2-4abc-a7a0-d9087c09b132">

Fill in the new keys → Deploy.

---

## **Deploy Ethereum RPC**

Search template:

### **Reef Chain – ETH RPC**

<img width="1352" height="765" src="https://github.com/user-attachments/assets/e3644fdf-4465-4fc8-967b-10f9d93513bc">

Deploy → It will use the default substrate RPC:

```
http://reef.host:9944
```

ETH RPC runs at:

```
http://reef.host:8545
```

<img width="977" height="505" src="https://github.com/user-attachments/assets/6d6a5b02-8c8b-4926-a635-a6829c2c2c4d">
<img width="1352" height="755" src="https://github.com/user-attachments/assets/3d66ed43-4e6c-48c5-953a-ca12cfede6db">

🎉 **Your full cluster (bootnode + validators + RPC + ETH RPC) is now live.**

---

---

# 🔵 **Method 2: Multiple Templates – Bootstrap & Validators**

---

## **Step 1: Generate Validator Keys (Same as Method 1)**

👉 Jump to: [Generate Validator Keys](#step-1-generate-validator-keys)

---

## **Step 2: Deploy Bootnode Validator**

Create service → choose template:

### **Reef Chain – Bootnode Validator**

<img width="1349" height="768" src="https://github.com/user-attachments/assets/dd42462e-22c9-44f9-8625-01cad45a77d6">

Fill in:

* `v1sec`, `v2sec`, `v3sec`
* `v1addr`, `v2addr`, `v3addr`
* `PORT=8000` → exposes custom spec
* `P2P_PORT=30335` → bootnode peer port

<img width="1342" height="756" src="https://github.com/user-attachments/assets/eb2a26a8-bc5c-4d54-aade-b47086c9fd89">

Bootnode starts → no peers yet (expected).

---

## **Step 3: Deploy Additional Validators**

Use:

### **Reef Chain – Validator**

<img width="1352" height="766" src="https://github.com/user-attachments/assets/98c57f34-d1f6-48e4-a11b-09a514817e0f">

Deploy 2 or more validators → finalize blocks.

---

## **Deploy ETH RPC (Method 2)**

Same template:

### **Reef Chain – ETH RPC**

<img width="1352" height="765" src="https://github.com/user-attachments/assets/e3644fdf-4465-4fc8-967b-10f9d93513bc">

ETH RPC default port:

```
http://reef.host:8545
```
