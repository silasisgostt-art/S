local Players          = game:GetService("Players")
local RunService       = game:GetService("RunService")
local TweenService     = game:GetService("TweenService")
local UserInputService = game:GetService("UserInputService")
local Player           = Players.LocalPlayer

local Config = {
    ForwardSpeed = 59,
    ReturnSpeed  = 28,
}

local POSITION_L1     = Vector3.new(-476.48, -6.28,  92.73)
local POSITION_LEND   = Vector3.new(-483.12, -4.95,  94.80)
local POSITION_LFINAL = Vector3.new(-473.38, -8.40,  22.34)

local POSITION_R1     = Vector3.new(-476.16, -6.52,  25.62)
local POSITION_REND   = Vector3.new(-483.04, -5.09,  23.14)
local POSITION_RFINAL = Vector3.new(-476.17, -7.91, 97.91)

local function getHRP()
    local c = Player.Character
    return c and c:FindFirstChild("HumanoidRootPart")
end
local function getHum()
    local c = Player.Character
    return c and c:FindFirstChildOfClass("Humanoid")
end

local AutoLeftEnabled = false
local autoLeftPhase   = 1
local autoLeftConn    = nil

local function stopAutoLeft()
    if autoLeftConn then autoLeftConn:Disconnect(); autoLeftConn = nil end
    autoLeftPhase = 1
    local hum = getHum()
    if hum then hum:Move(Vector3.zero, false) end
end

local function startAutoLeft()
    if autoLeftConn then autoLeftConn:Disconnect() end
    autoLeftPhase = 1

    autoLeftConn = RunService.Heartbeat:Connect(function()
        if not AutoLeftEnabled then return end
        local h, hum = getHRP(), getHum()
        if not h or not hum then return end

        if autoLeftPhase == 1 then
            local d = Vector3.new(POSITION_L1.X - h.Position.X, 0, POSITION_L1.Z - h.Position.Z)
            if d.Magnitude < 1 then autoLeftPhase = 2; return end
            local md = d.Unit
            hum:Move(md, false)
            h.AssemblyLinearVelocity = Vector3.new(md.X * Config.ForwardSpeed, h.AssemblyLinearVelocity.Y, md.Z * Config.ForwardSpeed)

        elseif autoLeftPhase == 2 then
            local d = Vector3.new(POSITION_LEND.X - h.Position.X, 0, POSITION_LEND.Z - h.Position.Z)
            if d.Magnitude < 1 then
                autoLeftPhase = 0
                hum:Move(Vector3.zero, false)
                h.AssemblyLinearVelocity = Vector3.new(0, 0, 0)
                task.delay(0.2, function()
                    if AutoLeftEnabled then autoLeftPhase = 3 end
                end)
                return
            end
            local md = d.Unit
            hum:Move(md, false)
            h.AssemblyLinearVelocity = Vector3.new(md.X * Config.ForwardSpeed, h.AssemblyLinearVelocity.Y, md.Z * Config.ForwardSpeed)

        elseif autoLeftPhase == 0 then
            return

        elseif autoLeftPhase == 3 then
            local d = Vector3.new(POSITION_L1.X - h.Position.X, 0, POSITION_L1.Z - h.Position.Z)
            if d.Magnitude < 1 then autoLeftPhase = 4; return end
            local md = d.Unit
            hum:Move(md, false)
            h.AssemblyLinearVelocity = Vector3.new(md.X * Config.ReturnSpeed, h.AssemblyLinearVelocity.Y, md.Z * Config.ReturnSpeed)

        elseif autoLeftPhase == 4 then
            local d = Vector3.new(POSITION_LFINAL.X - h.Position.X, 0, POSITION_LFINAL.Z - h.Position.Z)
            if d.Magnitude < 1 then
                hum:Move(Vector3.zero, false)
                h.AssemblyLinearVelocity = Vector3.new(0, 0, 0)
                AutoLeftEnabled = false
                stopAutoLeft()
                if _G._updateMiniLeft then _G._updateMiniLeft() end
                return
            end
            local md = d.Unit
            hum:Move(md, false)
            h.AssemblyLinearVelocity = Vector3.new(md.X * Config.ReturnSpeed, h.AssemblyLinearVelocity.Y, md.Z * Config.ReturnSpeed)
        end
    end)
end

local AutoRightEnabled = false
local autoRightPhase   = 1
local autoRightConn    = nil

local function stopAutoRight()
    if autoRightConn then autoRightConn:Disconnect(); autoRightConn = nil end
    autoRightPhase = 1
    local hum = getHum()
    if hum then hum:Move(Vector3.zero, false) end
