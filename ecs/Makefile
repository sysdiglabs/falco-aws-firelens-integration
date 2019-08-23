IMAGE=falcosecurity/fluentbit-ecs-falco

deploy: deploy-fluent-bit deploy-falco

deploy-fluent-bit:
	echo "Not implemented"

deploy-falco:
	echo "Not implemented"

clean: clean-fluent-bit clean-falco

clean-fluent-bit:
	echo "Not implemented"

clean-falco:
	echo "Not implemented"

build:
	docker build -t ${IMAGE} fluent-bit-image-for-ecs

push: build
	docker push ${IMAGE}
