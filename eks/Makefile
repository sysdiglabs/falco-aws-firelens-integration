deploy: deploy-fluent-bit deploy-falco

deploy-fluent-bit:
	-aws iam create-policy --policy-name EKS-CloudWatchLogs --policy-document file://./fluent-bit/aws/iam_role_policy.json
	aws iam attach-role-policy --role-name sysdig-nestor-eks-node --policy-arn `aws iam list-policies | jq -r '.[][] | select(.PolicyName == "EKS-CloudWatchLogs") | .Arn'`
	kubectl apply -f fluent-bit/kubernetes/

deploy-falco:
	helm install --name=falco --set falco.jsonOutput=true --set image.tag=0.17.0 stable/falco

clean: clean-fluent-bit clean-falco

clean-fluent-bit:
	kubectl delete -f fluent-bit/kubernetes/

clean-falco:
	helm del --purge falco
