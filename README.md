# tem-auth-service
the eternal monuments auth service

1. add the default ssh key (if you have multiple keys) inorder to add the private repo (defined in requirements.txt) before build
```
ssh-add ~/.ssh/id_ed25519_ramchn  # To add a specific key
```

2. local build - venv creation and activation:
```
python3 -m venv venv
source venv/bin/activate
```

3. build with public requirements using the container
```
grep -v "git+" requirements.txt > public_requirements.txt 
sam build --build-dir build --use-container --manifest public_requirements.txt
```

4. build with private requirements not using the container
```
grep "git+" requirements.txt > private_requirements.txt
python -m pip install -r private_requirements.txt --no-deps -t build/LoginFunction/
```

5. manual copy of the fourth party library from build folder to src folder


6. deploy the service
```
sam deploy --config-env dev
```