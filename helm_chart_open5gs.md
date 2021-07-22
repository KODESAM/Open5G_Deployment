# Install chart from helm repository

# charts in `charts/`` folder are packaged and available at Gradiant's openverso helm repo:

https://gradiant.github.io/openverso-charts/

# You can add the helm repo to your Helm CLI:

helm repo add openverso https://gradiant.github.io/openverso-charts/

# Then you have a collection of charts available to install. For example, to install open5gs:

helm install openverso/open5gs

# Install chart from release

# install using the URL of the release. For example, to install open5gs v0.1.0 chart:

helm install https://github.com/Gradiant/openverso-charts/releases/download/open5gs-0.1.0/open5gs-0.1.0.tgz
