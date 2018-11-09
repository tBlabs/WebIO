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

## Board
```
import { Board } from 'BluePill.Client.Lib'

connectionString = '192.168.1.7:3000'
DIContainer.Bind(SampleBoard).ToConst(new Board(connectionString))
```


# BoardClient

```

abstract Sensor
{
	OnChange(callback)
	OrRising
	OnFalling
	
	get Value { value }
	
	UpdateFromHost(update)	
	{
		value = update.new
		
		ExecuteEvents(update)
	}
	
	abstract ExecuteEvents(update)
}

abstract class Actuator
{
	set Value(val)
	{
		connector.Set(addr, val)		
	}
	get Value
	{
		value
	}
	OnChange(callback)
	
	UpdateFromHost(update)
	{
		value = update.new
		ExecuteEvents(update)
	}
	
	ExecuteEvents(update)
	{
		if (update.new != update.old) onChange()
	}
}



class Input : Sensor
{
	ctor(addr)
	
	OnPress
	OnLongPress

	ExecuteEvents(update)
	{
		if (update.new != update.old) onChange()
	}
}

class Output
{
	ctor(addr, connector: IBoardSetter)
	{
		super(addr, connector)
	}
	
	On()/Off()
	{
		base.Value = 1/0
	}
}


class Board
{
	Input1: IInput = new Input(Addr.)
	Output1: IOutput = new Output(Addr.Out1, connector)
	
	ctor(connector)
	{
		connector.OnUpdate(addr, update=>
		{
			io = ByAddr(addr)
			io.UpdateFromHost(update)
		}
	}
}

class BoardConnector
{
	Set(addr, value)
	{
		socket.emit('set', addr, value)
	}
	
	OnUpdate: UpdateCallback
	
	ctor()
	{
		socket.on('update', u=>
			OnUpdate(u)
	}
}

socketClient = io(connectionString)
board = Board(new BoardConnector(socketClient))

board.Input1.OnChange((state)=>
{
	board.Output1.Value = state;  
})


ActuatorTest
	connectorMock = new Mock<IBoardConnector>
	
	board.Output1.Value = 1;

	connectorMock.verify(Set(1,1), Once)

SensorTest

	board.Input1.OnChange((v)=>expect(v==1))
	
	connectorMock.OnUpdate(1,1) 

```
