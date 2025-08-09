##### Sonarqube Mac Installation #####
helm repo add sonarqube https://SonarSource.github.io/helm-chart-sonarqube
helm repo update

helm template sonarqube sonarqube/sonarqube \
  --version 2025.3.1 \
  -f sonarqube-values.yaml -n tools --create-namespace --debug

helm install sonarqube sonarqube/sonarqube \
  --version 2025.3.1 \
  -f sonarqube-values.yaml -n tools --create-namespace

helm upgrade sonarqube sonarqube/sonarqube \
  --version 2025.3.1 \
  -f sonarqube-values.yaml \
  -n tools
 
#for latest chart version
helm repo update
helm upgrade sonarqube sonarqube/sonarqube \
  -f sonarqube-values.yaml \
  -n tools

#for diff in previous version
helm diff upgrade sonarqube sonarqube/sonarqube \
  --version 2025.3.1 \
  -f sonarqube-values.yaml \
  -n tools
#####

helm install sonarqube . -n tools
helm upgrade sonarqube . -n tools

kubectl delete pv sonarqube-pv postgres-pv
