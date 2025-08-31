1. Create OIDC provider

REGION_CODE=us-east-1
CLUSTER_NAME=roboshop
ACC_ID=253490767945

eksctl utils associate-iam-oidc-provider \
    --region $REGION_CODE \
    --cluster $CLUSTER_NAME \
    --approve
2. Create policy and attach permissions

arn:aws:iam::315069654700:policy/RoboShopMySQLSecretReader

eksctl create iamserviceaccount \
--cluster=$CLUSTER_NAME \
--namespace=roboshop \
--name=roboshop-mysql-secret-reader \
--attach-policy-arn=arn:aws:iam::253490767945:policy/MYsecretReaderMY \
--override-existing-serviceaccounts \
--region $REGION_CODE \
--approve

this command creates IAM role and SA and integrates them

aws secretsmanager get-secret-value --secret-id roboshop/mysql/password


roboshop/mysql/creds