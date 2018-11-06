# Hardware

- BluePill.Firmware

# Hardware drivers

- BluePill.Driver
- BluePill.Daemon

# Clients

- BluePill.Driver (yep, it's also http client)
- BluePill.Client.Lib (in progress)
- BluePill.Client.Cli (to do)
- BluePill.Client.Http (very long future)

# Managers

- FlowManager

## Flow example 
```
class SampleFlow
{
  ctor(SampleActorA, SampleActorB) { }
  
  Init()
  {
    sampleActorA.Action(()=>
    {
      sampleActorB.Set();
    })
  }
}
```

## Actor example
```
class SampleActor
{
  ctor(SampleBoard) { }
  
  Action(callback)
  {
    board.Sensor.OnEvent(callback)
  }
  
  Set()
  {
    board.Actuator.Set()
  }
}

```
