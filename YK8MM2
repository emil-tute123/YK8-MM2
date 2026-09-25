local player = game.Players.LocalPlayer
local playerGui = player:WaitForChild("PlayerGui")

local screenGui = Instance.new("ScreenGui")
screenGui.Name = "MM2FarmGUI"
screenGui.ResetOnSpawn = false
screenGui.ZIndexBehavior = Enum.ZIndexBehavior.Global
screenGui.Parent = playerGui

local isFarming = false
local farmingConnection = nil
local isMinimized = false
local dragging = false
local dragStart, startPos
local scriptStartedAt = os.clock()

local mainFrame = Instance.new("Frame")
mainFrame.Name = "MainFrame"
mainFrame.Size = UDim2.new(0, 390, 0, 330)
mainFrame.Position = UDim2.new(0.5, -195, 0.5, -165)
mainFrame.BackgroundColor3 = Color3.fromRGB(74, 12, 22)
mainFrame.BackgroundTransparency = 0.48
mainFrame.BorderSizePixel = 0
mainFrame.ZIndex = 2
mainFrame.ClipsDescendants = true
mainFrame.Parent = screenGui

local menuBackground = Instance.new("ImageLabel")
menuBackground.Name = "MenuBackground"
menuBackground.Size = UDim2.fromScale(1, 1)
menuBackground.Position = UDim2.fromScale(0, 0)
menuBackground.BackgroundColor3 = Color3.fromRGB(12, 15, 18)
menuBackground.BackgroundTransparency = 0
menuBackground.BorderSizePixel = 0
menuBackground.Image = "rbxassetid://129472393964753"
menuBackground.ImageTransparency = 0.18
menuBackground.ScaleType = Enum.ScaleType.Crop
menuBackground.ZIndex = 0
menuBackground.Parent = mainFrame

local menuBackgroundCorner = Instance.new("UICorner")
menuBackgroundCorner.CornerRadius = UDim.new(0, 16)
menuBackgroundCorner.Parent = menuBackground

local menuShade = Instance.new("Frame")
menuShade.Name = "MenuShade"
menuShade.Size = UDim2.fromScale(1, 1)
menuShade.BackgroundColor3 = Color3.fromRGB(65, 8, 18)
menuShade.BackgroundTransparency = 0.64
menuShade.BorderSizePixel = 0
menuShade.ZIndex = 0
menuShade.Parent = mainFrame

local menuShadeCorner = Instance.new("UICorner")
menuShadeCorner.CornerRadius = UDim.new(0, 16)
menuShadeCorner.Parent = menuShade

local uiCorner = Instance.new("UICorner")
uiCorner.CornerRadius = UDim.new(0, 16)
uiCorner.Parent = mainFrame

local frameStroke = Instance.new("UIStroke")
frameStroke.Color = Color3.fromRGB(255, 225, 225)
frameStroke.Thickness = 2
frameStroke.Transparency = 0.08
frameStroke.Parent = mainFrame

local glow = Instance.new("Frame")
glow.Size = UDim2.new(1.03, 0, 1.03, 0)
glow.Position = UDim2.new(-0.015, 0, -0.015, 0)
glow.BackgroundColor3 = Color3.fromRGB(255, 55, 85)
glow.BackgroundTransparency = 0.93
glow.BorderSizePixel = 0
glow.Parent = mainFrame

local glowCorner = Instance.new("UICorner")
glowCorner.CornerRadius = UDim.new(0, 18)
glowCorner.Parent = glow

local topBar = Instance.new("Frame")
topBar.Size = UDim2.new(1, 0, 0, 64)
topBar.BackgroundColor3 = Color3.fromRGB(95, 14, 29)
topBar.BackgroundTransparency = 1
topBar.BorderSizePixel = 0
topBar.ZIndex = 3
topBar.Parent = mainFrame

local topCorner = Instance.new("UICorner")
topCorner.CornerRadius = UDim.new(0, 16)
topCorner.Parent = topBar

