pipeline
{
	agent any
	stages
	{
		stage('Checkout')
		{
			steps
			{
				git 'https://github.com/iamdevopstrainer/html-application'
			}
		}
				
		stage('Build Docker Image')
		{
			steps
			{
				sh 'sudo mkdir -p /code/htmljob/$BUILD_NUMBER'
				sh 'sudo cp /var/lib/jenkins/workspace/htmljob/application.html /code/htmljob/$BUILD_NUMBER/'
				sh 'sudo cp /var/lib/jenkins/workspace/htmljob/Dockerfile /code/htmljob/$BUILD_NUMBER'
				sh 'sudo docker build -f /code/htmljob/$BUILD_NUMBER/Dockerfile -t iamdevopstrainer/httpd-20210930:$BUILD_NUMBER /code/htmljob/$BUILD_NUMBER'
			}
		}

		stage('Push Docker Image')
		{
			steps
			{
				sh "sudo docker push iamdevopstrainer/httpd-20210930:$BUILD_NUMBER"
			}
		}

		stage('Update Application')
		{
			steps
			{
				sh "sudo kubectl set image deployment.apps/httpd-dep httpd-cont=iamdevopstrainer/httpd-20210930:$BUILD_NUMBER --record=true"
			}
		}
		
	}
		
}
