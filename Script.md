------------------------------------------------
-- SERVICES
------------------------------------------------

local Players = game:GetService("Players")
local UIS = game:GetService("UserInputService")
local RunService = game:GetService("RunService")

local player = Players.LocalPlayer
local PlayerGui = player:WaitForChild("PlayerGui")

------------------------------------------------
-- VARIABLES
------------------------------------------------

local infiniteJump = false
local walkSpeed = 16
local autoWin = false
local detecting = false
local greenWinPart = nil

------------------------------------------------
-- GUI
------------------------------------------------

local gui = Instance.new("ScreenGui")
gui.Name = "BannersHub"
gui.ResetOnSpawn = false
gui.Parent = PlayerGui

------------------------------------------------
-- MAIN FRAME
------------------------------------------------

local frame = Instance.new("Frame")
frame.Size = UDim2.new(0,330,0,260)
frame.Position = UDim2.new(0.5,-165,0.5,-130)
frame.BackgroundColor3 = Color3.fromRGB(30,30,30)
frame.BorderSizePixel = 0
frame.Parent = gui
Instance.new("UICorner",frame)

------------------------------------------------
-- TITLE
------------------------------------------------

local title = Instance.new("TextLabel")
title.Size = UDim2.new(1,0,0,35)
title.BackgroundColor3 = Color3.fromRGB(20,20,20)
title.Text = "Banner's Hub"
title.TextColor3 = Color3.new(1,1,1)
title.TextScaled = true
title.Parent = frame
Instance.new("UICorner",title)

------------------------------------------------
-- CLOSE
------------------------------------------------

local close = Instance.new("TextButton")
close.Size = UDim2.new(0,30,0,30)
close.Position = UDim2.new(1,-35,0,3)
close.Text = "X"
close.TextScaled = true
close.BackgroundColor3 = Color3.fromRGB(200,60,60)
close.TextColor3 = Color3.new(1,1,1)
close.Parent = frame
Instance.new("UICorner",close)

------------------------------------------------
-- MINI UI
------------------------------------------------

local mini = Instance.new("ImageButton")
mini.Size = UDim2.new(0,60,0,60)
mini.Position = UDim2.new(0,20,0.5,-30)
mini.Image = "rbxassetid://7072718362"
mini.BackgroundColor3 = Color3.fromRGB(40,40,40)
mini.Visible = false
mini.Parent = gui
Instance.new("UICorner",mini)

close.MouseButton1Click:Connect(function()
	frame.Visible = false
	mini.Visible = true
end)

mini.MouseButton1Click:Connect(function()
	frame.Visible = true
	mini.Visible = false
end)

------------------------------------------------
-- DRAG SYSTEM
------------------------------------------------

local function makeDraggable(obj)

	local dragging = false
	local dragStart
	local startPos

	obj.InputBegan:Connect(function(input)

		if input.UserInputType == Enum.UserInputType.MouseButton1 then

			dragging = true
			dragStart = input.Position
			startPos = frame.Position

			input.Changed:Connect(function()
				if input.UserInputState == Enum.UserInputState.End then
					dragging = false
				end
			end)

		end

	end)

	UIS.InputChanged:Connect(function(input)

		if dragging and input.UserInputType == Enum.UserInputType.MouseMovement then

			local delta = input.Position - dragStart

			frame.Position = UDim2.new(
				startPos.X.Scale,
				startPos.X.Offset + delta.X,
				startPos.Y.Scale,
				startPos.Y.Offset + delta.Y
			)

		end

	end)

end

makeDraggable(frame)
makeDraggable(title)
makeDraggable(mini)

------------------------------------------------
-- TAB BAR
------------------------------------------------

local tabBar = Instance.new("Frame")
tabBar.Size = UDim2.new(1,0,0,30)
tabBar.Position = UDim2.new(0,0,0,35)
tabBar.BackgroundColor3 = Color3.fromRGB(25,25,25)
tabBar.Parent = frame

local mainTab = Instance.new("TextButton")
mainTab.Size = UDim2.new(0.5,0,1,0)
mainTab.Text = "Main"
mainTab.TextScaled = true
mainTab.BackgroundColor3 = Color3.fromRGB(50,50,50)
mainTab.TextColor3 = Color3.new(1,1,1)
mainTab.Parent = tabBar

local discordTab = Instance.new("TextButton")
discordTab.Size = UDim2.new(0.5,0,1,0)
discordTab.Position = UDim2.new(0.5,0,0,0)
discordTab.Text = "Discord"
discordTab.TextScaled = true
discordTab.BackgroundColor3 = Color3.fromRGB(50,50,50)
discordTab.TextColor3 = Color3.new(1,1,1)
discordTab.Parent = tabBar

------------------------------------------------
-- PAGES
------------------------------------------------

local mainPage = Instance.new("Frame")
mainPage.Size = UDim2.new(1,0,1,-65)
mainPage.Position = UDim2.new(0,0,0,65)
mainPage.BackgroundTransparency = 1
mainPage.Parent = frame

local discordPage = Instance.new("Frame")
discordPage.Size = UDim2.new(1,0,1,-65)
discordPage.Position = UDim2.new(0,0,0,65)
discordPage.BackgroundTransparency = 1
discordPage.Visible = false
discordPage.Parent = frame

mainTab.MouseButton1Click:Connect(function()
	mainPage.Visible = true
	discordPage.Visible = false
end)

