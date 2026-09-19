## Reproducing the issue

In dev inbox, accept the proposal (giving a rating does not matter). Then in the dev inbox again, reject the proposal (this will not change the already present reasponse value, `accept` in this case), then fill out the reject reason form, this will record the reject `reason` next to the `accept` response, hence producing *inconsistent state*.

## Description of the issue

When submitting the review form, the PATCH endpoint only checks `reason` (for `reject`), but not `match_rating` (for `accept`). In more general terms, the mentor was allowed to record a review corresponding to a different `response value` (record a `reject reason` in case of already existing `accept` response value).

## With more time
 - I would model reponse differently, have a more generalized approach, a single matching `review` field next to `value`, and this would store the `reason` or `match_rating`. Currently if we would add a new type of response, e.g.: pending, or new fields to reject or accpet, we need to check for them manually inside of `views.py` and `services/student_proposal.py`.
 - Refactor the frontend so that we don't allow the user to record a review if we already have a corresponding review for our response.
