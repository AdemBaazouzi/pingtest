---
title: Orchestrate a PingIntelligence Deployment
---
# Orchestrate a PingIntelligence Deployment

Use kustomize for the PingIntelligence deployment from your local `pingidentity-devops-getting-started/20-kustomize/02-fullstack/pingintelligence` directory (the location of the YAML files) and call into your local `pingidentity-devops-getting-started/20-kustomize/01-standalone` directory for the base product configurations.

`kustomization.yaml` does the following:

* References your local `pingidentity-devops-getting-started/20-kustomize/01-standalone/pingintelligence` directory for the base product configurations
* Uses environment variable `onprem` for ABS deployment
* Set `PING_INTELLIGENCE_ASE_ENABLE_ABS: "false"` 

## Connect ASE to ABS

ABS onprem
* `PING_INTELLIGENCE_ASE_ENABLE_ABS: "true"`
* Provide a valid ABS access key with `PING_INTELLIGENCE_ABS_ACCESS_KEY`
* Provide a valid ABS secret key with `PING_INTELLIGENCE_ABS_SECRET_KEY` 

ABS Cloud
* `PING_INTELLIGENCE_ABS_DEPLOYMENT_TYPE: "cloud"`
* Provide a valid gateway jwt with `PING_INTELLIGENCE_GATEWAY_CREDENTIALS` which is generated by PingOne

For more information about the ASE to ABS connectivity please visit [PingIntelligence](https://docs.pingidentity.com/bundle/pingintelligence-51/page/lca1564008967281.html)