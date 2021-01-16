# Theta Quartz Plugin Docs

## Pokemon Essentials
Theta Quartz, just like many other fangames, is created using Pokemon Essentials. All the commands from Pokemon Essentials are functional within the Plugin.

You can use RGSS (Ruby Game Scripting System), The scripting language for Pokemon Essentials, to create your own plugins for the game.

## Usage Example

```rb
Plugin.reigster({
  :NAME => "Example Plugin",
  :VERSION => "Beta 6.9 Final Release",
  :CREDITS => ["Author 1","Author 2""Author 3"] #... so on.
}) # Registers a new plugin with the specific name, Version and credits.

module TQEvents
  def self.mart # Redefines the pre-existing mart event, to disable it's functionality
    pbMessage("You have disabled the Pokemart in this Plugin.")
  end
end

```
## Setup
Firstly, Download The Plugin Compiler from here(add hyperlink). After downloading the Compiler, Head into the folder called `Scripts`. You will write all the code there.
The extension used for Plugins is `.rb`, And they are written in the form of RGSS. You can create multiple files as per your need, And after you're done, Run `Compiler.exe` to compile the plugins into one Single Plugin File with the extension `.tq` which is usable in the game.
To load the plugin into the game, Paste the `.tq` Plugin File into the `Plugins` Folder within the Game's Main Folder.

## API

### Structuring the Plugin

For creating a new plugin, You need to use the method `Plugin.register`.

`Plugin.register` takes a hash as its argument. The hash contains a key value pair of `:NAME`, `:VERSION`, and `:CREDITS`.

`:NAME` contains the plugin's Name. `Type: String`

`:VERSION` contains the Plugin's Version.  `Type: String`

`:CREDITS` contains a list of people to credit. `Type: String Array`

**Examples**
```rb
# ====================
Plugin.register(
  {
    :NAME => "Youngster Joey Everywhere",
    :VERSION => "v1.3",
    :CREDITS => ["TheBanana"]
  }
)
# ====================
Plugin.register(
  {
    :NAME => "Nuzlocke Mode",
    :VERSION => "Beta 1.3",
    :CREDITS => ["Staline","Trumphet"]
  }
)
```
 
After calling the registration method, you can extend any of the modules listed in the next topic, and create your plugin.

```rb
# ==================================
module TQEvents
  def self.pokecenter
    pbMessage(_INTL(
      "The Nurse Joy event is now modified to not heal the Player's Pokemon."
    ))
  end
  def self.faint
    pbMessage(_INTL(
      "You just fainted, What a weakling.." 
    ))
  end
end
# ==================================
# Adds a new function that deletes all the existing trainers.
module TQTrainers
  def self.delete
    newdata = {}
    self.compile(newdata)
  end
end

```
--------------------------------------

### Modules and Methods

| Module | Information |
| --- | --- |
| TQEvents | Contains methods of all the major events. |
| TQTrainers | Contains Trainers, Their data and functions. |

#### `TQEvents` Methods

| Method | Information |
| --- | --- |
| pokecenter | The Nurse Joy event. |
| pokemart | The Mart Guy event. |
| starter | The Starter Choosing event. |
| menu | The Pause Menu event. |
| faint | The Faint event (Called when Player's party faints.) |

#### `TQTrainers` Methods

| Method | Information | Example |
| --- | --- | --- |
| getTrainers | Returns a hash containing all of the Trainers. | --- |
| battle(trainer) | Starts a new Trainer Battle. | `TQTrainers.battle("Youngster_Joey")` |
| battle_end(trainer,win?) | This function is called after a battle ends. | `TQTrainers.battle_end("Youngster_Joey",true)` |
| compile(hash) | Compiles the Trainer's data defined in `hash`, Is called after adding a new trainer into `data` hash | `TQTrainers.compile(trainers)` |

Other than module specific methods, there are also some **Global Functions**:

| Function | Information | Example |
| --- | --- |--- |
| tqGetLevel | Returns an integer (level) based upon Player's Party. Open World Level.| `tqGetLevel` |
| tqTextInput(title,minimum_characters,maximum_characters) | Takes a Keyboard Input from Player and returns it. | `player_name = tqTextInput("What is your Name?")` |
| tqJsonStringify(string) | Converts a JSON String `string` into Ruby Hash. | `tqJsonStringify( "any JSON String" )` |
