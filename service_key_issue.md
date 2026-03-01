# GCP Service Account Key Creation Disabled

This document is to address `Service Account Key Creation Disabled` issue. Sometime in February, Google decided to set deny service key creation as the default policy.

If we follows the setup guide [here](https://drive.google.com/file/d/1UlqE8E9si7ATKmj0mJn4zj4NMvOQODXa/view?usp=sharing), some of us might get this problem. Please note that as Google is progressively propagate this policy not all of us will be affected.

During service account key creation, affected users will get the following error message.

![alt text](assets/error.png)


Once we encounter this issue, we need to check our project settings. To go to project settings, click the 3 dot on the top right corner and select `Project settings`

![alt text](assets/get_project_settings.png)

On the project settings, notice the location which is under an organization. (See image below). This is how Google propagate this policy.

![alt text](assets/project_settings.png)

To get around this limitation, there is 2 options:
- Create a new project under `No Organization`
- Give ourselves proper credential to disable this policy

## Option 1: Create a new project under `no organization`

First click on the project selection option as shown below:

![alt text](assets/get_create_new_project.png)

We should see the screen similar to below:

![alt text](assets/project_page.png)

Click on the top left organization and select `No organization`:

![alt text](assets/orgn_selection.png)

After that you should see something similar but no projects created. 

![alt text](assets/no_orgn.png)

Click `New project` on the top right corner.

![alt text](assets/new_project.png)

Select a project name that is unique so that the id is the same as project name. Most important make sure that under `Organization` we have no organization.

Once the project is created, it should be similar as below

![alt text](assets/after_new_project.png)

Next, refer to the setup guide [here](https://drive.google.com/file/d/1UlqE8E9si7ATKmj0mJn4zj4NMvOQODXa/view?usp=sharing) and repeat step 3 to step 5.

Once your service is created you should see something similar.

![alt text](assets/svc_key_ok.png)

After service key is downloaded, we need to re-configure our CLI (command line interface). You need to execute both instructions.

For Windows WSL user:

```bash
gcloud init
```

follow by:

```bash
gcloud auth application-default login
```

For Mac users:

```bash
# Try
gcloud init

# If not working try
./google-cloud-sdk/bin/gcloud init
```

follow by:

```bash
# Try
gcloud auth application-default login

# If not working try
./google-cloud-sdk/bin/gcloud auth application-default login
```

> To test out if your connection is good, you can re-run lesson 2.2 under Google Cloud Storage. (DO NOT USE Anonymous Client).

> If you still encounter error such as `billing account not enabled`, please add a credit card to the account and link to the appropriate project.


## Option 2: Override the Disable Service Key Creation Policy

Please follow the [video here on how to Override the Disable Service Key Creation Policy](https://drive.google.com/file/d/104oQPv5-DNWPe28gXGj1pbin9yilbGVX/view?usp=sharing)


1. Go to the home screen and click on the projects selector

![alt text](assets/override_policy/home_screen.png)

2. Select the organization

![alt text](assets/override_policy/select_orgn.png)

3. Resulting screen is as follows and click on the search bar:

![alt text](assets/override_policy/orgn_selected.png)

4. Select `IAM & Admin`

![alt text](assets/override_policy/select_iam.png)

5. Click on the edit button to add a new role

![alt text](assets/override_policy/edit_add_roles.png)

6. Click on `Add Another Role`

![alt text](assets/override_policy/add_new_role.png)

7. Add `Organization Policy Administrator` and click `Save`

![alt text](assets/override_policy/add_orgn_policy_admin.png)

8. Select `Organization Policies`

![alt text](assets/override_policy/select_orgn_policies.png)

9. Click to search the policies

![alt text](assets/override_policy/search_policies.png)

10. Type and search for `Disable Service Account Key Creation`

![alt text](assets/override_policy/search_for_disable_service_key.png)

11. You should have 2 policies as shown below:

![alt text](assets/override_policy/disable_creation_policies.png)

**Please note that we need to override both policies using the follow ways.** Click on the first policy.

12. Click on `Manage Policy`

![alt text](assets/override_policy/manage_policy.png)

13. Select `Override Parents Policies`

![alt text](assets/override_policy/select_override.png)

14. Click on `Add Rule`

![alt text](assets/override_policy/add_rule.png)

15. Set `Enforcement` to `Off` and click `Done`

![alt text](assets/override_policy/set_enforcement_off.png)

16. Click on `Set Policy`

![alt text](assets/override_policy/set_policy.png)

**You need to override both policy shown in step 11.**

You can proceed to download the service key. However, if you encounter issue you will need to perform step 11 to step 16 at the project level.

### To switch from Organization to Project Level

1. Click project selector

![alt text](assets/override_policy/click_project_selector.png)

2. Select your project

![alt text](assets/override_policy/select_project.png)

3. Search for policy at the project level

![alt text](assets/override_policy/search_policies_project.png)

Then you need to override both policies at the project level by repeating step 11 to step 16. 