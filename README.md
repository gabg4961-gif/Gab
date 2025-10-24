-- 🌈 LOADING SCREEN + TELEGUIADO BY.GAB 🌈
local Players = game:GetService("Players")
local TweenService = game:GetService("TweenService")
local RunService = game:GetService("RunService")

local player = Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humanoidRoot = character:WaitForChild("HumanoidRootPart")
local PlayerGui = player:WaitForChild("PlayerGui")

-- ==================== LOADING SCREEN ====================
local screenGui = Instance.new("ScreenGui")
screenGui.Name = "LoadingScreen"
screenGui.Parent = PlayerGui

local frame = Instance.new("Frame")
frame.Size = UDim2.new(1,0,1,0)
frame.Position = UDim2.new(0,0,0,0)
frame.BackgroundColor3 = Color3.fromRGB(0,0,0)
frame.BorderSizePixel = 0
frame.Parent = screenGui

local loadingText = Instance.new("TextLabel")
loadingText.Size = UDim2.new(0,400,0,50)
loadingText.Position = UDim2.new(0.5,-200,0.35,0)
loadingText.BackgroundTransparency = 1
loadingText.Font = Enum.Font.SourceSansBold
loadingText.TextSize = 36
loadingText.Text = "XModded Premium RGB"
loadingText.TextColor3 = Color3.fromRGB(255,0,0)
loadingText.Parent = frame

local progressBar = Instance.new("Frame")
progressBar.Size = UDim2.new(0,0,0,20)
progressBar.Position = UDim2.new(0.5,-150,0.5,0)
progressBar.BackgroundColor3 = Color3.fromRGB(255,0,0)
progressBar.BorderSizePixel = 0
progressBar.Parent = frame

local timeText = Instance.new("TextLabel")
timeText.Size = UDim2.new(0,300,0,50)
timeText.Position = UDim2.new(0.5,-150,0.45,30)
timeText.BackgroundTransparency = 1
timeText.TextColor3 = Color3.fromRGB(255,255,255)
timeText.Font = Enum.Font.SourceSansBold
timeText.TextScaled = true
timeText.Text = "5:00"
timeText.Parent = frame

local skipButton = Instance.new("TextButton")
skipButton.Size = UDim2.new(0,120,0,50)
skipButton.Position = UDim2.new(0.5,-60,0.55,60)
skipButton.BackgroundColor3 = Color3.fromRGB(0,200,0)
skipButton.TextColor3 = Color3.fromRGB(255,255,255)
skipButton.Text = "SKIP"
skipButton.Font = Enum.Font.SourceSansBold
skipButton.TextScaled = true
skipButton.Parent = frame

local skip = false
skipButton.MouseButton1Click:Connect(function()
    skip = true
end)

-- RGB lento
spawn(function()
    local colors = {Color3.fromRGB(255,0,0), Color3.fromRGB(0,255,0), Color3.fromRGB(0,0,255)}
    local index = 1
    while frame.Parent do
        loadingText.TextColor3 = colors[index]
        progressBar.BackgroundColor3 = colors[index]
        index = index + 1
        if index > #colors then index = 1 end
        wait(0.3)
    end
end)

-- Carregamento de 5 minutos
local totalTime = 300
for i = 0,totalTime do
    if skip then break end
    wait(1)
    local percent = i/totalTime
    progressBar.Size = UDim2.new(percent,0,0,20)
    local remaining = totalTime - i
    local minutes = math.floor(remaining/60)
    local seconds = remaining % 60
    timeText.Text = string.format("%d:%02d", minutes, seconds)
end

frame:Destroy()

-- ==================== TELEGUIADO ====================
local savedPosition = nil
local uiVisible = true

local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "TeleGuiado"
ScreenGui.ResetOnSpawn = false
ScreenGui.Parent = PlayerGui

local Frame = Instance.new("Frame")
Frame.Size = UDim2.new(0, 280, 0, 160)
Frame.Position = UDim2.new(0.5, -140, 0.5, -80)
Frame.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
Frame.BackgroundTransparency = 0.1
Frame.BorderSizePixel = 0
Frame.Active = true
Frame.Draggable = true
Frame.Parent = ScreenGui
Instance.new("UICorner", Frame).CornerRadius = UDim.new(0, 12)

-- Título RGB
local Title = Instance.new("TextLabel")
Title.Parent = Frame
Title.Size = UDim2.new(1, 0, 0, 40)
Title.BackgroundTransparency = 1
Title.Text = "TELEGUIADO BY.GAB"
Title.TextColor3 = Color3.new(1, 1, 1)
Title.TextScaled = true
Title.Font = Enum.Font.GothamBold

