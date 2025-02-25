. Push the updated configuration to your GitOps repository to trigger a rollout.

. Open {Product} interface and navigate to the entity you configured.

. Select the *CD* tab and then select the GitOps application. This opens a side panel. In the side panel we have the Resources table, in that table verify that it displays `Rollouts` and `AnalysisRuns` (optional).

Expand the Rollout object in the table. You should see:
The Revisions section, which displays details about traffic distribution between different rollout versions (for example, Canary or Blue-Green).
The Analysis Runs section, showing the status of AnalysisRuns associated with the rollout.
Ensure that rollout and analysis run details update dynamically when changes are pushed to the GitOps repository.
