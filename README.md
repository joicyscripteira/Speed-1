-- Boost de velocidade (corrida) seguro para anti-cheat
local Players = game:GetService("Players")
local UIS = game:GetService("UserInputService")
local player = Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humanoid = character:WaitForChild("Humanoid")

-- GUI para botão de celular (opcional)
local screenGui = Instance.new("ScreenGui", player:WaitForChild("PlayerGui"))
screenGui.Name = "SpeedBoostGUI"

local button = Instance.new("TextButton")
button.Size = UDim2.new(0, 100, 0, 40)
button.Position = UDim2.new(1, -110, 1, -50)
button.Text = "Speed ON"
button.BackgroundColor3 = Color3.fromRGB(0, 170, 255)
button.TextColor3 = Color3.new(1,1,1)
button.Parent = screenGui

-- Variáveis
local boosted = false
local normalSpeed = 16 -- Velocidade padrão
local boostedSpeed = 13.88 * 3.6 -- 50km/h ≈ 13.88 studs/s; Roblox usa valores mais altos para corrida suave

-- Alternar Boost ao clicar
button.MouseButton1Click:Connect(function()
	if not character or not character:FindFirstChild("Humanoid") then return end
	boosted = not boosted
	humanoid.WalkSpeed = boosted and boostedSpeed or normalSpeed
	button.Text = boosted and "Speed OFF" or "Speed ON"
	button.BackgroundColor3 = boosted and Color3.fromRGB(255, 50, 50) or Color3.fromRGB(0, 170, 255)
end)

-- Reaplicar velocidade se morrer/resetar
player.CharacterAdded:Connect(function(char)
	character = char
	humanoid = character:WaitForChild("Humanoid")
	humanoid.WalkSpeed = boosted and boostedSpeed or normalSpeed
end)
