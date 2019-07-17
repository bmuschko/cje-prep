# Key CI/CD/Jenkins Concepts and their Usage

## Defining, Configuring and Organizing a Job

1. From the dashboard, click the "New Item" button.
2. Enter the item name "my-freestyle-job" and select "Freestyle project". Press the "OK" button.
3. In the job configuration, define the option to only keep the last 2 builds. Provide the description "A simple freestyle job". Upon building the project, a String parameter named `message` should be provided. Press the "Save" button.
4. Trigger a new build by pressing the "Build with Parameters" button. Enter a value for the `message` parameter. The build should finish successfully. Locate the provided parameter value in the build information.
5. Run the build two more times. What do you see?
6. Create a new view named "test". Add the job to the view.
7. Create a new folder named "freestyle" as part of the view. Move the job into the folder.
8. Locate the build information in `$JENKINS_HOME`. Inspect the directory structure.

<details><summary>Show Solution</summary>
<p>

We'll start by creating the new freestyle job.

![New Freestyle Job](./images/02-job-creation/new-freestyle-job.png)

Configure the job as follows.

![Job Configuration](./images/02-job-creation/job-configuration.png)

The build will ask for a parameter value when triggered.

![Build with Parameters](./images/02-job-creation/build-with-params.png)

The build history only stores the previous two builds.

![Build History](./images/02-job-creation/build-history.png)

Create a new view.

![New View](./images/02-job-creation/new-view.png)

After adding the job to the view, it will show up in a separate tab.

![Job in View](./images/02-job-creation/job-in-view.png)

Create a new folder.

![New Folder](./images/02-job-creation/new-folder.png)

The job became a child of the folder after moving it there.

![Job In Folder](./images/02-job-creation/job-in-folder.png)

Navigating to the `job` directory under the Jenkins Home reveals the build history.

```bash
$ cd /Users/bmuschko/.jenkins/jobs/freestyle/jobs
$ tree my-freestyle-job
my-freestyle-job
├── builds
│   ├── 1
│   │   ├── build.xml
│   │   ├── changelog.xml
│   │   └── log
│   ├── 2
│   │   ├── build.xml
│   │   ├── changelog.xml
│   │   └── log
│   ├── 3
│   │   ├── build.xml
│   │   ├── changelog.xml
│   │   └── log
│   ├── lastFailedBuild -> -1
│   ├── lastStableBuild -> 3
│   ├── lastSuccessfulBuild -> 3
│   ├── lastUnstableBuild -> -1
│   ├── lastUnsuccessfulBuild -> -1
│   └── legacyIds
├── config.xml
├── lastStable -> builds/lastStableBuild
├── lastSuccessful -> builds/lastSuccessfulBuild
└── nextBuildNumber

8 directories, 15 files
```

</p>
</details>