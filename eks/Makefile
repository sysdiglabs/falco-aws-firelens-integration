deploy: deploy-fluent-bit deploy-falco

deploy-fluent-bit:
	kubectl apply -f fluent-bit/

deploy-falco:
	helm install --name=falco --set falco.jsonOutput=true stable/falco

clean: clean-fluent-bit clean-falco

clean-fluent-bit:
	kubectl delete -f fluent-bit/

clean-falco:
	helm del --purge falco
