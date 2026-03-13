------------------------------------------------
-- SERVICES
------------------------------------------------

local Players = game:GetService("Players")
local UIS = game:GetService("UserInputService")

local player = Players.LocalPlayer
local PlayerGui = player:WaitForChild("PlayerGui")

------------------------------------------------
-- VARIABLES
------------------------------------------------

local infiniteJump = false
local autoTeleport = false
local correctKey = "Slapbattlesnewscript5772984901"

------------------------------------------------
-- KEY SYSTEM
------------------------------------------------

local KeyGui = Instance.new("ScreenGui",PlayerGui)

local KeyFrame = Instance.new("Frame",KeyGui)
KeyFrame.Size = UDim2.new(0,300,0,180)
KeyFrame.Position = UDim2.new(0.5,-150,0.5,-90)
KeyFrame.BackgroundColor3 = Color3.fromRGB(30,30,30)

local Title = Instance.new("TextLabel",KeyFrame)
Title.Size = UDim2.new(1,0,0,40)
Title.BackgroundTransparency = 1
Title.Text = "Enter Key"
Title.TextScaled = true
Title.TextColor3 = Color3.new(1,1,1)

local KeyBox = Instance.new("TextBox",KeyFrame)
KeyBox.Size = UDim2.new(0.8,0,0,35)
KeyBox.Position = UDim2.new(0.1,0,0.35,0)
KeyBox.PlaceholderText = "Enter key"

local Submit = Instance.new("TextButton",KeyFrame)
Submit.Size = UDim2.new(0.8,0,0,30)
Submit.Position = UDim2.new(0.1,0,0.6,0)
Submit.Text = "Submit"

local GetKey = Instance.new("TextButton",KeyFrame)
GetKey.Size = UDim2.new(0.8,0,0,25)
GetKey.Position = UDim2.new(0.1,0,0.8,0)
GetKey.Text = "Get Key"

GetKey.MouseButton1Click:Connect(function()
	if setclipboard then
		setclipboard("https://work.ink/2n0B/banners-hub")
		GetKey.Text = "Copied!"
	end
end)

Submit.MouseButton1Click:Connect(function()

	if KeyBox.Text == correctKey then
		KeyGui:Destroy()
	else
		KeyBox.Text = "Wrong Key!"
	end

end)

repeat task.wait() until not KeyGui.Parent

------------------------------------------------
-- MAIN GUI
------------------------------------------------

local ScreenGui = Instance.new("ScreenGui",PlayerGui)

local Main = Instance.new("Frame",ScreenGui)
Main.Size = UDim2.new(0,300,0,350)
Main.Position = UDim2.new(0.5,-150,0.5,-175)
Main.BackgroundColor3 = Color3.fromRGB(35,35,35)

------------------------------------------------
-- MINI UI
------------------------------------------------

local Mini = Instance.new("TextButton",ScreenGui)
Mini.Size = UDim2.new(0,60,0,60)
Mini.Position = UDim2.new(0,20,0.5,-30)
Mini.Text = "Hub"
Mini.BackgroundColor3 = Color3.fromRGB(255,140,0)
Mini.Visible = false

Mini.MouseButton1Click:Connect(function()

	Main.Visible = true
	Mini.Visible = false

end)

------------------------------------------------
-- CLOSE BUTTON
------------------------------------------------

local Close = Instance.new("TextButton",Main)
Close.Size = UDim2.new(0,30,0,30)
Close.Position = UDim2.new(1,-35,0,5)
Close.Text = "X"

Close.MouseButton1Click:Connect(function()

	Main.Visible = false
	Mini.Visible = true

end)

------------------------------------------------
-- TITLE
------------------------------------------------

local HubTitle = Instance.new("TextLabel",Main)
HubTitle.Size = UDim2.new(1,0,0,40)
HubTitle.BackgroundTransparency = 1
HubTitle.Text = "Banner's Hub"
HubTitle.TextScaled = true
HubTitle.TextColor3 = Color3.new(1,1,1)

------------------------------------------------
-- INFINITE JUMP
------------------------------------------------

