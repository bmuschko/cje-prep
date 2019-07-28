# Key CI/CD/Jenkins Concepts and their Usage

## Creating a User and Setting Permissions

1. Ensure that you are logged in as admin user.
2. Create a new user named `miller`. Provide the relevant information.
3. Configure Matrix Security by adding the admin user and the newly created user. The admin user should have all permissions. The `miller` user should only have read permissions for jobs and views.
4. Log out of the system.
5. Log in with the user `miller` and navigate to one of the jobs. Notice that you cannot edit the configuration or trigger a new build.

<details><summary>Show Solution</summary>
<p>

Create the new user.

![Create User](./images/08-matrix-security/create-user.png)

The new user is now listed.

![User Overview](./images/08-matrix-security/user-overview.png)

Configure users and permissions.

![Matrix Security](./images/08-matrix-security/matrix-security-permissions.png)

Log in with new user.

![Matrix Security](./images/08-matrix-security/user-login.png)

The job doesn't allow any editing or build triggering operations.

![Job Overview](./images/08-matrix-security/job-overview.png)

</p>
</details>