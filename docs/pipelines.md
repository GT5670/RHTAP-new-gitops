.Verification

. Push the updated configuration to your GitOps repository to trigger a rollout.

. Open {Product} interface and navigate to the entity you configured.

. Select the *CD* tab and then select the *GitOps application*. This opens a side panel. 

. In the *Resource* table of the side panel, verify that the following resources are displayed:

* Rollouts

* AnalysisRuns (optional)

. Expand a rollout resource and review the following details:

* The Revisions row displays details about traffic distribution between different rollout versions.

* The Analysis Runs row displays the status of analysis tasks that evaluate rollout success.
