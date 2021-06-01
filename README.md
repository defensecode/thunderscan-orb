# DefenseCode ThunderScan CircleCI Orb ![ThunderScan](https://raw.githubusercontent.com/defensecode/thunderscan-action/master/images/thunderscan-icon.png)


<p align="center">
  <img src="https://raw.githubusercontent.com/defensecode/thunderscan-action/master/images/defensecode.png">
</p>


A [CircleCI Orb](https://circleci.com/orbs/) for adding DefenseCode ThunderScan SAST analysis into your CI/CD pipeline to identify security risks in your applications. To use this orb you simply need a running instance of the ThunderScan API.

**DefenseCode ThunderScan®** is a SAST (Static Application Security Testing, WhiteBox Testing) solution for performing deep and extensive security analysis of application source code. ThunderScan® is easy to use and can be deployed during or after development with easy integration into DevOps environment and CI/CD pipeline.

Find more info in the official website: [DefenseCode.com](https://www.defensecode.com)

## Usage Examples
### Scan Application

```yaml
version: 2.1

orbs:
  thunderscan: defensecode/thunderscan@1.0.0

workflows:
  scan-workflow:
    jobs:
      - thunderscan/scan:
          scan-name: "$CIRCLE_PROJECT_REPONAME/$CIRCLE_BUILD_NUM"
          report: true
          report-filename: thunderscan-test-report
          report-format: html,json
```

