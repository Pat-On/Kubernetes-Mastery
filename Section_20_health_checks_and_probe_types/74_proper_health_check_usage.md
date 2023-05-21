# Proper healthcheck usage


## should probes check container Dependencies

- a HTTP/TCP probe can not check an external dependency
- but a HTTP url could kick of code to validate a remote dependency
- if a web server depends on a database to function, and the database is down
  - the web server's  liveness probe should succeed
  - the web server's readiness probe should fail

- same thing for any hard dependency (without which the container can not work)

! Do not fail liveness probes for problems that are external to the container

## Healthchecks for workers

in that context, worker = process that does not accept connections

- readiness is not useful
  - because workers are not backends for a service
- Liveness may help us restart a broken worker, but how can we check it?
- embedding an HTTP server is a (potential expensive) option
- using a 'lease' file can be relatively easy:
  - touch a file during each iteration of the main loop
  - check the timestamp of that file from an exec probe
- writing logs and checking them from the probe also works  <------- Interesting idea