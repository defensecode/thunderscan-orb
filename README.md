# DefenseCode ThunderScan CircleCI Orb ![ThunderScan](https://raw.githubusercontent.com/defensecode/thunderscan-action/master/images/thunderscan-icon.png)

<p align="center">
  <img src="https://raw.githubusercontent.com/defensecode/thunderscan-action/master/images/defensecode.png">
</p>

**DefenseCode ThunderScan®** CircleCI orb is available in the [CircleCI public registry](https://circleci.com/developer/orbs/orb/defensecode/thunderscan)  of Orbs as a certified partner. As a reusable package of YAML configuration that condenses repeated pieces of ThunderScan config into a single line of code, the orb provides an easy way for Developers and AppSec teams to rapidly find and triage security risks and have **continuous visibility** with every build. With orbs, it is possible to write a parameterized configuration once and utilize it across multiple similar projects.

**DefenseCode ThunderScan®** is a SAST (Static Application Security Testing, WhiteBox Testing) solution for performing deep and extensive security analysis of application source code. ThunderScan® is easy to use and can be deployed during or after development with easy integration into DevOps environment and CI/CD pipeline.

Find more info on the official website: [DefenseCode.com](https://www.defensecode.com)

## Usage Examples

The example below shows how to import the ThunderScan<sup>®</sup> orb into your config file.

```yaml
version: 2.1

orbs:
  thunderscan: defensecode/thunderscan@1.0
```

To define a simple scan job that will **break the build** if a scan results in more than one high risk vulnerability, export HTML and JSON reports from a ThunderScan scan and store them as artifacts, we can use the following example:

```yaml
workflows:
  build:
    jobs:
      - thunderscan/scan:
          threshold: "high:1"
          report: true
          report-filename: thunderscan-report
          report-format: html,json
          scan-name: "$CIRCLE_PROJECT_REPONAME/$CIRCLE_BUILD_NUM"
          post-run:
            - store_artifacts:
                path: ./thunderscan-report.json
            - store_artifacts:
                path: ./thunderscan-report.html
```
The environment variables containing the URL of the ThunderScan<sup>®</sup> API instance (`THUNDERSCAN_API_URL`) and API token (`THUNDERSCAN_API_TOKEN`) should be set in the **context** or **project variables**.

Scan job of the ThunderScan<sup>®</sup> orb performs a checkout of the repository to make it available to the job, downloads the command line client which is then invoked to: zip, upload and initiate a scan with provided parameters (full list of parameters is available in the [orb listing](https://circleci.com/developer/orbs/orb/defensecode/thunderscan)).

![circleci-example-screenshot](https://user-images.githubusercontent.com/29266274/124599242-bd10f380-de65-11eb-9ef6-1264ee5c4f79.png)