local gradient = Instance.new("UIGradient")
gradient.Color = ColorSequence.new({
    ColorSequenceKeypoint.new(0, Color3.fromRGB(31, 103, 205)),
    ColorSequenceKeypoint.new(0.5, Color3.fromRGB(24, 64, 139)),
    ColorSequenceKeypoint.new(1, Color3.fromRGB(153, 31, 67))
})
gradient.Parent = topBar
gradient.Transparency = NumberSequence.new(1)

local umbrella = Instance.new("ImageLabel")
umbrella.Size = UDim2.new(0, 36, 0, 36)
umbrella.Position = UDim2.new(0, 16, 0.5, -18)
umbrella.BackgroundTransparency = 1
umbrella.Image = "rbxassetid:6031097223"
umbrella.Parent = topBar

local title = Instance.new("TextLabel")
title.Size = UDim2.new(0.55, 0, 0, 36)
title.Position = UDim2.new(0, 62, 0, 5)
title.BackgroundTransparency = 1
title.Text = "YK8"
title.TextColor3 = Color3.fromRGB(255, 255, 255)
title.TextScaled = true
title.Font = Enum.Font.PermanentMarker
title.TextStrokeColor3 = Color3.fromRGB(4, 13, 32)
title.TextStrokeTransparency = 0.15
title.ZIndex = 5
title.TextXAlignment = Enum.TextXAlignment.Left
title.Parent = topBar

local subtitle = Instance.new("TextLabel")
subtitle.Size = UDim2.new(0.6, 0, 0, 16)
subtitle.Position = UDim2.new(0, 64, 0, 34)
subtitle.BackgroundTransparency = 1
subtitle.Text = ""
subtitle.TextColor3 = Color3.fromRGB(255, 215, 215)
subtitle.TextSize = 10
subtitle.Font = Enum.Font.GothamBold
subtitle.TextStrokeColor3 = Color3.fromRGB(4, 13, 32)
subtitle.TextStrokeTransparency = 0.35
subtitle.ZIndex = 5
subtitle.Visible = false
subtitle.TextXAlignment = Enum.TextXAlignment.Left
subtitle.Parent = topBar

local minimizeBtn = Instance.new("TextButton")
minimizeBtn.Size = UDim2.new(0, 32, 0, 32)
minimizeBtn.Position = UDim2.new(1, -78, 0.5, -16)
minimizeBtn.BackgroundColor3 = Color3.fromRGB(160, 30, 52)
minimizeBtn.Text = "−"
minimizeBtn.TextColor3 = Color3.new(1,1,1)
minimizeBtn.TextScaled = true
minimizeBtn.Font = Enum.Font.PermanentMarker
minimizeBtn.Parent = topBar

local minimizeCorner = Instance.new("UICorner")
minimizeCorner.CornerRadius = UDim.new(0, 10)
minimizeCorner.Parent = minimizeBtn

minimizeBtn.MouseEnter:Connect(function()
    minimizeBtn.BackgroundColor3 = Color3.fromRGB(220, 58, 80)
end)
minimizeBtn.MouseLeave:Connect(function()
    if not isMinimized then
        minimizeBtn.BackgroundColor3 = Color3.fromRGB(160, 30, 52)
    else
        minimizeBtn.BackgroundColor3 = Color3.fromRGB(67, 177, 151)
    end
end)

local closeBtn = Instance.new("TextButton")
closeBtn.Size = UDim2.new(0, 32, 0, 32)
closeBtn.Position = UDim2.new(1, -40, 0.5, -16)
closeBtn.BackgroundColor3 = Color3.fromRGB(205, 42, 62)
closeBtn.Text = "×"
closeBtn.TextColor3 = Color3.new(1,1,1)
closeBtn.TextScaled = true
closeBtn.Font = Enum.Font.PermanentMarker
closeBtn.Parent = topBar

local closeCorner = Instance.new("UICorner")
closeCorner.CornerRadius = UDim.new(0, 10)
closeCorner.Parent = closeBtn

closeBtn.MouseEnter:Connect(function()
    closeBtn.BackgroundColor3 = Color3.fromRGB(232, 70, 91)
end)
closeBtn.MouseLeave:Connect(function()
    closeBtn.BackgroundColor3 = Color3.fromRGB(174, 47, 70)
end)

