### What is it?
This is a simple example of how we can send code coverage from GitLab CI/CD to messenger like Slack via webhook. Also how to generate detailed code coverage report in GitLab pages.

### How it works:
- At the test stage we are running go test and save output to coverage.out file. P.S go tool cover on this stage need for GitLab ci coverage report.
- Saved coverage.out file to artifacts for next job.
- At the pages stage, we are running go tool cover for getting total coverage, then we will find Total string. Next, we will parse them with awk and getting only coverage number. Then with the xargs and curl we sending coverage percent to slack via webhook.
- Next, we create .HTML file from coverage.out with go tool cover, who generated pretty formatted HTML with coverage. After this, we create a public folder and move index.html inside. because GitLab always deploys your website from a very specific folder called public in your repository. When you create a new project in GitLab, a repository becomes available automatically.
- If pages stage successfully done, you will see a new job in the CI pipeline like pages:deploy, created by GitLab.
- Go to your repository GitLab pages (https://your-url.gitlab.io/your-repo/) where you will see your detailed coverage report

#### Useful links:

- https://about.gitlab.com/blog/2016/11/03/publish-code-coverage-report-with-gitlab-pages/
- https://docs.gitlab.com/ee/user/project/pages/index.html
- https://docs.gitlab.com/ee/ci/yaml/README.html#artifacts
 
