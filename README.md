
# Upload artifacts to jfrog

This action is intended to be used for uploading artifacts from given local directory (within self-hosted runner) to JFrog.
It checks given directory, searches for directories without prefix "Uploaded-", archives them, uploads to given JFrog repository and adds prefix "Uploaded-" to directories that has been uploaded.
The workflow using this action could be triggered on some scheduled time.

## Inputs

### jfrog-repo-url:
Url of JFrog repository to upload to. **Required**
### jfrog-username:
  JFrog username to use for uploading artifact. Should have WRITE permissions. **Required**
### jfrog-password:
  JFrog user password.
### local-storage-path:
  Path of local (usually self-hosted) runner's directory where artifacts are stored. **Required**
###days-limit-for-uploaded-artifacts:
    Limit of days to keep files in the given local storage path. Older uploaded repositories will be deleted. Default is 30 days.


## Example

```
    name: Upload artifacts to JFrog
    
    on:
      workflow_dispatch:
      schedule:
        - cron: "0 3 * * *"
    
    jobs:
      upload artifacts:
        runs-on: [ec2, windows, medium]
        name: Upload artifacts to JFrog for some application
        steps:
          - uses: telia-actions/upload-artifacts-to-jfrog@v1
            with:
              jfrog-repo-url: ${{ vars.JFROG_REPO_URL }}
              jfrog-username: ${{ vars.JFROG_USERNAME }}
              jfrog-password: ${{ secrets.JFROG_PASSWORD }}
              local-storage-path: 'D:/local-artifacts/some-application'

```
