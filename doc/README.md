# Plugin

https://github.com/influxdata/telegraf/blob/master/CONTRIBUTING.md

"His plugin code looks good to go. He needs to place that file in $GOPATH/src/github.com/influxdata/telegraf/plugin/inputs/testPlugin/testPlugin.go

He should write a test for the plugin and place it at $GOPATH/src/github.com/influxdata/telegraf/plugin/inputs/testPlugin/testPlugin_test.go

After this is complete he needs to register the plugin at $GOPATH/src/github.com/influxdata/telegraf/plugin/inputs/all/all.go

Then he should run make from $GOPATH/src/github.com/influxdata/telegraf. This will place the new telegraf binary in $GOPATH/bin/telegraf.

Run the binary with the following flags to generate the valid configuration:

$GOPATH/bin/telegraf -sample-config -input-filter testPlugin -output-filter influxdb > testPlugin_config.conf

From there you can run the binary with the -test flag by passing it the sample config:

$GOPATH/bin/telegraf -config testPlugin_config.conf -test

This will output the line protocol that is to be inserted into the database."

-> And the testPlugin.go that he talks about:`
```
package testPlugin

import (
    "time"
)

type ReadFile struct {
 counter int64
}

func (s *TestPlugin) Description() string {
  return "This is a test plugin to write data to influxdb with a plugin"
}

func (s *TestPlugin) SampleConfig() string {
  return "ok = true # indicate if everything is fine"
}

func Gather(acc telegraf.Accumulator) error {

c := time.Tick(10 * time.Second)
for now := range c {
    counter := counter + 1
    acc.Add("counter",counter, tags)
 }
} 

func init() {
  inputs.Add("testPlugin", func() telegraf.Input { return &TestPlugin{} })
}
```
