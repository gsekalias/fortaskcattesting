# fortaskcattesting
The AWS CloudFormation templates you want to test as part of the CI/CD pipeline

A. Have a gitHub repo to maintain the CloudFormation templates to be tested with two branches (e.g. master & develop).  The following items are needed for the next step:
	a. Reponame
	b. gitHubUser
  c. OAuth token
	d. releaseBranch
	e. SourceRepoBranch.

    Note: Reference https://github.com/aws-quickstart/taskcat#migrating-from-08x for suggested configuration files for taskcat version > v0.8.x

B. Build out S3 bucket:  (manual buildout at the moment)
	       Example Bucket: "taskcat-assets"

   Place "lambda.zip" in folder structure "assets > functions > package"

	 Place the following 5 Cloudformation templates in folder structure "assets > templates".
    1. taskcat-ci-pipeline.template.yaml
    2. copy-lambdas.template.yaml
    3. ssm.template.yaml
    4. iam-roles.template.yaml
    5. pipeline.template.yaml

C.  Create pipeline stacks:  (5 minutes to build-out all of the AWS resources needed)
	  1. Create Stack using the Amazon S3 URL for "taskcat-ci-pipeline.template.yaml" using the items from the previous steps.  This will launch the other 4 templates.

        Note: The pipeline will have an initial run at creation triggered by the initial repo connection.  This will not result in any reports.

    2. Make any changes to the target CF template that will be tested and to the .taskcat.yml file and push to the SourceRepoBranch.  This will trigger the pipeline.

    3. Passing results will be placed in the created artifact bucket under "taskcat_report".

    4. We still do not understand what occurs when the pipeline fails.

     










# Taskcat Releases
https://github.com/aws-quickstart/taskcat/releases