-- Botão fechar
local CloseButton = Instance.new("TextButton")
CloseButton.Size = UDim2.new(0, 40, 0, 40)
CloseButton.Position = UDim2.new(1, -45, 0, 5)
CloseButton.Text = "✖"
CloseButton.TextScaled = true
CloseButton.BackgroundColor3 = Color3.fromRGB(200, 50, 50)
CloseButton.TextColor3 = Color3.fromRGB(255, 255, 255)
CloseButton.Font = Enum.Font.GothamBold
CloseButton.Parent = Frame
Instance.new("UICorner", CloseButton).CornerRadius = UDim.new(0, 10)

-- Botões SALVAR POSIÇÃO e TELEPORT
local SaveButton = Instance.new("TextButton")
SaveButton.Parent = Frame
SaveButton.Size = UDim2.new(0.8, 0, 0, 40)
SaveButton.Position = UDim2.new(0.1, 0, 0.45, 0)
SaveButton.Text = "SALVAR POSIÇÃO"
SaveButton.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
SaveButton.TextColor3 = Color3.fromRGB(255, 255, 255)
SaveButton.TextScaled = true
SaveButton.Font = Enum.Font.GothamBold
Instance.new("UICorner", SaveButton).CornerRadius = UDim.new(0, 8)

local TeleportButton = Instance.new("TextButton")
TeleportButton.Parent = Frame
TeleportButton.Size = UDim2.new(0.8, 0, 0, 40)
TeleportButton.Position = UDim2.new(0.1, 0, 0.75, 0)
TeleportButton.Text = "TELEPORT"
TeleportButton.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
TeleportButton.TextColor3 = Color3.fromRGB(255, 255, 255)
TeleportButton.TextScaled = true
TeleportButton.Font = Enum.Font.GothamBold
Instance.new("UICorner", TeleportButton).CornerRadius = UDim.new(0, 8)

local MiniButton = Instance.new("TextButton")
MiniButton.Size = UDim2.new(0, 60, 0, 40)
MiniButton.Position = UDim2.new(0, 20, 1, -60)
MiniButton.Text = "☰"
MiniButton.BackgroundColor3 = Color3.fromRGB(0, 200, 0)
MiniButton.TextColor3 = Color3.fromRGB(255, 255, 255)
MiniButton.TextScaled = true
MiniButton.Font = Enum.Font.GothamBold
MiniButton.Visible = false
MiniButton.Parent = ScreenGui
Instance.new("UICorner", MiniButton).CornerRadius = UDim.new(0, 10)

-- Funções
SaveButton.MouseButton1Click:Connect(function()
	character = player.Character or player.CharacterAdded:Wait()
	humanoidRoot = character:WaitForChild("HumanoidRootPart")
	savedPosition = humanoidRoot.Position
	SaveButton.Text = "POSIÇÃO SALVA ✅"
	task.wait(1)
	SaveButton.Text = "SALVAR POSIÇÃO"
end)

TeleportButton.MouseButton1Click:Connect(function()
	if not savedPosition then
		TeleportButton.Text = "NENHUMA POSIÇÃO"
		task.wait(1)
		TeleportButton.Text = "TELEPORT"
		return
	end
	character = player.Character or player.CharacterAdded:Wait()
	humanoidRoot = character:WaitForChild("HumanoidRootPart")
	local tween = TweenService:Create(
		humanoidRoot,
		TweenInfo.new(0.5, Enum.EasingStyle.Linear, Enum.EasingDirection.Out),
		{CFrame = CFrame.new(savedPosition + Vector3.new(0, 5, 0))}
	)
	tween:Play()
end)

-- RGB lento no título
task.spawn(function()
	while task.wait(0.05) do
		local t = tick() * 2
		local r = math.sin(t) * 0.5 + 0.5
		local g = math.sin(t + 2) * 0.5 + 0.5
		local b = math.sin(t + 4) * 0.5 + 0.5
		Title.TextColor3 = Color3.new(r, g, b)
	end
end)

-- Fechar e reabrir interface
CloseButton.MouseButton1Click:Connect(function()
	uiVisible = false
	Frame.Visible = false
	MiniButton.Visible = true
end)

MiniButton.MouseButton1Click:Connect(function()
	uiVisible = true
	MiniButton.Visible = false
	Frame.Visible = true
end)
