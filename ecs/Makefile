CLUSTER_ARN="arn:aws:ecs:eu-west-1:845151661675:cluster/nestor-sysdig-ecs-demo"
NODE_ROLE_NAME="ecsInstanceRole"

deploy: deploy-fluent-bit deploy-falco

deploy-fluent-bit:
	-aws iam create-policy --policy-name ECS-CloudWatchLogs --policy-document file://./fluent-bit/iam_role_policy.json
	aws iam attach-role-policy --role-name $(NODE_ROLE_NAME) --policy-arn `aws iam list-policies | jq -r '.[][] | select(.PolicyName == "ECS-CloudWatchLogs") | .Arn'`

deploy-falco:
	aws ecs register-task-definition --cli-input-json file://./falco/task-definition.json
	aws ecs create-service --cluster $(CLUSTER_ARN) --service-name falco --task-definition `aws ecs list-task-definitions | jq -r '.taskDefinitionArns[] | select(. | contains("Falco"))'` --scheduling-strategy DAEMON

clean: clean-fluent-bit clean-falco

clean-fluent-bit:
	aws iam detach-role-policy --role-name $(NODE_ROLE_NAME) --policy-arn `aws iam list-policies | jq -r '.[][] | select(.PolicyName == "ECS-CloudWatchLogs") | .Arn'`
	aws iam delete-policy --policy-arn `aws iam list-policies | jq -r '.[][] | select(.PolicyName == "ECS-CloudWatchLogs") | .Arn'`

clean-falco:
	-aws ecs delete-service --cluster $(CLUSTER_ARN) --service falco
	aws ecs deregister-task-definition --task-definition `aws ecs list-task-definitions | jq -r '.taskDefinitionArns[] | select(. | contains("Falco"))'`
