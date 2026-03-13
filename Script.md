------------------------------------------------
-- KEY SYSTEM
------------------------------------------------

local correctKey = "Slapbattlesnewscript5772984901"
local keyAccepted = false

local Players = game:GetService("Players")
local UIS = game:GetService("UserInputService")
local RunService = game:GetService("RunService")

local player = Players.LocalPlayer
local PlayerGui = player:WaitForChild("PlayerGui")

local KeyGui = Instance.new("ScreenGui", PlayerGui)
KeyGui.Name = "KeySystem"

local KeyFrame = Instance.new("Frame", KeyGui)
KeyFrame.Size = UDim2.new(0,300,0,180)
KeyFrame.Position = UDim2.new(0.5,-150,0.5,-90)
KeyFrame.BackgroundColor3 = Color3.fromRGB(30,30,30)

local Title = Instance.new("TextLabel", KeyFrame)
Title.Size = UDim2.new(1,0,0,40)
Title.BackgroundTransparency = 1
Title.Text = "Enter Script Key"
Title.TextScaled = true
Title.TextColor3 = Color3.new(1,1,1)

local KeyBox = Instance.new("TextBox", KeyFrame)
KeyBox.Size = UDim2.new(0.8,0,0,40)
KeyBox.Position = UDim2.new(0.1,0,0.35,0)
KeyBox.PlaceholderText = "Enter Key"

local Submit = Instance.new("TextButton", KeyFrame)
Submit.Size = UDim2.new(0.8,0,0,30)
Submit.Position = UDim2.new(0.1,0,0.6,0)
Submit.Text = "Submit"

local GetKey = Instance.new("TextButton", KeyFrame)
GetKey.Size = UDim2.new(0.8,0,0,30)
GetKey.Position = UDim2.new(0.1,0,0.8,0)
GetKey.Text = "Get Key Link"

GetKey.MouseButton1Click:Connect(function()
	if setclipboard then
		setclipboard("https://work.ink/2n0B/banners-hub")
		GetKey.Text = "Copied!"
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
-- VARIABLES
------------------------------------------------

local infiniteJump = false
local walkSpeed = 16

------------------------------------------------
-- MAIN GUI
------------------------------------------------

local ScreenGui = Instance.new("ScreenGui", PlayerGui)
ScreenGui.Name = "BannersHub"

local MainFrame = Instance.new("Frame", ScreenGui)
MainFrame.Size = UDim2.new(0,300,0,350)
MainFrame.Position = UDim2.new(0.5,-150,0.5,-175)
MainFrame.BackgroundColor3 = Color3.fromRGB(30,30,30)

------------------------------------------------
-- MINI UI
------------------------------------------------

local MiniButton = Instance.new("TextButton", ScreenGui)
MiniButton.Size = UDim2.new(0,60,0,60)
MiniButton.Position = UDim2.new(0,20,0.5,-30)
MiniButton.BackgroundColor3 = Color3.fromRGB(255,140,0)
MiniButton.Text = "Hub"
MiniButton.TextScaled = true
MiniButton.Visible = false

MiniButton.MouseButton1Click:Connect(function()
	MainFrame.Visible = true
	MiniButton.Visible = false
end)

------------------------------------------------
-- CLOSE BUTTON
------------------------------------------------

local Close = Instance.new("TextButton", MainFrame)
Close.Size = UDim2.new(0,30,0,30)
Close.Position = UDim2.new(1,-35,0,5)
Close.Text = "X"
Close.BackgroundColor3 = Color3.fromRGB(200,60,60)

Close.MouseButton1Click:Connect(function()
	MainFrame.Visible = false
	MiniButton.Visible = true
end)

------------------------------------------------
-- TITLE
------------------------------------------------

local Title2 = Instance.new("TextLabel", MainFrame)
Title2.Size = UDim2.new(1,0,0,40)
Title2.BackgroundTransparency = 1
Title2.Text = "Banner's Hub"
Title2.TextScaled = true
Title2.TextColor3 = Color3.new(1,1,1)

------------------------------------------------
-- INFINITE JUMP
------------------------------------------------

local IJButton = Instance.new("TextButton", MainFrame)
IJButton.Size = UDim2.new(0.8,0,0,40)
IJButton.Position = UDim2.new(0.1,0,0.2,0)
IJButton.Text = "Infinite Jump: OFF"

IJButton.MouseButton1Click:Connect(function()
	infiniteJump = not infiniteJump
	IJButton.Text = "Infinite Jump: "..(infiniteJump and "ON" or "OFF")
end)

UIS.JumpRequest:Connect(function()
	if infiniteJump then
		local char = player.Character
		if char and char:FindFirstChildOfClass("Humanoid") then
			char:FindFirstChildOfClass("Humanoid"):ChangeState("Jumping")
		end
	end
end)

------------------------------------------------
-- SPEED
------------------------------------------------

local SpeedBox = Instance.new("TextBox", MainFrame)
SpeedBox.Size = UDim2.new(0.8,0,0,40)
SpeedBox.Position = UDim2.new(0.1,0,0.35,0)
SpeedBox.PlaceholderText = "Set Speed"

SpeedBox.FocusLost:Connect(function()
	local num = tonumber(SpeedBox.Text)
	if num and player.Character then
		player.Character:FindFirstChildOfClass("Humanoid").WalkSpeed = num
	end
end)

------------------------------------------------
-- TELEPORT
------------------------------------------------

local TPButton = Instance.new("TextButton", MainFrame)
TPButton.Size = UDim2.new(0.8,0,0,40)
TPButton.Position = UDim2.new(0.1,0,0.5,0)
TPButton.Text = "Teleport to Win"

TPButton.MouseButton1Click:Connect(function()
	if player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
		for _,v in pairs(workspace:GetDescendants()) do
			if v.Name == "GreenWinPart" then
				player.Character.HumanoidRootPart.CFrame = v.CFrame
			end
		end
	end
end)

------------------------------------------------
-- DISCORD PAGE
------------------------------------------------

local Discord = Instance.new("TextLabel", MainFrame)
Discord.Size = UDim2.new(1,0,0,60)
Discord.Position = UDim2.new(0,0,0.75,0)
Discord.BackgroundTransparency = 1
Discord.TextWrapped = true
Discord.TextScaled = true
Discord.Text = "Join pur Discord server to support us https://discord.gg/UtmYPJPfPm"
Discord.TextColor3 = Color3.fromRGB(0,255,255)
