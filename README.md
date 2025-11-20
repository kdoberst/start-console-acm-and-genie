# start-console-acm-and-genie

This repo contains the steps to run the console with ACM/MCE and Genie (POC) locally.


## Prerequisites

### Repos
 - Lightspeed repo - https://github.com/openshift/lightspeed-service
 - Genie POC repo - https://github.com/jhadvig/genie-plugin
 - ACM console repo - https://github.com/stolostron/console

### Requirements
 - Docker running
 - Podman with the default machine running
 - Either a LLM running with Ollama OR credits for OpenAI api
 - Access to an OCP Hub cluster 

## Summary
 - Start up Lightspeed locally
 - Start up the parts of the Genie POC locally:
    - OBS-MCP
    - Layout manager
    - NextGen UI
    - Dynamic plugin (only - do not start console)

 - Start up ACM with this command: `npx concurrently npm:start:backend npm:serve:plugins npm:watch:multicluster-sdk -n backend,frontend,watch -c green,blue,bgCyan` (do not use the documented commands)
 
 - Start up OCP console using script in this repo.
    - This can be done in any directory
    - You may need to give execute permission (`chmod +x start-ocp-console.sh` )

 - Go to the following in a browser:
   - Ensure all three plugins are listed (acm, mce, genie): http://localhost:9000/k8s/cluster/operator.openshift.io~v1~Console/cluster/console-plugins
  - Ensure ACM is working: http://localhost:9000/multicloud/infrastructure/clusters/managed
  - Ensure Genie is working: http://localhost:9000/genie/widgets


 ----


 

The `start-ocp-console.sh   ` script was copied from the ACM repo and the following modifications were made:
 - Pulled in env variables from other files at the top of the file
 - Added `genie-plugin` to the list in BRIDGE_PLUGINS
 - Added the genie endpoints to the list in BRIDGE_PLUGIN_PROXY

