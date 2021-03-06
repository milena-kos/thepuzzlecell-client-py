# The Puzzle Cell Client Python Package
This package allows you to connect to TPC servers as a client and send packets.

Available at [PyPi](https://pypi.org/project/thepuzzlecell/)

# Documentation

## Install

To use The Puzzle Cell Client, install it using pip:
```
pip install thepuzzlecell
```

## Quickstart

Here is a quick example:
```py
import thepuzzlecell

async def test():
    connection = await thepuzzlecell.client("wss://tpc.milenakos.repl.co", "2.0", "Hello World Client")
    
    await connection.send_packet("Hello")
    await connection.send_packet("World!")

    for y in range(0, 10):
        await connection.place(x=0, y=y, id="push")

    print(connection.get_packets())
    
    await connection.close()

asyncio.run(test())
```

Easy, right?

## API and stuff

- `thepuzzlecell`

  - `client(ip, version="2.0", client_id="PythonUser", auto_reconnect=False)` creates a `Client()` and returns it

  - `Client` is main class

    - async `connect()` does not take any arguments and runs on self variables

    - `listen()` runs a loop to listen for any incoming packets (interal; not recommended to use externally)

    - async `get(websocket)` returns information from given websocket

    - async `send_packet(data)` send given information into self.websocket

    - async `close()` closes self.websocket

    - `get_packets(**wait_until_packet=False)` gets packets collected by `listen()`

      - `get_packet(**wait_until_packet=False)` is an alias for it

    - async `place(**x, **y, **id, **rot=0, **heat=0)` places cell

    - async `bg(**x, **y, **bg="placeable")` sets background (placeables)

    - async `setinit(code)` sets initial state on the server

    - async `new_hover(**uuid=self.client_id, **x, **y, **id, **rot=0)` creates new hover

    - async `set_hover(**uuid=self.client_id, **x, **y)` sets the new hover position

    - async `drop_hover(uuid=self.client_id)` removes the hover

    - async `set_cursor(**uuid=self.client_id, **x, **y)` sets cursor state