end

local function startAutoRight()
    if autoRightConn then autoRightConn:Disconnect() end
    autoRightPhase = 1

    autoRightConn = RunService.Heartbeat:Connect(function()
        if not AutoRightEnabled then return end
        local h, hum = getHRP(), getHum()
        if not h or not hum then return end

        if autoRightPhase == 1 then
            local d = Vector3.new(POSITION_R1.X - h.Position.X, 0, POSITION_R1.Z - h.Position.Z)
            if d.Magnitude < 1 then autoRightPhase = 2; return end
            local md = d.Unit
            hum:Move(md, false)
            h.AssemblyLinearVelocity = Vector3.new(md.X * Config.ForwardSpeed, h.AssemblyLinearVelocity.Y, md.Z * Config.ForwardSpeed)

        elseif autoRightPhase == 2 then
            local d = Vector3.new(POSITION_REND.X - h.Position.X, 0, POSITION_REND.Z - h.Position.Z)
            if d.Magnitude < 1 then
                autoRightPhase = 0
                hum:Move(Vector3.zero, false)
                h.AssemblyLinearVelocity = Vector3.new(0, 0, 0)
                task.delay(0.2, function()
                    if AutoRightEnabled then autoRightPhase = 3 end
                end)
                return
            end
            local md = d.Unit
            hum:Move(md, false)
            h.AssemblyLinearVelocity = Vector3.new(md.X * Config.ForwardSpeed, h.AssemblyLinearVelocity.Y, md.Z * Config.ForwardSpeed)

        elseif autoRightPhase == 0 then
            return

        elseif autoRightPhase == 3 then
            local d = Vector3.new(POSITION_R1.X - h.Position.X, 0, POSITION_R1.Z - h.Position.Z)
            if d.Magnitude < 1 then autoRightPhase = 4; return end
            local md = d.Unit
            hum:Move(md, false)
            h.AssemblyLinearVelocity = Vector3.new(md.X * Config.ReturnSpeed, h.AssemblyLinearVelocity.Y, md.Z * Config.ReturnSpeed)

        elseif autoRightPhase == 4 then
            local d = Vector3.new(POSITION_RFINAL.X - h.Position.X, 0, POSITION_RFINAL.Z - h.Position.Z)
            if d.Magnitude < 1 then
                hum:Move(Vector3.zero, false)
                h.AssemblyLinearVelocity = Vector3.new(0, 0, 0)
                AutoRightEnabled = false
                stopAutoRight()
                if _G._updateMiniRight then _G._updateMiniRight() end
                return
            end
            local md = d.Unit
            hum:Move(md, false)
            h.AssemblyLinearVelocity = Vector3.new(md.X * Config.ReturnSpeed, h.AssemblyLinearVelocity.Y, md.Z * Config.ReturnSpeed)
        end
    end)
end

local sg = Instance.new("ScreenGui")
sg.Name        = "AutoLR_GUI"
sg.ResetOnSpawn = false
sg.DisplayOrder = 999
sg.Parent       = Player.PlayerGui

local frame = Instance.new("Frame")
frame.Size            = UDim2.new(0, 200, 0, 230)
frame.Position        = UDim2.new(0, 20, 0.5, -115)
frame.BackgroundColor3 = Color3.fromRGB(2, 2, 6)
frame.BorderSizePixel = 0
frame.Active    = true
frame.Draggable = true
frame.Parent    = sg
Instance.new("UICorner", frame).CornerRadius = UDim.new(0, 14)

local stroke = Instance.new("UIStroke", frame)
stroke.Thickness = 2
local borderGrad = Instance.new("UIGradient", stroke)
borderGrad.Color = ColorSequence.new({
    ColorSequenceKeypoint.new(0,    Color3.fromRGB(0,   210, 130)),
    ColorSequenceKeypoint.new(0.25, Color3.fromRGB(0,   0,   0  )),
    ColorSequenceKeypoint.new(0.5,  Color3.fromRGB(70,  140, 255)),
    ColorSequenceKeypoint.new(0.75, Color3.fromRGB(0,   0,   0  )),
    ColorSequenceKeypoint.new(1,    Color3.fromRGB(0,   210, 130)),
})
task.spawn(function()
    local r = 0
    while frame.Parent do
        r = (r + 3) % 360
        borderGrad.Rotation = r
        task.wait(0.02)
    end
end)