local contentContainer = Instance.new("Frame")
contentContainer.Name = "ContentContainer"
contentContainer.Size = UDim2.new(1, 0, 1, -64)
contentContainer.Position = UDim2.new(0, 0, 0, 64)
contentContainer.BackgroundTransparency = 1
contentContainer.ZIndex = 3
contentContainer.Parent = mainFrame

local line = Instance.new("Frame")
line.Size = UDim2.new(0.88, 0, 0, 1)
line.Position = UDim2.new(0.06, 0, 0.045, 0)
line.BackgroundColor3 = Color3.fromRGB(255, 180, 190)
line.BackgroundTransparency = 0.25
line.BorderSizePixel = 0
line.Parent = contentContainer

local avatarCard = Instance.new("Frame")
avatarCard.Name = "ProfileCard"
avatarCard.Size = UDim2.new(0.88, 0, 0, 76)
avatarCard.Position = UDim2.new(0.06, 0, 0.09, 0)
avatarCard.BackgroundColor3 = Color3.fromRGB(68, 11, 27)
avatarCard.BackgroundTransparency = 0.04
avatarCard.BorderSizePixel = 0
avatarCard.ZIndex = 4
avatarCard.Parent = contentContainer

local avatarCardCorner = Instance.new("UICorner")
avatarCardCorner.CornerRadius = UDim.new(0, 14)
avatarCardCorner.Parent = avatarCard

local avatarCardStroke = Instance.new("UIStroke")
avatarCardStroke.Color = Color3.fromRGB(255, 130, 145)
avatarCardStroke.Transparency = 0.35
avatarCardStroke.Parent = avatarCard

local avatarImage = Instance.new("ImageLabel")
avatarImage.Size = UDim2.new(0, 58, 0, 58)
avatarImage.Position = UDim2.new(0, 10, 0.5, -29)
avatarImage.BackgroundColor3 = Color3.fromRGB(120, 25, 45)
avatarImage.BackgroundTransparency = 0
avatarImage.BorderSizePixel = 0
avatarImage.ZIndex = 5
avatarImage.Parent = avatarCard

local avatarCorner = Instance.new("UICorner")
avatarCorner.CornerRadius = UDim.new(0, 12)
avatarCorner.Parent = avatarImage

local playerNameLabel = Instance.new("TextLabel")
playerNameLabel.Size = UDim2.new(1, -86, 0, 24)
playerNameLabel.Position = UDim2.new(0, 82, 0, 14)
playerNameLabel.BackgroundTransparency = 1
playerNameLabel.Text = player.DisplayName
playerNameLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
playerNameLabel.TextStrokeColor3 = Color3.fromRGB(4, 16, 36)
playerNameLabel.TextStrokeTransparency = 0.35
playerNameLabel.TextSize = 18
playerNameLabel.Font = Enum.Font.PermanentMarker
playerNameLabel.TextXAlignment = Enum.TextXAlignment.Left
playerNameLabel.TextTruncate = Enum.TextTruncate.AtEnd
playerNameLabel.ZIndex = 6
playerNameLabel.Parent = avatarCard

local userNameLabel = Instance.new("TextLabel")
userNameLabel.Size = UDim2.new(1, -86, 0, 18)
userNameLabel.Position = UDim2.new(0, 82, 0, 39)
userNameLabel.BackgroundTransparency = 1
userNameLabel.Text = "@" .. player.Name .. "  |  ID " .. player.UserId
userNameLabel.TextColor3 = Color3.fromRGB(255, 210, 215)
userNameLabel.TextStrokeColor3 = Color3.fromRGB(4, 16, 36)
userNameLabel.TextStrokeTransparency = 0.4
userNameLabel.TextSize = 11
userNameLabel.Font = Enum.Font.PermanentMarker
userNameLabel.TextXAlignment = Enum.TextXAlignment.Left
userNameLabel.TextTruncate = Enum.TextTruncate.AtEnd
userNameLabel.ZIndex = 6
userNameLabel.Parent = avatarCard