discordTab.MouseButton1Click:Connect(function()
	mainPage.Visible = false
	discordPage.Visible = true
end)

------------------------------------------------
-- BUTTON CREATOR
------------------------------------------------

local function createButton(text,y)

	local b = Instance.new("TextButton")
	b.Size = UDim2.new(1,-20,0,40)
	b.Position = UDim2.new(0,10,0,y)
	b.Text = text
	b.TextScaled = true
	b.BackgroundColor3 = Color3.fromRGB(60,60,60)
	b.TextColor3 = Color3.new(1,1,1)
	b.Parent = mainPage
	Instance.new("UICorner",b)

	return b

end

------------------------------------------------
-- AUTO WIN
------------------------------------------------

local autoBtn = createButton("Auto Win OFF",10)

autoBtn.MouseButton1Click:Connect(function()

	autoWin = not autoWin
	autoBtn.Text = autoWin and "Auto Win ON" or "Auto Win OFF"

end)

------------------------------------------------
-- INFINITE JUMP
------------------------------------------------

local jumpBtn = createButton("Infinite Jump OFF",60)

jumpBtn.MouseButton1Click:Connect(function()

	infiniteJump = not infiniteJump
	jumpBtn.Text = infiniteJump and "Infinite Jump ON" or "Infinite Jump OFF"

end)

------------------------------------------------
-- SPEED BOX
------------------------------------------------

local speedBox = Instance.new("TextBox")
speedBox.Size = UDim2.new(1,-20,0,40)
speedBox.Position = UDim2.new(0,10,0,110)
speedBox.PlaceholderText = "Set your speed"
speedBox.TextScaled = true
speedBox.BackgroundColor3 = Color3.fromRGB(60,60,60)
speedBox.TextColor3 = Color3.new(1,1,1)
speedBox.Parent = mainPage
Instance.new("UICorner",speedBox)

speedBox.FocusLost:Connect(function()

	local n = tonumber(speedBox.Text)
	if n then
		walkSpeed = n
	end

end)

------------------------------------------------
-- APPLY SPEED
------------------------------------------------

RunService.RenderStepped:Connect(function()

	local char = player.Character
	if char then
		local hum = char:FindFirstChildOfClass("Humanoid")
		if hum then
			hum.WalkSpeed = walkSpeed
		end
	end

end)

------------------------------------------------
-- INFINITE JUMP
------------------------------------------------

UIS.JumpRequest:Connect(function()

	if infiniteJump then
		local hum = player.Character and player.Character:FindFirstChildOfClass("Humanoid")
		if hum then
			hum:ChangeState(Enum.HumanoidStateType.Jumping)
		end
	end

end)

------------------------------------------------
-- COUNTDOWN UI
------------------------------------------------

local countdown = Instance.new("TextLabel")
countdown.Size = UDim2.new(0,220,0,60)
countdown.Position = UDim2.new(0.5,-110,0.25,0)
countdown.BackgroundColor3 = Color3.fromRGB(0,0,0)
countdown.TextColor3 = Color3.new(1,1,1)
countdown.TextScaled = true
countdown.Visible = false
countdown.Parent = gui
Instance.new("UICorner",countdown)

------------------------------------------------
-- FIND GREEN PART
------------------------------------------------

task.spawn(function()

	while task.wait(2) do

		local farthest=nil
		local maxDist=0

		if player.Character and player.Character:FindFirstChild("HumanoidRootPart") then

			local root = player.Character.HumanoidRootPart.Position

			for _,v in pairs(workspace:GetDescendants()) do

				if v:IsA("BasePart") then

					local c = v.Color

					if c.G > 0.8 and c.R < 0.35 and c.B < 0.35 then

						local dist = (v.Position-root).Magnitude

						if dist > maxDist then
							maxDist = dist
							farthest = v
						end

					end

				end

			end

		end

		greenWinPart = farthest

	end

end)

------------------------------------------------
-- TELEPORT (10 BLOCKS BACK)
------------------------------------------------

local function teleport()

	if greenWinPart and player.Character and player.Character:FindFirstChild("HumanoidRootPart") then

		local root = player.Character.HumanoidRootPart

		local backPosition = greenWinPart.Position - (greenWinPart.CFrame.LookVector * 10)

		root.CFrame = CFrame.new(backPosition + Vector3.new(0,5,0))

	end

end

------------------------------------------------
-- TIMER DETECT
------------------------------------------------

task.spawn(function()

	while task.wait(0.3) do

		if autoWin and not detecting then

			for _,v in pairs(player.PlayerGui:GetDescendants()) do

				if v:IsA("TextLabel") and v.Text == "1:59" then

					detecting = true
					countdown.Visible = true

					for i = 7,1,-1 do
						countdown.Text = "Teleport in "..i
						task.wait(1)
					end

					countdown.Visible = false
					teleport()

					repeat task.wait() until v.Text ~= "1:59"

					detecting = false

				end

			end

		end

	end

end)

------------------------------------------------
-- DISCORD PAGE
------------------------------------------------

local discordText = Instance.new("TextLabel")
discordText.Size = UDim2.new(1,-20,0,120)
discordText.Position = UDim2.new(0,10,0,20)
discordText.BackgroundTransparency = 1
discordText.TextColor3 = Color3.new(1,1,1)
discordText.TextScaled = true
discordText.TextWrapped = true
discordText.Text = "Join our Discord server to support us! https://discord.gg/UtmYPJPfPm"
discordText.Parent = discordPage
