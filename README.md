local Players = game:GetService("Players")
local player = Players.LocalPlayer
local RunService = game:GetService("RunService")

local function getNearestEnemy()
    local character = player.Character
    if not character or not character:FindFirstChild("HumanoidRootPart") then return end

    local nearestEnemy = nil
    local shortestDistance = math.huge

    for _, enemy in pairs(workspace.Enemies:GetChildren()) do
        if enemy:FindFirstChild("HumanoidRootPart") and enemy:FindFirstChildOfClass("Humanoid") then
            local distance = (character.HumanoidRootPart.Position - enemy.HumanoidRootPart.Position).magnitude
            if distance < shortestDistance then
                shortestDistance = distance
                nearestEnemy = enemy
            end
        end
    end

    return nearestEnemy
end

local function dodge()
    local character = player.Character
    if character and character:FindFirstChild("HumanoidRootPart") then
        local currentPos = character.HumanoidRootPart.Position
    
        character.HumanoidRootPart.CFrame = CFrame.new(currentPos + Vector3.new(math.random(-50,50), 0, math.random(-50,50)))
    end
end

local function protect()
    local character = player.Character or player.CharacterAdded:Wait()
    local humanoid = character:WaitForChild("Humanoid")

    humanoid:GetPropertyChangedSignal("Health"):Connect(function()
        if humanoid.Health < humanoid.MaxHealth then
            dodge()
            humanoid.Health = humanoid.MaxHealth
        end
    end)
end

protect()
player.CharacterAdded:Connect(protect)
