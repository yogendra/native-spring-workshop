.PHONY=demo

demo: compile run push

compile: separator-compile 
	- docker build -t yogendra/helloworld-java-native:latest . 

run: separator-run-image
	- docker run --rm yogendra/helloworld-java-native:latest

push: separator-push
	- docker push yogendra/helloworld-java-native:latest

.PHONY: separator

separator-%:
	@echo ================================================================================
	@echo 
	@echo ================================================================================
	@echo $*
	@echo ================================================================================
