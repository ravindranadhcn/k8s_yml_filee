# k8s_yml_files
to validate yml file in python 
first install pip3 install pyyaml

python -c 'import yaml, sys; yaml.safe_load(sys.stdin)' < pod-definition.yml



kubectl run redis --image=redis:alpine --labels="tier=db,type=in-memory" --dry-run=client -o yaml
