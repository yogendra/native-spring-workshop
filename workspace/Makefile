IMAGE:=yogendra/graalvm-workspace:latest


.PHONY=all


all: build push

build:
	@docker build -t  ${IMAGE} . 

push: 
	@docker push ${IMAGE}
