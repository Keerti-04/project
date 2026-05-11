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