local avatarContent, avatarReady = game.Players:GetUserThumbnailAsync(
    player.UserId,
    Enum.ThumbnailType.HeadShot,
    Enum.ThumbnailSize.Size100x100
)
if avatarReady then
    avatarImage.Image = avatarContent
end

local miniAvatar = Instance.new("ImageLabel")
miniAvatar.Name = "MiniAvatar"
miniAvatar.Size = UDim2.new(0, 38, 0, 38)
miniAvatar.Position = UDim2.new(0, 12, 0.5, -19)
miniAvatar.BackgroundColor3 = Color3.fromRGB(120, 25, 45)
miniAvatar.BackgroundTransparency = 0
miniAvatar.BorderSizePixel = 0
miniAvatar.Image = avatarContent
miniAvatar.Visible = false
miniAvatar.ZIndex = 6
miniAvatar.Parent = topBar

local miniAvatarCorner = Instance.new("UICorner")
miniAvatarCorner.CornerRadius = UDim.new(1, 0)
miniAvatarCorner.Parent = miniAvatar

local miniAvatarStroke = Instance.new("UIStroke")
miniAvatarStroke.Color = Color3.fromRGB(255, 205, 215)
miniAvatarStroke.Thickness = 1
miniAvatarStroke.Transparency = 0.15
miniAvatarStroke.Parent = miniAvatar

local miniUserLabel = Instance.new("TextLabel")
miniUserLabel.Size = UDim2.new(0, 130, 0, 22)
miniUserLabel.Position = UDim2.new(0, 60, 0, 7)
miniUserLabel.BackgroundTransparency = 1
miniUserLabel.Text = "YK8  |  @" .. player.Name
miniUserLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
miniUserLabel.TextSize = 15
miniUserLabel.Font = Enum.Font.PermanentMarker
miniUserLabel.TextStrokeColor3 = Color3.fromRGB(40, 0, 10)
miniUserLabel.TextStrokeTransparency = 0.2
miniUserLabel.TextXAlignment = Enum.TextXAlignment.Left
miniUserLabel.TextTruncate = Enum.TextTruncate.AtEnd
miniUserLabel.Visible = false
miniUserLabel.ZIndex = 6
miniUserLabel.Parent = topBar

local runtimeLabel = Instance.new("TextLabel")
runtimeLabel.Size = UDim2.new(0, 130, 0, 16)
runtimeLabel.Position = UDim2.new(0, 60, 0, 30)
runtimeLabel.BackgroundTransparency = 1
runtimeLabel.Text = "ONLINE  •  00:00:00"
runtimeLabel.TextColor3 = Color3.fromRGB(255, 205, 215)
runtimeLabel.TextSize = 10
runtimeLabel.Font = Enum.Font.PermanentMarker
runtimeLabel.TextXAlignment = Enum.TextXAlignment.Left
runtimeLabel.Visible = false
runtimeLabel.ZIndex = 6
runtimeLabel.Parent = topBar

local function formatRuntime(seconds)
    local totalSeconds = math.floor(seconds)
    local hours = math.floor(totalSeconds / 3600)
    local minutes = math.floor((totalSeconds % 3600) / 60)
    local remainingSeconds = totalSeconds % 60
    return string.format("ONLINE  •  %02d:%02d:%02d", hours, minutes, remainingSeconds)
end

task.spawn(function()
    while screenGui.Parent do
        runtimeLabel.Text = formatRuntime(os.clock() - scriptStartedAt)
        task.wait(1)
    end
end)

local statusLabel = Instance.new("TextLabel")
statusLabel.Size = UDim2.new(0.9, 0, 0, 28)
statusLabel.Position = UDim2.new(0.08, 0, 0.39, 0)
statusLabel.BackgroundTransparency = 1
statusLabel.Text = "● Status: Ready!"
statusLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
statusLabel.TextStrokeColor3 = Color3.fromRGB(5, 15, 31)
statusLabel.TextStrokeTransparency = 0.35
statusLabel.TextScaled = true
statusLabel.Font = Enum.Font.PermanentMarker
statusLabel.TextXAlignment = Enum.TextXAlignment.Left
statusLabel.ZIndex = 5
statusLabel.Parent = contentContainer

