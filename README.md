# Important: Unauthorized access to our vantage6 image registry

## Update: April 3rd, 2026 - 12:00
 
In addition to the findings yesterday, we wish to highlight the following images:

- infrastructure/vpn-client:4.14
- infrastructure/vpn-configurator:4.14
- infrastructure/ssh-tunnel:4.14
- infrastructure/squid:4.14

These images have been compromised on March 24, 2026. Importantly, these images are run by vantage6 nodes if VPN / SSH tunnel / whitelisting features are configured by the node. Unlike the algorithm images, these images have internet access and therefore we expect that malware would be downloaded if these images have been run on a vantage6 node.
 
To scan your system, you may use this script, kindly provided by Johan van Soest and colleagues: [test_docker_image.sh](https://gist.github.com/jvsoest/d5d7f600ff1ba0d03556a29392c788b9). It lists all docker images on your system and searches if the malicious pattern is found in them.
 
For reference, the malware found is described here: [VirusTotal - File - 912186b9420585ebf21e52f37390f3cee88adda85d2a815b44ab01bb40dd580f](https://www.virustotal.com/gui/file/912186b9420585ebf21e52f37390f3cee88adda85d2a815b44ab01bb40dd580f/detection). Note that it is tagged by several vendors as a coin miner, but we do not know if that annotation is correct, and it is probably not possible to determine this with certainty.

## 2 April 2026 - 10:15
Dear community members,

We are hereby reporting unauthorized access to the community Harbor image registry. A malicious user has gained admin access to the application and injected a malicious binary into some of the images. This malicious binary is a malware downloader. In other words, once this application is started it will download a malicious application.

The attacker seems not to have targeted the vantage6 registry specifically, but rather was attacking diverse harbor registries. This makes it less likely the attacker is after sensitive data. Also, fortunately, NO node images have been affected with the exception of the unreleased version 5 images. This means that production nodes should have functioned as normal.

The most important images that are affected are:

- infrastructure/server:cotopaxi - affected since 24/3, containing version 4.14
- version 5 infrastructure images tagged with Uluru

A complete of overview of all affected images can be found below this message. Also, the malicious cotopaxi server image does not start (see issue [[BUG] Server 4.14.0 (cotopaxi): /wrapper.sh permission denied on container start · Issue #2578 · vantage6/vantage6](https://github.com/vantage6/vantage6/issues/2578)).

We expect that there is only an impact for those of you who have run the version 5 beta images. However, we encourage you to investigate if any of the affected images might have run in your projects. Note that also many algorithm images have been affected, but since algorithms in vantage6 lack an internet connection, we do not expect that the malware download succeeded. However, note that the image with the downloader may still be present.

After discovering the presence of malicious images, we shutdown the harbor2 service yesterday evening. We will get back to you when the service will be resumed.

Apart from investigating the impact to your project, we would advise you to purge any affected vantage6 images.

We will keep you informed of any new updates.

| Image + tag                                                                                     | Affected at |
| ----------------------------------------------------------------------------------------------- | ----------- |
| infrastructure/node:5.0                                                                         | 3/31/26     |
| infrastructure/node:uluru                                                                       | 3/31/26     |
| infrastructure/ui:uluru                                                                         | 3/31/26     |
| infrastructure/algorithm-store:uluru                                                            | 3/31/26     |
| infrastructure/hq:uluru                                                                         | 3/31/26     |
| infrastructure/hq:uluru-live                                                                    | 3/31/26     |
| infrastructure/node:5.0                                                                         | 3/24/26     |
| infrastructure/node:uluru                                                                       | 3/24/26     |
| infrastructure/server:cotopaxi                                                                  | 3/24/26     |
| infrastructure/server:cotopaxi-live                                                             | 3/24/26     |
| infrastructure/vpn-client:4.14                                                                  | 3/24/26     |
| infrastructure/vpn-configurator:4.14                                                            | 3/24/26     |
| infrastructure/ui:uluru                                                                         | 3/24/26     |
| infrastructure/ssh-tunnel:4.14                                                                  | 3/24/26     |
| infrastructure/squid:4.14                                                                       | 3/24/26     |
| infrastructure/algorithm-store:uluru                                                            | 3/24/26     |
| infrastructure/hq:uluru                                                                         | 3/24/26     |
| infrastructure/hq:uluru-live                                                                    | 3/24/26     |
| infrastructure/arm-node:latest                                                                  | 3/11/26     |
| infrastructure/arm-node@sha256:a015130db8f4bec722d0a87cd7be4b7f4c6fbb7b940ed982c23c42752f149612 | 3/11/26     |
| infrastructure/arm-node@sha256:ccde7f94e516b4119bba5b6a12f5fea17d112095b7574ed5a09a475ff0814dab | 3/11/26     |
| infrastructure/node:5.0                                                                         | 3/9/26      |
| infrastructure/node:uluru                                                                       | 3/9/26      |
| infrastructure/alpine:5.0                                                                       | 3/9/26      |
| infrastructure/ui:uluru                                                                         | 3/9/26      |
| infrastructure/algorithm-store:uluru                                                            | 3/9/26      |
| infrastructure/hq:uluru                                                                         | 3/9/26      |
| infrastructure/hq:uluru-live                                                                    | 3/9/26      |
| infrastructure/node:kKesjjS                                                                     | 3/1/26      |
| infrastructure/node:BLShJZN                                                                     | 3/1/26      |
| infrastructure/ui:iwsMGAT                                                                       | 3/1/26      |
| infrastructure/ui:MlTztYM                                                                       | 3/1/26      |
| infrastructure/ui:LCNfyio                                                                       | 3/1/26      |
| infrastructure/ui:WqFBXyL                                                                       | 3/1/26      |
| infrastructure/algorithm-store:YPClroD                                                          | 3/1/26      |
| infrastructure/algorithm-store:Ibusuay                                                          | 3/1/26      |
| infrastructure/hq:NGFPPJH                                                                       | 3/1/26      |
| infrastructure/hq:LctVwEJ                                                                       | 3/1/26      |
| web/vantage6.ai:latest                                                                          | 2/16/26     |
| test-private/average:latest                                                                     | 2/16/26     |
| starter/basics:a432c4f                                                                          | 2/16/26     |
| starter/basics:latest                                                                           | 2/16/26     |
| starter/glm:latest                                                                              | 2/16/26     |
| starter/utils:keep20230911                                                                      | 2/16/26     |
| starter/utils:with-node-status-check                                                            | 2/16/26     |
| starter/utils:latest                                                                            | 2/16/26     |
| starter/crosstab:latest                                                                         | 2/16/26     |
| starter/coxph:latest                                                                            | 2/16/26     |
| starter/coxzph:latest                                                                           | 2/16/26     |
| starter/survfit:latest                                                                          | 2/16/26     |
| starter/survdiff:latest                                                                         | 2/16/26     |
| starter/dummy:dev                                                                               | 2/16/26     |
| starter/vtg.chisq:0.0.11                                                                        | 2/16/26     |
| starter/vtg.chisq:0.0.12                                                                        | 2/16/26     |
| starter/vtg.chisq:0.0.13                                                                        | 2/16/26     |
| starter/vtg.chisq:0.0.14                                                                        | 2/16/26     |
| starter/vtg.chisq:0.0.15                                                                        | 2/16/26     |
| starter/vtg.chisq:latest                                                                        | 2/16/26     |
| starter/vtg.survfit:0.0.5                                                                       | 2/16/26     |
| starter/vtg.survfit:dev                                                                         | 2/16/26     |
| starter/vtg.survfit:0.0.6                                                                       | 2/16/26     |
| starter/vtg.survfit:latest                                                                      | 2/16/26     |
| starter/vtg.summary:0.0.15                                                                      | 2/16/26     |
| starter/vtg.summary:dev                                                                         | 2/16/26     |
| starter/vtg.summary:0.0.16                                                                      | 2/16/26     |
| starter/vtg.summary:latest                                                                      | 2/16/26     |
| starter/vtg.coxph:dev                                                                           | 2/16/26     |
| starter/vtg.coxph:0.1.1                                                                         | 2/16/26     |
| starter/vtg.coxph:latest                                                                        | 2/16/26     |
| starter/vtg.crosstab:dev                                                                        | 2/16/26     |
| starter/vtg.crosstab:0.0.7                                                                      | 2/16/26     |
| starter/vtg.crosstab:0.0.8                                                                      | 2/16/26     |
| starter/vtg.crosstab:latest                                                                     | 2/16/26     |
| starter/vtg.glm:0.0.1                                                                           | 2/16/26     |
| starter/vtg.glm:latest                                                                          | 2/16/26     |
| starter/vtg.debugger:dev                                                                        | 2/16/26     |
| starter/vtg.survdiff:dev                                                                        | 2/16/26     |
| starter/vtg.survdiff:0.0.1                                                                      | 2/16/26     |
| starter/vtg.survdiff:0.0.2                                                                      | 2/16/26     |
| starter/vtg.survdiff:latest                                                                     | 2/16/26     |
| plugin/n2n-diagnostics-aioc:latest                                                              | 2/16/26     |
| plugin/flower-aioc:latest                                                                       | 2/16/26     |
| plugin/playground-aioc:latest                                                                   | 2/16/26     |
| plugin/aioc:nlp                                                                                 | 2/16/26     |
| plugin/pluginml:nlp                                                                             | 2/16/26     |
| plugin/pluginml:old-harm                                                                        | 2/16/26     |
| plugin/pluginfhir:test                                                                          | 2/16/26     |
| melle/aioc:petronas                                                                             | 2/16/26     |
| infrastructure/hello-world:latest                                                               | 2/16/26     |
| infrastructure/hello-vantage6:latest                                                            | 2/16/26     |
| infrastructure/old-base:latest                                                                  | 2/16/26     |
| infrastructure/ohdsi-api:0.0.5                                                                  | 2/16/26     |
| infrastructure/ohdsi-api:0.0.5                                                                  | 2/16/26     |
| infrastructure/ohdsi-api:0.0.5                                                                  | 2/16/26     |
| infrastructure/ohdsi-api:0.0.7                                                                  | 2/16/26     |
| infrastructure/ohdsi-api:latest                                                                 | 2/16/26     |
| infrastructure/ohdsi-api:0.0.8                                                                  | 2/16/26     |
| infrastructure/k8snode:latest                                                                   | 2/16/26     |
| idea4rc/kaplan-meier:cotopaxi-v6-4.7.1                                                          | 2/16/26     |
| idea4rc/kaplan-meier:latest                                                                     | 2/16/26     |
| demo/average:4.6.0                                                                              | 2/16/26     |
| demo/average:latest                                                                             | 2/16/26     |
| demo/omop-tester:latest                                                                         | 2/16/26     |
| demo/crosstab-ohdsi:v4                                                                          | 2/16/26     |
| demo/crosstab-ohdsi:cotopaxi-v0.0.2                                                             | 2/16/26     |
| blueberry/kaplan-meier:cotopaxi-v6-4.5.5                                                        | 2/16/26     |
| blueberry/kaplan-meier:cotopaxi-v6-4.0.0                                                        | 2/16/26     |
| blueberry/kaplan-meier:latest                                                                   | 2/16/26     |
| blueberry/basic-omop-queries:cotopaxi-v6-4.5.5                                                  | 2/16/26     |
| blueberry/basic-omop-queries:latest                                                             | 2/16/26     |
| blueberry/omop-cohorts:cotopaxi-v6-4.0.0                                                        | 2/16/26     |
| blueberry/omop-cohorts:latest                                                                   | 2/16/26     |
| blueberry/omop-cohort-diagnostics:cotopaxi-v6-4.0.0                                             | 2/16/26     |
| blueberry/omop-cohort-diagnostics:latest                                                        | 2/16/26     |
| blueberry/ohdsi-update-csv:latest                                                               | 2/16/26     |
| blueberry/create-cohorts:cotopaxi-v6-4.7.1                                                      | 2/16/26     |
| blueberry/create-cohorts:latest                                                                 | 2/16/26     |
| blueberry/summary:cotopaxi-v6-4.7.1                                                             | 2/16/26     |
| blueberry/summary:latest                                                                        | 2/16/26     |
| blueberry/sessions:cotopaxi-v6-4.7.1                                                            | 2/16/26     |
| blueberry/sessions:latest                                                                       | 2/16/26     |
| blueberry/analytics:cotopaxi-v6-4.9.1                                                           | 2/16/26     |
| blueberry/analytics:latest                                                                      | 2/16/26     |
| algorithms/glm:0.0.4-v6-4.9.0                                                                   | 2/16/26     |
| algorithms/glm:1.0.0-v6-4.10.2                                                                  | 2/16/26     |
| algorithms/glm:dev                                                                              | 2/16/26     |
| algorithms/glm:1.0.1-v6-4.11.0                                                                  | 2/16/26     |
| algorithms/glm:1.1.0-v6-4.12.0                                                                  | 2/16/26     |
| algorithms/glm:latest                                                                           | 2/16/26     |
| algorithms/summary:1.0.0-v6-4.9.0                                                               | 2/16/26     |
| algorithms/summary:dev                                                                          | 2/16/26     |
| algorithms/summary:1.1.0-v6-4.9.1                                                               | 2/16/26     |
| algorithms/summary:1.1.0                                                                        | 2/16/26     |
| algorithms/summary:latest                                                                       | 2/16/26     |
| algorithms/basics:ca71692                                                                       | 2/16/26     |
| algorithms/basics:78c0dc9                                                                       | 2/16/26     |
| algorithms/basics:780d387                                                                       | 2/16/26     |
| algorithms/basics:542d5f9                                                                       | 2/16/26     |
| algorithms/basics:latest                                                                        | 2/16/26     |
| algorithms/kaplan-meier:latest                                                                  | 2/16/26     |
| algorithms/kaplan-meier:cotopaxi-v6-4.5.0                                                       | 2/16/26     |
| algorithms/utils:latest                                                                         | 2/16/26     |
| algorithms/n2n-diagnostics:v6-v3.7.0                                                            | 2/16/26     |
| algorithms/n2n-diagnostics:latest                                                               | 2/16/26     |
| algorithms/n2n-diagnostics:v6-v3.9.0                                                            | 2/16/26     |
| algorithms/ror_algo:8                                                                           | 2/16/26     |
| algorithms/ror_algo:9                                                                           | 2/16/26     |
| algorithms/glmm:latest                                                                          | 2/16/26     |
| algorithms/coxzph:latest                                                                        | 2/16/26     |
| algorithms/coxph:latest                                                                         | 2/16/26     |
| algorithms/crosstab:1.1.0                                                                       | 2/16/26     |
| algorithms/crosstab:1.1.1-v6-                                                                   | 2/16/26     |
| algorithms/crosstab:1.1.2-v6-4.6.0                                                              | 2/16/26     |
| algorithms/crosstab:latest                                                                      | 2/16/26     |
| algorithms/csv-extractor:test                                                                   | 2/16/26     |
| algorithms/csv-extractor:dev                                                                    | 2/16/26     |
| algorithms/session-basics:bart                                                                  | 2/16/26     |
| algorithms/session-basics:0.2.24-v6-                                                            | 2/16/26     |
| algorithms/session-basics:latest                                                                | 2/16/26     |
| algorithms/session-basics:bart-dev                                                              | 2/16/26     |

Kind regards,
The vantage6 team
