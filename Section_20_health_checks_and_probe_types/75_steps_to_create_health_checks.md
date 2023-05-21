# Steps to create healthchecks

## Questions to ask before adding healthchecks
- do we want liveness, readiness, both?
  - sometimes we can use the same check, but with different failure thresholds

- do we have existing HTTP endpoints that we can use?
- do we need to add new endpoints or perhaps use something else?
- /health or /readiness 
- are our healthcheck likely to use resources and/or slow down the app?
- do they depend on additional services?
  - this can be particularly tricky