local speedLabel = Instance.new("TextLabel")
speedLabel.Size = UDim2.new(0.9, 0, 0, 28)
speedLabel.Position = UDim2.new(0.08, 0, 0.52, 0)
speedLabel.BackgroundTransparency = 1
speedLabel.Text = "SPEED     50"
speedLabel.TextColor3 = Color3.fromRGB(255, 205, 205)
speedLabel.TextStrokeColor3 = Color3.fromRGB(5, 15, 31)
speedLabel.TextStrokeTransparency = 0.35
speedLabel.TextScaled = true
speedLabel.Font = Enum.Font.PermanentMarker
speedLabel.TextXAlignment = Enum.TextXAlignment.Left
speedLabel.ZIndex = 5
speedLabel.Parent = contentContainer

local startButton = Instance.new("TextButton")
startButton.Size = UDim2.new(0.9, 0, 0, 44)
startButton.Position = UDim2.new(0.04, 0, 0.65, 0)
startButton.Size = UDim2.new(0.92, 0, 0, 62)
startButton.BackgroundColor3 = Color3.fromRGB(190, 27, 55)
startButton.BackgroundTransparency = 1
startButton.Text = ""
startButton.TextColor3 = Color3.new(1, 1, 1)
startButton.TextScaled = true
startButton.Font = Enum.Font.PermanentMarker
startButton.TextStrokeColor3 = Color3.fromRGB(4, 13, 32)
startButton.TextStrokeTransparency = 0.25
startButton.AutoButtonColor = false
startButton.Active = true
startButton.ClipsDescendants = true
startButton.ZIndex = 10
startButton.Parent = contentContainer

local startButtonImage = Instance.new("ImageLabel")
startButtonImage.Name = "StartButtonImage"
startButtonImage.Size = UDim2.new(0.92, 0, 0, 62)
startButtonImage.Position = UDim2.new(0.04, 0, 0.65, 0)
startButtonImage.BackgroundTransparency = 1
startButtonImage.BorderSizePixel = 0
startButtonImage.Image = "rbxassetid://134655520753678"
startButtonImage.ImageTransparency = 0
startButtonImage.ScaleType = Enum.ScaleType.Crop
startButtonImage.Active = false
startButtonImage.ZIndex = 11
startButtonImage.Parent = contentContainer

local startButtonImageCorner = Instance.new("UICorner")
startButtonImageCorner.CornerRadius = UDim.new(0, 16)
startButtonImageCorner.Parent = startButtonImage

local startCorner = Instance.new("UICorner")
startCorner.CornerRadius = UDim.new(0, 16)
startCorner.Parent = startButton

local buttonStroke = Instance.new("UIStroke")
buttonStroke.Color = Color3.fromRGB(255, 205, 210)
buttonStroke.Transparency = 0.35
buttonStroke.Thickness = 1
buttonStroke.Parent = startButton

local btnGradient = Instance.new("UIGradient")
btnGradient.Color = ColorSequence.new({
    ColorSequenceKeypoint.new(0, Color3.fromRGB(255, 85, 105)),
    ColorSequenceKeypoint.new(1, Color3.fromRGB(145, 14, 39))
})
btnGradient.Parent = startButton
btnGradient.Transparency = NumberSequence.new(1)

startButton.MouseEnter:Connect(function()
    startButton.BackgroundColor3 = Color3.fromRGB(235, 58, 82)
end)
startButton.MouseLeave:Connect(function()
    if isFarming then
        startButton.BackgroundColor3 = Color3.fromRGB(145, 14, 39)
    else
        startButton.BackgroundColor3 = Color3.fromRGB(190, 27, 55)
    end
end)

