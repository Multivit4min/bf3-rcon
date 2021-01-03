## Battlefield 3 RCON Interface

[![npm](https://img.shields.io/npm/v/vu-rcon.svg)](https://www.npmjs.com/package/vu-rcon)

Example

```typescript
import { Battlefield } from "./src/Battlefield"

Battlefield.connect({ 
  host: "127.0.0.1",
  port: 47200,
  password: "RCON_PASSWORD"
}).then(async bf3 => {

  //listen to different events
  bf3.on("playerJoin", ({ name }) => bf3.say(`${name} is joining the game...`))
  bf3.on("playerLeave", event => console.log({ event }))
  bf3.on("kill", ({ killed, weapon }) => killed.say(`You just got killed with ${weapon.name}`))

  //get a list of players and yell the name to them
  const players = await bf3.getPlayers()
  players.forEach(player => player.yell(`Hello ${player.name}`))

  //ban someone
  const player = bf3.getPlayerByName("foobar")
  await player.banGuid().reason("foo").permanent().send()

})
```