git config --global user.email 'kepa23cs@cmrit.ac.in'
git config --global user.name 'Keerti-04'
ssh-keygen -t ed25519 -C "kepa23cs@cmrit.ac.in"
cat ~/.ssh/id_ed25519.pub
git init
git add pom.xml
git add src
git commit -m "first"
git remote add origin git@github.com:Keerti-04/devops
git remote set-url origin git@github.com:Keerti-04/devops.git
git config --global push.autoSetupRemote true
git push origin master
sudo cat /var/lib/jenkins/secrets/initialAdminPassword

PIPELINE SCRIPT
pipeline{
    agent any
    stages{
        stage('Checkout')
        {
            steps{
                git branch: 'master' , url: 'https://github.com/Keerti-04/program8.git'
            }
        }
        stage('Build')
        {
            steps{
                sh 'mvn clean package'
            }
        }
        stage('Test')
        {
            steps{
                sh 'mvn test'
            }
        }
        stage('Archive Artifact')
        {
            steps{
                archiveArtifacts artifacts: '**/target/*.jar',
                allowEmptyArchive: true
            }
        }
        stage('Deploy')
        {
            steps{
                sh """
                export ANSIBLE_HOST_KEY_CHECKING=False
                ansible-playbook -i host.ini p8.yml
                """
            }
        }
    }
}