local creditLabel = Instance.new("TextLabel")
creditLabel.Size = UDim2.new(1, 0, 0, 14)
creditLabel.Position = UDim2.new(0, 0, 1, -22)
creditLabel.BackgroundTransparency = 1
creditLabel.Text = "YK8  /  MM2 FARM"
creditLabel.TextColor3 = Color3.fromRGB(255, 215, 220)
creditLabel.TextScaled = true
creditLabel.Font = Enum.Font.PermanentMarker
creditLabel.TextStrokeColor3 = Color3.fromRGB(4, 13, 32)
creditLabel.TextStrokeTransparency = 0.35
creditLabel.TextTransparency = 0.3
creditLabel.ZIndex = 5
creditLabel.Parent = contentContainer

mainFrame.InputBegan:Connect(function(input)
    if not isMinimized and (input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch) then
        dragging = true
        dragStart = input.Position
        startPos = mainFrame.Position

        if not isMinimized then
            mainFrame:TweenSize(UDim2.new(0, 385, 0, 325), Enum.EasingDirection.Out, Enum.EasingStyle.Quad, 0.15, true)
        end

        local connection
        connection = game:GetService("UserInputService").InputChanged:Connect(function(input2)
            if dragging and (input2.UserInputType == Enum.UserInputType.MouseMovement or input2.UserInputType == Enum.UserInputType.Touch) then
                local delta = input2.Position - dragStart
                mainFrame.Position = UDim2.new(
                    startPos.X.Scale,
                    startPos.X.Offset + delta.X,
                    startPos.Y.Scale,
                    startPos.Y.Offset + delta.Y
                )
            end
        end)

        input.Changed:Connect(function()
            if input.UserInputState == Enum.UserInputState.End then
                dragging = false
                connection:Disconnect()
                if not isMinimized then
                    mainFrame:TweenSize(UDim2.new(0, 390, 0, 330), Enum.EasingDirection.Out, Enum.EasingStyle.Quad, 0.15, true)
                end
            end
        end)
    end
end)

local TweenService = game:GetService("TweenService")
local LP = game.Players.LocalPlayer
local Char = LP.Character or LP.CharacterAdded:Wait()
local HRP = Char:WaitForChild("HumanoidRootPart")
local Humanoid = Char:WaitForChild("Humanoid")

local function GetMap()
    while true do
        for _, obj in ipairs(workspace:GetChildren()) do
            if obj:GetAttribute("MapID") and obj:FindFirstChild("CoinContainer") then
                return obj
            end
        end
        task.wait()
    end
end

local function getNearest()
    local map = GetMap()
    local closest, dist = nil, math.huge
    for _, coin in ipairs(map.CoinContainer:GetChildren()) do
        local v = coin:FindFirstChild("CoinVisual")
        local coinPart = coin:IsA("BasePart") and coin or coin:FindFirstChildWhichIsA("BasePart", true)
        if v and coinPart and not v:GetAttribute("Collected") then
            local d = (HRP.Position - coinPart.Position).Magnitude
            if d < dist then
                closest = coin
                dist = d
            end
        end
    end
    return closest
end

local function tp(hp)
    Humanoid:ChangeState(11)
    local coinPart = hp:IsA("BasePart") and hp or hp:FindFirstChildWhichIsA("BasePart", true)
    if not coinPart then return end
    local d = (HRP.Position - coinPart.Position).Magnitude
    local t = TweenService:Create(HRP, TweenInfo.new(math.max(d / 25, 0.05), Enum.EasingStyle.Linear), {CFrame = coinPart.CFrame})
    t:Play()
    t.Completed:Wait()
end

local function startFarming()
    if farmingConnection then return end

    farmingConnection = task.spawn(function()
        while isFarming do
            local target = getNearest()
            if target and LP:GetAttribute("Alive") then
                tp(target)
                local v = target:FindFirstChild("CoinVisual")
                while v and not v:GetAttribute("Collected") and v.Parent and isFarming do
                    if not LP:GetAttribute("Alive") then break end
                    local n = getNearest()
                    if n and n ~= target then break end
                    task.wait()
                end
            else
                task.wait(0.5)
            end
        end
    end)
end

local function stopFarming()
    isFarming = false
    if farmingConnection then
        farmingConnection = nil
    end
end

