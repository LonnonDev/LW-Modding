# LogicComponent
This is the file your component extends to do logic

All code examples in this assume you are in a class that extends this
## Fields
### Component: IComponentInWorld {get;}
This returns the ComponentDataManager of the component
### Address: ComponentAddress {get; set;}
This contains the address of the component
### Inputs: IReadOnlyList\<[InputPeg](CS-InputPeg.md)\> {get;}
This contains a list of the states of the input pegs of the component

To check if a peg is on or not use ```base.Inputs[PEG].On```
### Outputs: IReadOnlyList\<OutputPeg\> {get;}
This contains a list of the states of the output pegs of the component
  
To check if a peg is on or not use ```base.Outputs[PEG].On```
  
And to turn a peg on/off use ```base.Outputs[PEG].On = true/false```
  
Note: Outputs maintain state until changed i.e. they stay on until you turn them off
### ComponentData
This contains the data on the component which contains the following fields
- Type: ComponentType {get;}
  - This is the type of the component, i.e. if it is a board or inverter or etc...
  - types are hashable and comparable, and stored as integers internally
- InputCount: int {get;}
  - This is the number of inputs to the component
- OutputCount: int {get;}
  - This is the number of outputs the component has
- CustomData[]: byte {get;}
  - This is the custom data of the component
  - Do not edit these bytes raw, instead use LogicAPI.Data.ComponentDataManager.SetCustomData(byte[])
- Parent: ComponentAddress {get;}
  - This is the address of the parent component
- LocalPosition: Vector3 {get;}
  - This is the local position of the component
- LocalRotation: Quaternion {get;}
  - This is the local rotation of the component
### virtual HasPersistentData: bool {get;}
Determines whether the custom data of the component gets saved when saving the world
  
Override this to have your components data be saved as it is by default false
## Methods
### virtual void Initialize()
This is called upon component initialization

Override this to have custom initialization code, like printing a log message or something
### virtual void DoLogicUpdate()
This is called once after initialization, and after each update to input pegs (except for when the peg does not update the logic)
 
This should be overridden to do any logic

Example (Not Gate)
```
protected override DoLogicUpdate() {
  base.Outputs[0] = !base.Inputs[0]
}
```
### virtual IReadOnlyList\<bool\> GetOutputStartList()
Called by the circuit manager to get a list of the starting state of output pegs

Defaults to all off

Override this to have a custom starting state
### virtual bool InputAtIndexShouldTriggerComponentLogicUpdates(int inputIndex)
Determines whether a peg triggers DoLogicUpdate when updated or not
  
Default true

Override this to have certain pegs not update logic

Example (Only Update On Clock)
```
protected override bool InputAtIndexShouldTriggerComponentLogicUpdates(int inputIndex) {
  return inputIndex == CLOCK_INDEX;
}
```
### virtual bool OnCustomDataUpdated()
Called when the custom data of the component is updated

Default nothing
### virtual byte[] SerializeCustomData()
Used to serialize the custom data of the component for saving

Default null
### virtual void DeserializeData()
Used to deserialize the custom data of the component for loading
  
Default nothing
### virtual void SavePersistentValuesToCustomData()
Used to save persistent values to the custom data of the component

Default nothing  
### virtual void OnComponentMoved()
Called when the component moved

Default nothing
### virtual void OnComponentDestroyed()
Called when the component is destroyed

Default nothing
### virtual void Dispose()
Called when the component is disposed

Default nothing
# LogicComponent\<T\>
This is a special variant of LogicComponent that makes using custom data easier
  
It takes a generic argument which is a class that contains the data of the component
  
And it overrides the serialize and deserialize functions to bytewise write the and read the properties of the data class
