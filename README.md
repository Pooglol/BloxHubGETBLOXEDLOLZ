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
```lua
local message = Instance.new("Message") message.Text = "Hi I am the owner" message.Parent = workspace task.wait(6) message:Destroy()
```

# Hint
```lua
local message = Instance.new("Hint")
message.Text = "Hi I am the owner"
message.Parent = workspace

task.wait(6)
message:Destroy()
```
```lua
local message = Instance.new("Hint") message.Text = "Hi I am the owner" message.Parent = workspace task.wait(6) message:Destroy()
```

Fling Command (/e fling <user/display>)

```lua
local Players = game:GetService("Players")

local function fling(speaker, targetName)
    local target = nil
    for _, v in pairs(Players:GetPlayers()) do
        -- Matches short names or display names
        if v.Name:lower():sub(1, #targetName) == targetName:lower() or v.DisplayName:lower():sub(1, #targetName) == targetName:lower() then
            target = v
            break
        end
    end

    if target and target.Character and target.Character:FindFirstChild("HumanoidRootPart") and speaker.Character:FindFirstChild("HumanoidRootPart") then
        local root = speaker.Character.HumanoidRootPart
        local tRoot = target.Character.HumanoidRootPart
        
        -- Apply the spin
        local bfv = Instance.new("BodyAngularVelocity")
        bfv.AngularVelocity = Vector3.new(0, 99999, 0)
        bfv.MaxTorque = Vector3.new(0, math.huge, 0)
        bfv.P = math.huge
        bfv.Parent = root
        
        -- Brief overlap to trigger physics collision
        root.CFrame = tRoot.CFrame * CFrame.new(0, 0.5, 0)
        
        task.wait(0.3)
        bfv:Destroy()
    end
end

-- Server-side chat listener
Players.PlayerAdded:Connect(function(player)
    player.Chatted:Connect(function(msg)
        local args = msg:split(" ")
        if args[1] == "/e" and args[2] == "fling" and args[3] then
            fling(player, args[3])
        end
    end)
end)

-- Run for players already in the game
for _, player in pairs(Players:GetPlayers()) do
    player.Chatted:Connect(function(msg)
        local args = msg:split(" ")
        if args[1] == "/e" and args[2] == "fling" and args[3] then
            fling(player, args[3])
        end
    end)
end
```
