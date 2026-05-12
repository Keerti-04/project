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


yml 

---
- name: deploy maven arti
  hosts: local
  gather_facts: no
  become: true
  become_user: student
  become_method: su
  tasks:
   - name: copy something to something
     copy:
      src: "/var/lib/jenkins/workspace/shibal8/p8.jar"
      dest: "/var/lib/jenkins/workspace/shibal8/targetmy-app-1.0-SNAPSHOT.jar"


7th Program

p1.yml
- name: My first playbook
  hosts: local
  connection: local
  tasks:
   - name: my first task
     debug:
       msg: "hello worldddddd shibaaaaaaaaaaal"


p2.yml
---
- name: playbook with 1 module
  hosts: local
  gather_facts: no
  tasks:
   - name: module command
     hello_world:
       name: "Ansible"
     register: result
   - name: show msg
     debug:
       msg: "{{result.message}}"


hello_world.py

from ansible.module_utils.basic import AnsibleModule

def run_module():
	module_args = dict(name=dict(type='str' , required=True))
	module = AnsibleModule(argument_spec=module_args)
	result ={"changed":False , "message":f"Hello {module.params['name']}"}
	module.exit_json(**result)
if __name__ == "__main__":
	run_module()


