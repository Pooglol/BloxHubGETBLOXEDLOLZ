# Skybox and Decal Spam
_You mad kyle?_
```lua
local DECAL_ID = "rbxassetid://7224093030"
local SKY_ID = "rbxassetid://7224093030"

if workspace:FindFirstChild("DECAL_SPAM_DONE") then
	warn("Already ran once.")
	return
end

local flag = Instance.new("BoolValue")
flag.Name = "DECAL_SPAM_DONE"
flag.Parent = workspace

local lighting = game:GetService("Lighting")
lighting:ClearAllChildren()

local sky = Instance.new("Sky")
sky.SkyboxBk = SKY_ID
sky.SkyboxDn = SKY_ID
sky.SkyboxFt = SKY_ID
sky.SkyboxLf = SKY_ID
sky.SkyboxRt = SKY_ID
sky.SkyboxUp = SKY_ID
sky.Parent = lighting

local faces = {
	Enum.NormalId.Front,
	Enum.NormalId.Back,
	Enum.NormalId.Left,
	Enum.NormalId.Right,
	Enum.NormalId.Top,
	Enum.NormalId.Bottom
}

for _, obj in ipairs(workspace:GetDescendants()) do
	if obj:IsA("BasePart") then
		for _, face in ipairs(faces) do
			local decal = Instance.new("Decal")
			decal.Texture = DECAL_ID
			decal.Face = face
			decal.Parent = obj
		end
	end
end
```

**Skybox and Decal Spam Removal**
```lua
for _, obj in ipairs(workspace:GetDescendants()) do
	if obj:IsA("Decal") and obj.Texture == "rbxassetid://7224093030" then
		obj:Destroy()
	end
end

for _, obj in ipairs(game:GetService("Lighting"):GetChildren()) do
	if obj:IsA("Sky") then
		obj:Destroy()
	end
end

if workspace:FindFirstChild("DECAL_SPAM_DONE") then
	workspace.DECAL_SPAM_DONE:Destroy()
end

print("Undo complete.")
```

# Message
```lua
local message = Instance.new("Message")
message.Text = "Hi I am the owner"
message.Parent = workspace

task.wait(6)
message:Destroy()
```

# Hint
```lua
local message = Instance.new("Hint")
message.Text = "Hi I am the owner"
message.Parent = workspace

task.wait(6)
message:Destroy()
```
