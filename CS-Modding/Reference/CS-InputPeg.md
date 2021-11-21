# Input Peg
This is the type of the members of the list [LogicComponent.Inputs](CS-LogicComponent.md#Inputs)

It is also the type that contains the information used by an input peg
## Fields
### `StateId: int {get; set;}`
This contains the id of the state of the input peg (TODO: More digging to find out what this state is)
### `On: bool {get;}`
This contains whether or not the peg is activated
### `SecretLinks: IReadOnlyList<InputPeg> {get;}`
Contains all the secret links that this peg has to another peg
### `PhasicLinks: IReadOnlyList<InputPeg> {get;}`
Contains all the phasic links that this peg is a part of

More on phasic links at the end of this file
### `OneWayPhasicLinkFollowers: IReadOnlyList<InputPeg> {get;}`
This is a list of other input pegs that this peg is a one way phasic link leader to
### `OneWayPhasicLinkLeaders: IReadOnlyList<InputPeg> {get;}`
This is a list of other input pegs that are one way phasic link leaders to this peg
### *readonly* `LogicComponent: LogicComponent`
This is the component this peg is attached to
### *readonly* `iAddress: InputAddress`
This is the address of this input
## Methods
### void AddSecretLinkWith(InputPeg otherInput)
This method connects this peg with a secret link to another peg
### void RemoveSecretLinkWith(InputPeg otherInput)
This method removes a previously made secret link to another peg
### void RemoveAllSecretLinks()
This method clears all secret links that this peg has
### void AddPhasicLinkWith(InputPeg otherInput)
This method generates a phasic link between this peg and another one

It will not create the link if there is already a phasic link between the 2 pegs
### void AddPhasicLinkWithUnsafe(InputPeg otherInput)
This does the same thing as AddPhasicLinkWith, but does not check if there is already a phasic link
### void RemovePhasicLinkWith(InputPeg otherInput)
This method removes a previously made phasic link with another peg

It safety checks if the link exists prior to calling or not
### void RemovePhasicLinkWithUnsafe(InputPeg otherInput)
This method does the same as AddPhasicLinkWith, but does not do the safety check
### void AddOneWayPhasicLinkTo(InputPeg otherInput)
This method adds a one way phasic link from this peg to another peg
### void RemoveOneWayPhasicLinkTo(InputPeg otherInput)
This method removes a one way phasic link from this peg to another peg
### void ClearAllPhasicLinks(InputPeg otherInput)
This method removes all phasic links this peg is a part of
# Phasic Links/One Way Phasic Links
A phasic link is a connection between to pegs where if one peg turns on the other peg immediately (0 ticks) and when both pegs are off the state also immediately updates

A one way phasic link is a link like above but only one peg drives the other rather than both pegs driving eachother in an or gate way

Examples
## Relay
```cs
protected override void DoLogicUpdate() {
  if (base.Inputs[1].On) {
    base.Inputs[0].AddPhasicLinkWith(base.Inputs[2]);
  } else {
    base.Inputs[0].RemovePhasicLinkWith(base.Inputs[2]);
  }
}
```
## Controlled Buffer
```cs
protected override void DoLogicUpdate() {
  if (base.Inputs[1].On) {
    base.Inputs[0].AddOneWayPhasicLinkTo(base.Inputs[2]);
  } else {
    base.Inputs[0].RemoveOneWayPhasicLinkTo(base.Inputs[2]);
  }
}
```