local IJ = Instance.new("TextButton",Main)
IJ.Size = UDim2.new(0.8,0,0,40)
IJ.Position = UDim2.new(0.1,0,0.2,0)
IJ.Text = "Infinite Jump: OFF"

IJ.MouseButton1Click:Connect(function()

	infiniteJump = not infiniteJump
	IJ.Text = "Infinite Jump: "..(infiniteJump and "ON" or "OFF")

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

local SpeedBox = Instance.new("TextBox",Main)
SpeedBox.Size = UDim2.new(0.8,0,0,40)
SpeedBox.Position = UDim2.new(0.1,0,0.4,0)
SpeedBox.PlaceholderText = "Set Speed"

SpeedBox.FocusLost:Connect(function()

	local num = tonumber(SpeedBox.Text)

	if num and player.Character then
		player.Character:FindFirstChildOfClass("Humanoid").WalkSpeed = num
	end

end)

------------------------------------------------
-- AUTO TELEPORT
------------------------------------------------

local TP = Instance.new("TextButton",Main)
TP.Size = UDim2.new(0.8,0,0,40)
TP.Position = UDim2.new(0.1,0,0.6,0)
TP.Text = "Auto Win: OFF"

TP.MouseButton1Click:Connect(function()

	autoTeleport = not autoTeleport
	TP.Text = "Auto Win: "..(autoTeleport and "ON" or "OFF")

end)

------------------------------------------------
-- DISCORD
------------------------------------------------

local Discord = Instance.new("TextLabel",Main)
Discord.Size = UDim2.new(1,0,0,60)
Discord.Position = UDim2.new(0,0,0.8,0)
Discord.BackgroundTransparency = 1
Discord.TextWrapped = true
Discord.TextScaled = true
Discord.Text = "Join our Discord server to support us https://discord.gg/UtmYPJPfPm"
Discord.TextColor3 = Color3.fromRGB(0,255,0)

------------------------------------------------
-- COUNTDOWN UI
------------------------------------------------

local Countdown = Instance.new("TextLabel",ScreenGui)
Countdown.Size = UDim2.new(0,200,0,50)
Countdown.Position = UDim2.new(0.5,-100,0.1,0)
Countdown.BackgroundColor3 = Color3.fromRGB(0,0,0)
Countdown.TextColor3 = Color3.new(1,1,1)
Countdown.TextScaled = true
Countdown.Visible = false

------------------------------------------------
-- FIND FARTHEST GREEN
------------------------------------------------

local function getFarthestGreen()

	local char = player.Character
	if not char then return end

	local root = char:FindFirstChild("HumanoidRootPart")
	if not root then return end

	local farthest
	local dist = 0

	for _,v in pairs(workspace:GetDescendants()) do

		if v:IsA("BasePart") then

			local c = v.Color

			if c.G > 0.8 and c.R < 0.2 and c.B < 0.2 then

				local d = (v.Position-root.Position).Magnitude

				if d > dist then
					dist = d
					farthest = v
				end

			end

		end

	end

	return farthest

end

------------------------------------------------
-- TIMER DETECTION
------------------------------------------------

local function timerIs159()

	for _,v in pairs(game:GetDescendants()) do

		if v:IsA("TextLabel") or v:IsA("TextBox") then

			if tostring(v.Text) == "1:59" then
				return true
			end

		end

	end

	return false

end

------------------------------------------------
-- AUTO TELEPORT SYSTEM
------------------------------------------------

task.spawn(function()

	local triggered = false

	while true do

		task.wait(0.5)

		if autoTeleport then

			local detected = timerIs159()

			if detected and not triggered then

				triggered = true

				Countdown.Visible = true

				for i = 7,0,-1 do
					Countdown.Text = "Teleport in "..i
					task.wait(1)
				end

				local part = getFarthestGreen()

				if part and player.Character then

					local root = player.Character:FindFirstChild("HumanoidRootPart")

					if root then
						root.CFrame = part.CFrame * CFrame.new(0,0,10)
					end

				end

				Countdown.Visible = false

			end

			if not detected then
				triggered = false
			end

		end

	end

end)
