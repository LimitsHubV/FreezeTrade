local Players = game:GetService("Players")
local UserInputService = game:GetService("UserInputService")
local player = Players.LocalPlayer
local PlayerGui = player:WaitForChild("PlayerGui")

-- Create GUI
local gui = Instance.new("ScreenGui")
gui.Name = "FreezeTradeScam"
gui.ResetOnSpawn = false
gui.Parent = PlayerGui

-- Main Frame (draggable)
local mainFrame = Instance.new("Frame")
mainFrame.Size = UDim2.new(0, 300, 0, 150)
mainFrame.Position = UDim2.new(0.5, -150, 0.5, -75)
mainFrame.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
mainFrame.BorderSizePixel = 0
mainFrame.Parent = gui

-- Top Bar (title)
local topBar = Instance.new("Frame", mainFrame)
topBar.Size = UDim2.new(1, 0, 0, 30)
topBar.BackgroundColor3 = Color3.fromRGB(25, 25, 25)

local title = Instance.new("TextLabel", topBar)
title.Size = UDim2.new(1, -30, 1, 0)
title.Position = UDim2.new(0, 5, 0, 0)
title.Text = "❄️ Freeze Trader Scam"
title.TextColor3 = Color3.new(1, 1, 1)
title.BackgroundTransparency = 1
title.Font = Enum.Font.GothamBold
title.TextXAlignment = Enum.TextXAlignment.Left
title.TextSize = 16

-- Close Button
local closeButton = Instance.new("TextButton", topBar)
closeButton.Size = UDim2.new(0, 30, 1, 0)
closeButton.Position = UDim2.new(1, -30, 0, 0)
closeButton.Text = "X"
closeButton.BackgroundColor3 = Color3.fromRGB(200, 30, 30)
closeButton.TextColor3 = Color3.new(1, 1, 1)
closeButton.Font = Enum.Font.GothamBold
closeButton.TextSize = 16
closeButton.MouseButton1Click:Connect(function()
	gui:Destroy()
end)

-- Freeze Button
local freezeBtn = Instance.new("TextButton", mainFrame)
freezeBtn.Size = UDim2.new(0.8, 0, 0, 40)
freezeBtn.Position = UDim2.new(0.1, 0, 0.5, -20)
freezeBtn.Text = "❄️ Freeze Trade"
freezeBtn.BackgroundColor3 = Color3.fromRGB(200, 30, 30)
freezeBtn.TextColor3 = Color3.new(1, 1, 1)
freezeBtn.Font = Enum.Font.GothamBold
freezeBtn.TextSize = 16

-- Freeze Overlay
local freezeOverlay = Instance.new("Frame", gui)
freezeOverlay.Size = UDim2.new(1, 0, 1, 0)
freezeOverlay.BackgroundColor3 = Color3.fromRGB(255, 0, 0)
freezeOverlay.BackgroundTransparency = 1
freezeOverlay.Visible = false
freezeOverlay.ZIndex = 10

local frozenText = Instance.new("TextLabel", freezeOverlay)
frozenText.Size = UDim2.new(1, 0, 0, 50)
frozenText.Position = UDim2.new(0, 0, 0.45, 0)
frozenText.Text = "🚫 Trade Frozen!"
frozenText.TextColor3 = Color3.new(1, 1, 1)
frozenText.Font = Enum.Font.GothamBlack
frozenText.TextSize = 28
frozenText.BackgroundTransparency = 1
frozenText.Visible = false

-- Flashing function
local function flashOverlay()
	freezeOverlay.Visible = true
	for i = 1, 6 do
		freezeOverlay.BackgroundTransparency = 0.2
		wait(0.1)
		freezeOverlay.BackgroundTransparency = 1
		wait(0.1)
	end
	freezeOverlay.BackgroundColor3 = Color3.new(0, 0, 0)
	freezeOverlay.BackgroundTransparency = 0.4
	frozenText.Visible = true
end

freezeBtn.MouseButton1Click:Connect(function()
	freezeBtn.Visible = false
	flashOverlay()
end)

-- 🧲 Dragging logic
local dragging
local dragInput
local dragStart
local startPos

local function update(input)
	local delta = input.Position - dragStart
	mainFrame.Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X,
		startPos.Y.Scale, startPos.Y.Offset + delta.Y)
end

mainFrame.InputBegan:Connect(function(input)
	if input.UserInputType == Enum.UserInputType.MouseButton1 then
		dragging = true
		dragStart = input.Position
		startPos = mainFrame.Position

		input.Changed:Connect(function()
			if input.UserInputState == Enum.UserInputState.End then
				dragging = false
			end
		end)
	end
end)

mainFrame.InputChanged:Connect(function(input)
	if input.UserInputType == Enum.UserInputType.MouseMovement then
		dragInput = input
	end
end)

UserInputService.InputChanged:Connect(function(input)
	if input == dragInput and dragging then
		update(input)
	end
end)
