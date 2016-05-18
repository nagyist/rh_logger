# rh_logger
## A package for logging / process status / metrics reporting for rhoana

How to use:

* `logger = rh_logger.get_logger(name, args)`: get a logger with the process's name and enough context in `args` to figure out the data inputs and outputs used to run it.
* `logger.start_process(msg)`: log the start of a process
* `logger.end_process(msg)`: log the end of a process
* `logger.report_metric(name, metric, subcontext=None)`: Report a metric such as accuracy or execution time. Subcontext gives enough information to narrow the metric to an instance of the named step.
* `logger.report_event(event, context=None)`: Report an event.  Context gives enough information to narrow the metric to an instance of the named step.
* `logger.report_exception(exception=None, msg=None)`: Report an exception. Exception is last exception thrown by default. Message is `str(exception)` by default.

Configuring:

rh_logger uses entry points to register and find its backend. The entry point
group is "rh_logger.backend". rh_logger comes with a default logger that logs
via Python logging. You can either specify another logger's entry point name
using the RH_LOGGING_BACKEND environment variable or call
`rh_logger.set_logging_backend` to pick a backend before calling
`rh_logger.get_logger`.

## Datadog logger

Datadog is a centralized console and API for monitoring a distributed
application (https://app.datadoghq.com). You can use rh_logging with the
datadog logger if you have a datadog account and have API and APP keys
for your application.

To configure:
* Set the RH_LOGGING_BACKEND environment variable to "datadog"
* Set the RH_DATADOG_API_KEY environment variable to your datadog API key
* Set the RH_DATADOG_APP_KEY environment variable to your datadog app key
* Use 'rh_logger.get_logger()' to get yourself a logger and log away.
