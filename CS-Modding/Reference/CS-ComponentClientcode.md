# ComponentClientCode

## Fields

### `Component => ComponentDataManager: IComponentInWorld`

### `Address {get;}: ComponentAddress`

### `BlockCount => BlockEntities.Count: int`
The amount of Blocks
### `InputCount => InputE.ntities.Count: int`
The amount of Inputs.
### `OutputCount => OutputEntities.Count: int`
The amount of Outputs.
## Methods

## internal void SetupForWorld_BeforePrefab(WorldRenderer worldRenderer, ComponentAddress cAddress, ComponentInfo info, ComponentDataManager componentDataManager)

## internal void SetupForWorld_AfterPrefab(ComponentAddress cAddress)

## internal void SetupForWorld_AfterDecorations(bool inMainWorld)

## protected virtual void Initialize()
This function runs when the component is interacted with.
## protected virtual void InitializeInGhost()
This function is ran when you see the ghost of the object.
## protected virtual void InitializeInWorld()
This function is ran when the Component is places.
## protected internal virtual void OnComponentReRendered()
This runs when the Component is Rerendered.
## protected internal virtual void OnComponentDestroyed()
This is ran when the Component is destroyed.
## protected internal virtual void OnComponentImaged()
?
## public void QueueFrameUpdate()
Queues a frame update.
## internal void FrameUpdateWrapper()
?
## protected virtual void FrameUpdate()
Ran when the Frame Updates.
## protected void ContinueUpdatingForAnotherFrame()
Update for another frame.
## public ChildPlacementInfo GetChildPlacementInfo()
?
## protected virtual ChildPlacementInfo GenerateChildPlacementInfo()
?
## protected void MarkChildPlacementInfoDirty()
?
## public bool HasCustomPlacementInfo()
?
## internal virtual void SetDefaultCustomData()
?
## public virtual void OverrideCustomDataInPickedUpComponent()
?
## public void QueueDataUpdate()
Queues a data update.
## internal void DataUpdateWrapper()
?
## protected virtual void DataUpdate()
Ran when data is updated.
## public virtual byte[] SerializeCustomData()
?
## protected virtual void DeserializeData(byte[] data)
?
## public void ReloadCustomDataClientSide()
Reloads custom data.
## internal void LoadCustomDataClientSide(byte[] data, bool queueDataUpdate = true)
Load Custom data client side.
## public void ForceDataRefreshClientSide()
Forces data refresh from client side.
## public IList<IDecoration> GetDecorations()
Get's the decorations.
## protected virtual IList<IDecoration> GenerateDecorations()
Generate decorations.
## public virtual PlacingRules GenerateDynamicPlacingRules()
Generate dynamic placing rules.
## public bool GetInputState(int inputNumber = 0)
Get input state.
## public bool GetOutputState(int outputNumber = 0)
Get output state.
## protected void SetBlockColor(Color24 color, int blockIndex = 0)
Set block color with 24 bit color.
## protected void SetBlockColor(Color32 color, int blockIndex = 0)
Set block color with 32 bit color.
## protected void SetBlockPosition(int blockIndex, Vector3 localPosition)
Sets the block's position.
## protected void SetBlockRotation(int blockIndex, Vector3 localEulerAngles)
Sets the block's rotation with euler angles.
## protected void SetBlockRotation(int blockIndex, Quaternion localRotation)
Sets the block's rotation with quaterinons.
## protected void SetBlockScale(int blockIndex, Vector3 scale)
Sets the blocks scale.
## protected void SetInputPosition(byte inputIndex, Vector3 localPosition)
Sets the input position.
## protected void SetOutputPosition(byte outputIndex, Vector3 localPosition)
Sets the output position.
## protected void SetInputRotation(byte inputIndex, Vector3 localEulerAngles)
Sets input rotation with euler angles.
## protected void SetInputRotation(byte inputIndex, Quaternion localRotation)
Sets input rotation with quaternions.
## protected void SetOutputRotation(byte outputIndex, Vector3 localEulerAngles)
Sets output rotation with euler angles.
## protected void SetOutputRotation(byte outputIndex, Quaternion localRotation)
Sets output rotation with local rotation.
## protected Vector3 GetRawBlockScale(int blockIndex = 0)
Get block scale.
## protected IRenderedEntity GetBlockEntity(int blockIndex = 0)
Get block entity.
## protected void SetDecorationPosition(int decorationIndex, Vector3 newLocalPosition)
Set decoration position.
## protected void TweenDecorationPosition(int decorationIndex, Vector3 newLocalPosition, float tweenTime)
Set decoration position with tweening.
## protected void SetDecorationRotation(int decorationIndex, Quaternion newLocalRotation)
Set decoration rotation.
## protected void TweenDecorationRotation(int decorationIndex, Quaternion newLocalRotation, float tweenTime)
Set decoration rotation with tweening.
## protected void SetDecorationScale(int decorationIndex, Vector3 newScale)
Set decoration scale.
## protected void TweenDecorationScale(int decorationIndex, Vector3 newScale, float tweenTime)
Set decoration scale with tweening,
## protected void RegenerateDynamicContent()
?