local function toggleFarming()
    isFarming = not isFarming

    if isFarming then
        startButton.Text = "⏹ STOP"
        startButton.BackgroundColor3 = Color3.fromRGB(177, 38, 73)
        statusLabel.Text = "● Status: Farming..."
        statusLabel.TextColor3 = Color3.fromRGB(255, 231, 139)
        game:GetService("TweenService"):Create(statusLabel, TweenInfo.new(0.3), {TextColor3 = Color3.fromRGB(255, 231, 139)}):Play()
        startFarming()
        print("MM2 Farm Started!")
    else
        startButton.Text = "▶ START"
        startButton.BackgroundColor3 = Color3.fromRGB(190, 27, 55)
        statusLabel.Text = "● Status: Stopped"
        statusLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
        game:GetService("TweenService"):Create(statusLabel, TweenInfo.new(0.3), {TextColor3 = Color3.fromRGB(255, 255, 255)}):Play()
        stopFarming()
        print("MM2 Farm Stopped!")
    end
end

local function toggleMinimize()
    isMinimized = not isMinimized

    if isMinimized then

        mainFrame:TweenSize(UDim2.new(0, 320, 0, 58), Enum.EasingDirection.Out, Enum.EasingStyle.Quad, 0.3, true)
        mainFrame:TweenPosition(UDim2.new(0.5, -160, 0, 18), Enum.EasingDirection.Out, Enum.EasingStyle.Quad, 0.3, true)
        minimizeBtn.Text = "+"
        minimizeBtn.BackgroundColor3 = Color3.fromRGB(67, 177, 151)
        minimizeBtn.TextSize = 24

        contentContainer.Visible = false

        umbrella.Visible = false
        title.Visible = false
        subtitle.Visible = false
        miniAvatar.Visible = true
        miniUserLabel.Visible = true
        runtimeLabel.Visible = true

        glow.Size = UDim2.new(1.08, 0, 1.12, 0)
        glow.Position = UDim2.new(-0.04, 0, -0.06, 0)

        title.Text = "YK8"
        title.Position = UDim2.new(0, 62, 0, 5)
        title.Size = UDim2.new(0.55, 0, 0, 36)
        title.TextScaled = true

        topCorner.CornerRadius = UDim.new(0, 20)

    else

        mainFrame:TweenSize(UDim2.new(0, 390, 0, 330), Enum.EasingDirection.Out, Enum.EasingStyle.Quad, 0.3, true)
        mainFrame:TweenPosition(UDim2.new(0.5, -195, 0.5, -165), Enum.EasingDirection.Out, Enum.EasingStyle.Quad, 0.3, true)
        minimizeBtn.Text = "−"
        minimizeBtn.BackgroundColor3 = Color3.fromRGB(160, 30, 52)
        minimizeBtn.TextSize = 18

        contentContainer.Visible = true

        umbrella.Visible = true

        subtitle.Visible = false
        title.Visible = true
        miniAvatar.Visible = false
        miniUserLabel.Visible = false
        runtimeLabel.Visible = false

        glow.Size = UDim2.new(1.04, 0, 1.04, 0)
        glow.Position = UDim2.new(-0.02, 0, -0.02, 0)

        title.Text = "YK8"
        title.Position = UDim2.new(0, 62, 0, 5)
        title.Size = UDim2.new(0.55, 0, 0, 36)
        title.TextScaled = true

        topCorner.CornerRadius = UDim.new(0, 16)
    end
end

minimizeBtn.MouseButton1Click:Connect(toggleMinimize)

closeBtn.MouseButton1Click:Connect(function()
    mainFrame:TweenSize(UDim2.new(0, 0, 0, 0), Enum.EasingDirection.In, Enum.EasingStyle.Quad, 0.3, true)
    task.wait(0.3)
    stopFarming()
    screenGui:Destroy()
end)

startButton.MouseButton1Click:Connect(toggleFarming)

LP.CharacterAdded:Connect(function(char)
    Char = char
    HRP = char:WaitForChild("HumanoidRootPart")
    Humanoid = char:WaitForChild("Humanoid")
end)
