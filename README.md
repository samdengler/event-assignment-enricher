# Event Assigment Enricher

## Architecture Diagram

![Architecture Diagram](/assets/images/architecture-diagram.png "Architecture diagram")

## Installation

1. Clone repository

### Consumer
1. `aws cloudformation create-stack --stack-name consumer --template-body file://consumer.yaml --parameters ParameterKey=PermittedOrganizationId,ParameterValue=$ORGANIZATION_ID`
1. Provide values for: Organization ID

### Producer
1. `aws cloudformation create-stack --stack-name producer --template-body file://producer.yaml --capabilities CAPABILITY_IAM --parameters ParameterKey=CentralEventBusArn,ParameterValue=$CENTRAL_EVENT_BUS_ARN ParameterKey=EventSourceCustomPrefix,ParameterValue=$CUSTOM_PREFIX`
1. Provide values for: CentralEventBusArn (from Consumer stack), EventSourceCustomPrefix

## Considerations

* Additional error handling for PutEvents integration in workflow definition
* Add DLQ to EventBridge target for StepFunctions workflow (https://docs.aws.amazon.com/eventbridge/latest/userguide/eb-rule-dlq.html)
* Uncomment "EXPRESS" configuration for the StateMachine definition to reduce Step Functions cost (however there's only 2 transition per successful execution)