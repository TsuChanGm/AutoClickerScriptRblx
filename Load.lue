-- Services
local uis = game:GetService("UserInputService")
local vim = game:GetService("VirtualInputManager")
local players = game:GetService("Players")
local runService = game:GetService("RunService")
local localPlayer = players.LocalPlayer

-- GUI
local gui = Instance.new("ScreenGui", game.CoreGui)
gui.Name = "AutoClickerUI"

local frame = Instance.new("Frame", gui)
frame.Size = UDim2.new(0, 200, 0, 150)
frame.Position = UDim2.new(0.5, -100, 0.5, -75)
frame.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
frame.Active = true
frame.Draggable = true

local cpsBox = Instance.new("TextBox", frame)
cpsBox.PlaceholderText = "CPS (e.g. 10)"
cpsBox.Size = UDim2.new(1, -20, 0, 30)
cpsBox.Position = UDim2.new(0, 10, 0, 10)
cpsBox.BackgroundColor3 = Color3.fromRGB(70, 70, 70)
cpsBox.TextColor3 = Color3.new(1, 1, 1)
cpsBox.Text = ""

local instructions = Instance.new("TextLabel", frame)
instructions.Text = "Press F6 to toggle"
instructions.Size = UDim2.new(1, -20, 0, 20)
instructions.Position = UDim2.new(0, 10, 0, 45)
instructions.BackgroundTransparency = 1
instructions.TextColor3 = Color3.new(1, 1, 1)
instructions.TextScaled = true

-- Auto Click Logic
local clicking = false
local clickThread

local function clickLoop(cps)
	while clicking do
		local cam = workspace.CurrentCamera
		local screenCenter = cam.ViewportSize / 2

		-- Simulate click at screen center
		vim:SendMouseButtonEvent(screenCenter.X, screenCenter.Y, 0, true, game, 0)
		vim:SendMouseButtonEvent(screenCenter.X, screenCenter.Y, 0, false, game, 0)

		task.wait(1 / cps)
	end
end

-- F6 Toggle
uis.InputBegan:Connect(function(input, processed)
	if processed then return end
	if input.KeyCode == Enum.KeyCode.F6 then
		if not clicking then
			local cps = tonumber(cpsBox.Text)
			if cps and cps > 0 then
				clicking = true
				instructions.Text = "Clicking: ON (F6 to stop)"
				clickThread = task.spawn(function()
					clickLoop(cps)
				end)
			else
				instructions.Text = "Enter valid CPS!"
			end
		else
			clicking = false
			instructions.Text = "Clicking: OFF (F6 to start)"
		end
	end
end)
