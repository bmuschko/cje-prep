# Key CI/CD/Jenkins Concepts and their Usage

## Storing and fingerprinting artifacts

1. Create a post-build action for archiving JAR file with the pattern `build/libs/*.jar`.
2. Execute the build. The build should list the artifact `gradle-initializr-1.0.0.jar`.
3. Have a look at the recorded fingerprints of this build.
4. Render the MD5 hash of the artifact and the usage of the artifact.
5. Install the Copy Artifacts plugin.
6. Create a downstream job named `consumer`.
7. Configure the downstream job to use the artifact produced by the upstream job.
8. Run the the build for the job `gradle-initializr`.
9. Have a look at the fingerprints of the downstream job.

<details><summary>Show Solution</summary>
<p>

In the job configuration, archive the artifact produced by the build. Check the box for generating fingerprints.

![Archive Artifacts](./images/07-artifacts/archive-artifacts.png)

Execute the build and find the archived artifact.

![Archived Artifact](./images/07-artifacts/build-artifact.png)

Have a look at the details of the fingerprinting.

![Fingerprint Details](./images/07-artifacts/fingerprint-details.png)

Install the Copy Artifacts plugin.

![Copy Artifacts Plugin](./images/07-artifacts/copy-artifacts-plugin.png)

Trigger the downstream job upon success.

![Trigger Downstream](./images/07-artifacts/trigger-upstream.png)

Copy artifacts from the upstream job.

![Copy Artifact From Upstream](./images/07-artifacts/copy-artifacts.png)

You can see the full usage of the artifact in upstream and downstream jobs.

![Fingerprint Usage](./images/07-artifacts/fingerprints-upstream.png)

</p>
</details>