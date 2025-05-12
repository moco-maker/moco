local Players = game:GetService("Players")
local player = Players.LocalPlayer

player.CharacterAdded:Connect(function(character)
    local humanoid = character:WaitForChild("Humanoid")
    local protected = true

    humanoid.HealthChanged:Connect(function()
        if protected then
            humanoid.Health = humanoid.MaxHealth
        end
    end)

    task.delay(10, function()
        protected = false
    end)
end)