local title = Instance.new("TextLabel", frame)
title.Size               = UDim2.new(1, 0, 0, 30)
title.BackgroundTransparency = 1
title.Text               = "Auto Play"
title.TextColor3         = Color3.fromRGB(100, 200, 255)
title.Font               = Enum.Font.GothamBlack
title.TextSize           = 14
title.ZIndex             = 3

local btnLeft = Instance.new("TextButton", frame)
btnLeft.Size             = UDim2.new(1, -20, 0, 34)
btnLeft.Position         = UDim2.new(0, 10, 0, 33)
btnLeft.BackgroundColor3 = Color3.fromRGB(30, 70, 180)
btnLeft.Text             = "AUTO LEFT  ●  OFF"
btnLeft.TextColor3       = Color3.fromRGB(255, 255, 255)
btnLeft.Font             = Enum.Font.GothamBold
btnLeft.TextSize         = 12
btnLeft.AutoButtonColor  = false
btnLeft.ZIndex           = 3
Instance.new("UICorner", btnLeft).CornerRadius = UDim.new(0, 10)

local btnRight = Instance.new("TextButton", frame)
btnRight.Size             = UDim2.new(1, -20, 0, 34)
btnRight.Position         = UDim2.new(0, 10, 0, 71)
btnRight.BackgroundColor3 = Color3.fromRGB(20, 110, 80)
btnRight.Text             = "AUTO RIGHT  ●  OFF"
btnRight.TextColor3       = Color3.fromRGB(255, 255, 255)
btnRight.Font             = Enum.Font.GothamBold
btnRight.TextSize         = 12
btnRight.AutoButtonColor  = false
btnRight.ZIndex           = 3
Instance.new("UICorner", btnRight).CornerRadius = UDim.new(0, 10)

local sep = Instance.new("Frame", frame)
sep.Size              = UDim2.new(0.85, 0, 0, 1)
sep.Position          = UDim2.new(0.075, 0, 0, 114)
sep.BackgroundColor3  = Color3.fromRGB(35, 35, 55)
sep.BorderSizePixel   = 0
sep.ZIndex            = 3

local function makeSlider(yPos, labelText, labelColor, fillColorSeq, defaultVal, maxVal, onChanged)
    local lbl = Instance.new("TextLabel", frame)
    lbl.Size               = UDim2.new(1, -20, 0, 16)
    lbl.Position           = UDim2.new(0, 10, 0, yPos)
    lbl.BackgroundTransparency = 1
    lbl.Text               = labelText .. defaultVal
    lbl.TextColor3         = labelColor
    lbl.Font               = Enum.Font.GothamBold
    lbl.TextSize           = 11
    lbl.TextXAlignment     = Enum.TextXAlignment.Left
    lbl.ZIndex             = 3

    local bg = Instance.new("Frame", frame)
    bg.Size               = UDim2.new(1, -20, 0, 8)
    bg.Position           = UDim2.new(0, 10, 0, yPos + 19)
    bg.BackgroundColor3   = Color3.fromRGB(15, 15, 25)
    bg.BorderSizePixel    = 0
    bg.ZIndex             = 3
    Instance.new("UICorner", bg).CornerRadius = UDim.new(1, 0)

    local fill = Instance.new("Frame", bg)
    fill.Size             = UDim2.new(defaultVal / maxVal, 0, 1, 0)
    fill.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
    fill.BorderSizePixel  = 0
    fill.ZIndex           = 4
    Instance.new("UICorner", fill).CornerRadius = UDim.new(1, 0)

    local fg = Instance.new("UIGradient", fill)
    fg.Color = fillColorSeq

    local sh = Instance.new("Frame", fill)
    sh.Size                  = UDim2.new(0, 20, 1, 0)
    sh.BackgroundColor3      = Color3.fromRGB(255, 255, 255)
    sh.BackgroundTransparency = 0.55
    sh.BorderSizePixel       = 0
    sh.ZIndex                = 5
    Instance.new("UICorner", sh).CornerRadius = UDim.new(1, 0)
    local shg = Instance.new("UIGradient", sh)
    shg.Transparency = NumberSequence.new({
        NumberSequenceKeypoint.new(0,   1),
        NumberSequenceKeypoint.new(0.5, 0.4),
        NumberSequenceKeypoint.new(1,   1),
    })
    task.spawn(function()
        local offset = math.random()
        task.wait(offset * 1.5)
        while sh.Parent do
            sh.Position = UDim2.new(-0.15, 0, 0, 0)
            TweenService:Create(sh, TweenInfo.new(1.2, Enum.EasingStyle.Quad, Enum.EasingDirection.InOut),
                {Position = UDim2.new(1.1, 0, 0, 0)}):Play()
            task.wait(1.9)
        end
    end)

    local knob = Instance.new("Frame", fill)
    knob.Size            = UDim2.new(0, 12, 0, 12)
    knob.Position        = UDim2.new(1, -6, 0.5, -6)
    knob.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
    knob.BorderSizePixel = 0
    knob.ZIndex          = 6
    Instance.new("UICorner", knob).CornerRadius = UDim.new(1, 0)

    local btn = Instance.new("TextButton", bg)
    btn.Size             = UDim2.new(1, 0, 4, 0)
    btn.Position         = UDim2.new(0, 0, -1.5, 0)
    btn.BackgroundTransparency = 1
    btn.Text             = ""
    btn.ZIndex           = 7

    local dragging = false
    btn.MouseButton1Down:Connect(function() dragging = true end)
    UserInputService.InputEnded:Connect(function(i)
        if i.UserInputType == Enum.UserInputType.MouseButton1 then dragging = false end
    end)
    UserInputService.InputChanged:Connect(function(i)
        if dragging and i.UserInputType == Enum.UserInputType.MouseMovement then
            local pct = math.clamp((i.Position.X - bg.AbsolutePosition.X) / bg.AbsoluteSize.X, 0, 1)
            local val = math.max(1, math.floor(pct * maxVal))
            fill.Size = UDim2.new(pct, 0, 1, 0)
            lbl.Text  = labelText .. val
            onChanged(val)
        end
    end)

    return lbl, fill
