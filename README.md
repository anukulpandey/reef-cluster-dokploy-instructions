# Reef Cluster Dokploy Instructions

We can run the cluster in 2 ways.

1. Single template for whole cluster

2. Multiple templates ( Separate bootstrap and validators setup )



The first step is to generate keys for running the validator, you can do it as follows:

Click on create service

<img width="1348" height="767" alt="Screenshot 2025-12-12 at 2 32 48 PM" src="https://github.com/user-attachments/assets/61ffc1b3-7601-4fa0-a8c9-37dd91fe5f0c" />

Select Template from the menu

Add `https://d1633d6c.templates-70k.pages.dev/` url at top right

Search Reef 

<img width="1345" height="760" alt="Screenshot 2025-12-12 at 2 33 41 PM" src="https://github.com/user-attachments/assets/0a73fe6e-7e5d-4553-bcd7-0dca6fc2a831" />

Click on "Create" button on `Reef Chain - Keys Generator` card and click confirm on popup.

<img width="1352" height="768" alt="Screenshot 2025-12-12 at 2 34 43 PM" src="https://github.com/user-attachments/assets/2a8cae47-6ad4-4d82-aa79-3f7dfb9599ff" />

Open the newly generated card service and click on `Deploy` 

<img width="1352" height="760" alt="Screenshot 2025-12-12 at 4 07 57 PM" src="https://github.com/user-attachments/assets/82aa445a-c1b7-46de-aa20-abbecc5b79ba" />

The logs must look like this, it has generated 3 validators keypairs.

<img width="1352" height="803" alt="Screenshot 2025-12-12 at 4 09 03 PM" src="https://github.com/user-attachments/assets/6566a708-3d07-4c90-8dba-26a123dc8514" />

You will get keypairs like these

<img width="1352" height="805" alt="Screenshot 2025-12-12 at 4 10 30 PM" src="https://github.com/user-attachments/assets/1efb99f2-aa24-4ff4-8326-da8a79104afd" />

Copy the address and seed, we will need these later when configuring the validators

Now let's deploy, bootstrap, create a new service, select template and from templates select `Reef Chain - Bootnode Validator` :

<img width="1349" height="768" alt="Screenshot 2025-12-12 at 4 12 00 PM" src="https://github.com/user-attachments/assets/dd42462e-22c9-44f9-8625-01cad45a77d6" />

Paste the validator keys here in environment

<img width="1342" height="756" alt="Screenshot 2025-12-12 at 4 13 54 PM" src="https://github.com/user-attachments/assets/eb2a26a8-bc5c-4d54-aade-b47086c9fd89" />

the `PORT=8000` is for making the spec file publicly available which will allow other validators to fetch it from the bootstrap template.

`P2P_PORT=30335` is responsible for p2p connection between the peers.

In the logs of validator, there wont be peers initially, need to run the validators for that.

<img width="1347" height="754" alt="Screenshot 2025-12-12 at 4 18 57 PM" src="https://github.com/user-attachments/assets/68568d1f-8ee2-4abc-a7a0-d9087c09b132" />

Select `Reef Chain - Validator`

and replace the environments and deploy it.

Do the same for 2 more validators, 3 validators will make the cluster start finalising blocks.

<img width="1352" height="766" alt="Screenshot 2025-12-12 at 4 19 39 PM" src="https://github.com/user-attachments/assets/98c57f34-d1f6-48e4-a11b-09a514817e0f" />

Next step is to run the eth-rpc , we can do that from templates and selecting `Reef Chain - ETH RPC` :

<img width="1352" height="765" alt="Screenshot 2025-12-12 at 4 22 30 PM" src="https://github.com/user-attachments/assets/e3644fdf-4465-4fc8-967b-10f9d93513bc" />

Deploy and it will point to `http://reef.host:9944` by default, you can change that in the environment.

<img width="977" height="505" alt="Screenshot 2025-12-12 at 4 23 39 PM" src="https://github.com/user-attachments/assets/6d6a5b02-8c8b-4926-a635-a6829c2c2c4d" />

<img width="1352" height="755" alt="Screenshot 2025-12-12 at 4 23 51 PM" src="https://github.com/user-attachments/assets/3d66ed43-4e6c-48c5-953a-ca12cfede6db" />

The port in the environment is for eth rpc. i.e it will be run at `http://reef.host:8545`.

Voila! the cluster is running fine.
