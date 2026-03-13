------------------------------------------------
-- KEY SYSTEM
------------------------------------------------

local correctKey = "Slapbattlesnewscript5772984901"
local keyAccepted = false

local Players = game:GetService("Players")
local player = Players.LocalPlayer
local PlayerGui = player:WaitForChild("PlayerGui")

local KeyGui = Instance.new("ScreenGui", PlayerGui)
KeyGui.Name = "KeySystem"

local KeyFrame = Instance.new("Frame", KeyGui)
KeyFrame.Size = UDim2.new(0,300,0,180)
KeyFrame.Position = UDim2.new(0.5,-150,0.5,-90)
KeyFrame.BackgroundColor3 = Color3.fromRGB(30,30,30)

local KeyTitle = Instance.new("TextLabel", KeyFrame)
KeyTitle.Size = UDim2.new(1,0,0,40)
KeyTitle.BackgroundTransparency = 1
KeyTitle.Text = "Enter Script Key"
KeyTitle.TextScaled = true
KeyTitle.TextColor3 = Color3.fromRGB(255,255,255)

local KeyBox = Instance.new("TextBox", KeyFrame)
KeyBox.Size = UDim2.new(0.8,0,0,40)
KeyBox.Position = UDim2.new(0.1,0,0.35,0)
KeyBox.PlaceholderText = "Enter Key Here"

local Submit = Instance.new("TextButton", KeyFrame)
Submit.Size = UDim2.new(0.8,0,0,30)
Submit.Position = UDim2.new(0.1,0,0.6,0)
Submit.Text = "Submit"

-- COPY LINK BUTTON
local GetKey = Instance.new("TextButton", KeyFrame)
GetKey.Size = UDim2.new(0.8,0,0,30)
GetKey.Position = UDim2.new(0.1,0,0.8,0)
GetKey.Text = "Get Key Link"

GetKey.MouseButton1Click:Connect(function()
	if setclipboard then
		setclipboard("https://work.ink/2n0B/banners-hub")
		GetKey.Text = "Copied!"
	else
		GetKey.Text = "Clipboard not supported"
	end
end)

Submit.MouseButton1Click:Connect(function()
	if KeyBox.Text == correctKey then
		keyAccepted = true
		KeyGui:Destroy()
	else
		KeyBox.Text = "Wrong Key!"
	end
end)

repeat task.wait() until keyAccepted


------------------------------------------------
-- Banner's Hub / SLAP BATTLES SCRIPT
------------------------------------------------

local UIS = game:GetService("UserInputService")
local RunService = game:GetService("RunService")

local PlayerGui = player:WaitForChild("PlayerGui")

-- VARIABLES
local infiniteJump = false
local walkSpeed = 16
local autoWin = false
local detecting = false
local greenWinPart = nil

-- GUI
local ScreenGui = Instance.new("ScreenGui", PlayerGui)
ScreenGui.Name = "BannersHub"

local MainFrame = Instance.new("Frame", ScreenGui)
MainFrame.Size = UDim2.new(0, 300, 0, 400)
MainFrame.Position = UDim2.new(0.5, -150, 0.5, -200)
MainFrame.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
MainFrame.BorderSizePixel = 0
MainFrame.Visible = true

-- Title
local Title = Instance.new("TextLabel", MainFrame)
Title.Size = UDim2.new(1, 0, 0, 50)
Title.BackgroundTransparency = 1
Title.Text = "Banner's Hub"
Title.TextScaled = true
Title.TextColor3 = Color3.fromRGB(255, 255, 255)

-- Infinite Jump Button
local IJButton = Instance.new("TextButton", MainFrame)
IJButton.Size = UDim2.new(0.8, 0, 0, 40)
IJButton.Position = UDim2.new(0.1, 0, 0.2, 0)
IJButton.Text = "Infinite Jump: OFF"
IJButton.TextColor3 = Color3.fromRGB(255, 255, 255)

IJButton.MouseButton1Click:Connect(function()
    infiniteJump = not infiniteJump
    IJButton.Text = "Infinite Jump: " .. (infiniteJump and "ON" or "OFF")
end)

-- WalkSpeed
local SpeedSlider = Instance.new("TextBox", MainFrame)
SpeedSlider.Size = UDim2.new(0.8, 0, 0, 40)
SpeedSlider.Position = UDim2.new(0.1, 0, 0.35, 0)
SpeedSlider.PlaceholderText = "Set WalkSpeed (default 16)"

SpeedSlider.FocusLost:Connect(function()
    local val = tonumber(SpeedSlider.Text)
    if val then
        walkSpeed = val
        player.Character.Humanoid.WalkSpeed = walkSpeed
    end
end)

-- Auto Win Button
local AWButton = Instance.new("TextButton", MainFrame)
AWButton.Size = UDim2.new(0.8, 0, 0, 40)
AWButton.Position = UDim2.new(0.1, 0, 0.5, 0)
AWButton.Text = "Auto Win: OFF"
AWButton.TextColor3 = Color3.fromRGB(255, 255, 255)

AWButton.MouseButton1Click:Connect(function()
    autoWin = not autoWin
    AWButton.Text = "Auto Win: " .. (autoWin and "ON" or "OFF")
end)

-- Discord Page
local DiscordLabel = Instance.new("TextLabel", MainFrame)
DiscordLabel.Size = UDim2.new(1, 0, 0, 60)
DiscordLabel.Position = UDim2.new(0, 0, 0.75, 0)
DiscordLabel.Text = "Join our Discord server to support us https://discord.gg/UtmYPJPfPm"
DiscordLabel.TextWrapped = true
DiscordLabel.TextScaled = true
DiscordLabel.TextColor3 = Color3.fromRGB(0, 255, 255)
DiscordLabel.BackgroundTransparency = 1

-- FUNCTIONS
UIS.InputBegan:Connect(function(input)
    if input.KeyCode == Enum.KeyCode.Space and infiniteJump then
        local char = player.Character
        if char and char:FindFirstChild("Humanoid") then
            char.Humanoid:ChangeState(Enum.HumanoidStateType.Jumping)
        end
    end
end)

RunService.Heartbeat:Connect(function()
    if autoWin and player.Character then
        local char = player.Character
        if char:FindFirstChild("HumanoidRootPart") then
            for _, part in pairs(workspace:GetChildren()) do
                if part.Name == "GreenWinPart" then
                    char.HumanoidRootPart.CFrame = part.CFrame
                end
            end
        end
    end
end)
