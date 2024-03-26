<a href="#" onclick="history.back()">back</a>

## Failure Scenarios

This page defines the foreseen failure scenarios within the BaRS standard and its implementations. The scenarios are broken down by endpoint and describe which HTTP Status Code, BaRS HTTP Error Code and FHIR issue.code to use for each eventuality. In any case, the diagnostics text should reflect the scenarios given and not necessarily be used verbatim where examples are given.

The rationale, described in the {{core-failure_scenarios-1.1.3, text:error handling}} section is that as much information on the nature of the failure as possible is provided in a standard way.

Each scenario has a Source to state whether it is the BaRS Proxy or the Receiver which is generating the error. In scenarios where a SEND prefix is used, the sender is not adhering to the API specification in one way or another. These codes are held within OperationOoutcome.issue.details.code and use the http-error-codes value set.

Note: in future, the PROXY prefix will no longer be used, and all errors from the Proxy will use a code with no prefix.