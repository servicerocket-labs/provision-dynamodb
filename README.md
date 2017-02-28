# serverless-dynamic-dynamodb

[![Build Status](https://travis-ci.org/ServiceRocket/serverless-dynamic-dynamodb.svg?branch=master)](https://travis-ci.org/ServiceRocket/serverless-dynamic-dynamodb) [![serverless](http://public.serverless.com/badges/v3.svg)](http://www.serverless.com)


> Automatically scale dynamic dynamodb throughput using CLI or automate it further using [serverless framework](http://www.serverless.com).

### Disclaimer

Any reliance you place on serverless-dynamic-dynamodb is strictly at your own risk.

## Getting Started

### CLI Usage

1. Install CLI tool globally via NPM and verify the CLI tool.

        npm install -g serverless-dynamic-dynamodb
        
        provision-dynamodb --help

2. You will need to ensure that you have both `dynamodb:DescribeTable` on the select tables and
   `cloudwatch:GetMetricStatistics`. Refer to [example.json](./example.json) as a guide to automatically scale 
   the select tables.

        DRY_RUN=true provision-dynamodb jsonfile example.json
        
    > Tips: Set DRY_RUN system environment for a dry run without actually applying the changes.
    
    Alternatively, JSON can be specified inline:
    
        DRY_RUN=true provision-dynamodb json '[{"name":"ld-faiz-tenant-info","readStrategy":{"name":"capacity-ratio","upperThresholdRatio":0.8,"lowerThresholdRatio":0.15,"incrementRatio":3,"decrementRatio":0.8,"lowerBoundUnit":1,"upperBoundUnit":28},"writeStrategy":{"name":"capacity-ratio","upperThresholdRatio":0.8,"lowerThresholdRatio":0.15,"incrementRatio":3,"decrementRatio":0.8,"lowerBoundUnit":1,"upperBoundUnit":28}}]'
        
### Serverless Project

1. Clone this project and update serverless settings in [serverless.yml](./serverless.yml) as documented in  [Serverless.yml Reference](https://serverless.com/framework/docs/providers/aws/guide/serverless.yml/). You should consider to fork this and customise it for your own deployment.
   
2. Configure scaling strategy. TODO: Give recommendations.

3. Deploy.

        sls deploy
      
## Scaling Strategy

TODO: Explain about throughput calculations.