end

makeSlider(
    120,
    "Speed 1 (aller) : ",
    Color3.fromRGB(100, 180, 255),
    ColorSequence.new({
        ColorSequenceKeypoint.new(0,   Color3.fromRGB(120, 190, 255)),
        ColorSequenceKeypoint.new(0.5, Color3.fromRGB(60,  130, 255)),
        ColorSequenceKeypoint.new(1,   Color3.fromRGB(30,  80,  220)),
    }),
    Config.ForwardSpeed,
    100,
    function(v) Config.ForwardSpeed = v end
)

makeSlider(
    163,
    "Speed 2 (retour) : ",
    Color3.fromRGB(80, 220, 140),
    ColorSequence.new({
        ColorSequenceKeypoint.new(0,   Color3.fromRGB(130, 255, 180)),
        ColorSequenceKeypoint.new(0.5, Color3.fromRGB(40,  200, 100)),
        ColorSequenceKeypoint.new(1,   Color3.fromRGB(20,  140,  60)),
    }),
    Config.ReturnSpeed,
    100,
    function(v) Config.ReturnSpeed = v end
)

local LEFT_ON   = Color3.fromRGB(60,  130, 255)
local LEFT_OFF  = Color3.fromRGB(30,  70,  180)
local RIGHT_ON  = Color3.fromRGB(50,  200, 150)
local RIGHT_OFF = Color3.fromRGB(20,  110, 80 )

local function updateLeft()
    if AutoLeftEnabled then
        TweenService:Create(btnLeft, TweenInfo.new(0.2), {BackgroundColor3 = LEFT_ON}):Play()
        btnLeft.Text = "AUTO LEFT  ●  ON"
    else
        TweenService:Create(btnLeft, TweenInfo.new(0.2), {BackgroundColor3 = LEFT_OFF}):Play()
        btnLeft.Text = "AUTO LEFT  ●  OFF"
    end
end

local function updateRight()
    if AutoRightEnabled then
        TweenService:Create(btnRight, TweenInfo.new(0.2), {BackgroundColor3 = RIGHT_ON}):Play()
        btnRight.Text = "AUTO RIGHT  ●  ON"
    else
        TweenService:Create(btnRight, TweenInfo.new(0.2), {BackgroundColor3 = RIGHT_OFF}):Play()
        btnRight.Text = "AUTO RIGHT  ●  OFF"
    end
end

_G._updateMiniLeft  = updateLeft
_G._updateMiniRight = updateRight

btnLeft.MouseButton1Click:Connect(function()
    AutoLeftEnabled = not AutoLeftEnabled
    if AutoLeftEnabled then
        AutoRightEnabled = false
        stopAutoRight()
        updateRight()
        startAutoLeft()
    else
        stopAutoLeft()
    end
    updateLeft()
end)

btnRight.MouseButton1Click:Connect(function()
    AutoRightEnabled = not AutoRightEnabled
    if AutoRightEnabled then
        AutoLeftEnabled = false
        stopAutoLeft()
        updateLeft()
        startAutoRight()
    else
        stopAutoRight()
    end
    updateRight()
end)

updateLeft()
updateRight()
