# Graylog Hook for Logrus <img src="http://i.imgur.com/hTeVwmJ.png" width="40" height="40" alt=":walrus:" class="emoji" title=":walrus:" />

Use this hook to send your logs to [Graylog](http://graylog2.org) server over UDP.
The hook is non-blocking: even if UDP is used to send messages, the extra work
should not block the logging function.

All logrus fields will be sent as additional fields on Graylog.

## Usage

The hook must be configured with:

* A Graylog UDP address (a "ip:port" string)
* A facility
* an optional hash with extra global fields. These fields will be included in all messages sent to Graylog

```go
import (
    "log/syslog"
    "github.com/Sirupsen/logrus"
    "github.com/gemnasium/logrus-hooks/graylog
    )

func main() {
    log := logrus.New()
    hook, err := log.AddHook(graylog.NewGraylogHook("<graylog_ip>:<graylog_port>", "some_facility", map[string]interface{}{"foo": "bar"}))
    log.Hooks.Add(hook)
    log.Info("some logging message")
}
```
