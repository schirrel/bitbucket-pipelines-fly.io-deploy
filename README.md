# Deploy to Fly.io with bitbucket-pipelines
How to deploy to fly.io using bitbucket pipelines


# Create Token
Go to your fly project under the token menu and generate a new token
<img width="1286" alt="Screenshot 2024-08-27 at 19 54 36" src="https://github.com/user-attachments/assets/20409f12-7ccc-455e-8ab4-905fd7d7605c">
<img width="1299" alt="Screenshot 2024-08-27 at 19 59 18" src="https://github.com/user-attachments/assets/9e771b3a-2471-42f4-9f64-eba77c2c9410">


# Save token as Variable
Now go to your bitbucket repository settings, under **Pipeline** side menu, at `Repository Variables` (aka `https://bitbucket.org/YOURORG/YOURPROJECT/YOURREPO/pipelines/repository-variables`).   
And create a new variable with the name `FLY_API_TOKEN`.
<img width="997" alt="Screenshot 2024-08-27 at 19 55 33" src="https://github.com/user-attachments/assets/a005e4ea-066f-4120-bc0b-5bcf0a49e200">

# Create pipeline file
Last but not least, create the pipeline file.  
Here you are going to use the golang image so we can install flyctl
```
image: golang:1.15
```

now we are going to create our pipeline steps
```
image: golang:1.15
pipelines:
  default:
    - step:
        name: Deploy to Fly.io
        deployment: production
```

and we will have the scripts as in a linux machine instalation

```
        script:
          - apt-get update -qq && apt-get install -y curl
          - curl -L https://fly.io/install.sh | sh
          - export FLYCTL_INSTALL="/root/.fly"
          - export PATH="$FLYCTL_INSTALL/bin:$PATH"
          - flyctl deploy
```





The sample file is at [bitbucket-pipelines.yml](./bitbucket-pipelines.yml).
