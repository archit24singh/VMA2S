# VMA2S
DevSecOps projects which I've built and am in the process of open sourcing it
<img width="1039" alt="sample_devsecops_arch_1" src="https://github.com/archit24singh/VMA2S/assets/65055187/73349795-8f9a-4f21-abe1-f532f48cf960">

## DVPWA + Bandit
Run bandit SAST scans over the dvpwa (Damn Vulnerable Python Web Application) repository using GitLab CI.
#update things here regarding the 3 screenshots you added (with ref links) start a new project

### Code
```yaml
stages: #denotes the stages in the pipeline. we need only one stage.
  - bandit_scan #since we're running a bandit scan, it's bandit_scan :)

build-job:
  stage: bandit_scan #which stage does this job belong to?
  image: python:3.6 #what image are we cloning to run this?
  script:
    - git clone https://github.com/anxolerd/dvpwa #clone DVPWA
    - cd dvpwa #cd into the folder
    - pip3 install bandit #install the bandit package
    # Run bandit with verbose (-v), recursive (-r) so that it scans all the subdirectories too, pass the path to dvpwa, output format as json (-f), and we want to store the output file as result.json (-o)
    - bandit -v -r /builds/sample_devsecops/damnvulnerablepythonapp/dvpwa -f json -o /builds/sample_devsecops/damnvulnerablepythonapp/dvpwa/result.json
  artifacts: #To keep the generated output result.json as an artifact
    when: always #ensure that this artifact is present even if the build fails
    paths: #where to store the artifact
      - /builds/sample_devsecops/damnvulnerablepythonapp/dvpwa/result.json
```
Clean code present in .gitlab-ci.yml

### Results
Update the YAML CI/CD Code into a repository as the .gitlab-ci.yml file.
<img width="1288" alt="dvpwa_bandit_1" src="https://github.com/archit24singh/VMA2S/assets/65055187/e664b5f0-2d68-419e-942d-b53bfc9f65db">

Auto-trigger the pipeline when a commit is made to the repository and a valid .gitlab-ci.yml file is present. As indicated, Artifact is generated and uploaded.

<img width="1448" alt="dvpwa_bandit_2" src="https://github.com/archit24singh/VMA2S/assets/65055187/2b51b2bf-f0ef-4980-9010-fbee89833cbf">

Artifact contains bandit scan reports of the Damn Vulnerable Python Web Application as highlighted below.



<img width="1725" alt="dvpwa_bandit_3" src="https://github.com/archit24singh/VMA2S/assets/65055187/b19a05cc-4d48-44ab-b9e4-abf289faa82b">













