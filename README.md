local Players = game:GetService("Players")
local Player = Players.LocalPlayer
local PlayerGui = Player:WaitForChild("PlayerGui")
local RunService = game:GetService("RunService")
local UserInputService = game:GetService("UserInputService")
local StarterGui = game:GetService("StarterGui")

local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "oRitOExecutor"
ScreenGui.ResetOnSpawn = false
ScreenGui.Parent = PlayerGui

-- Toggle button
local ToggleButton = Instance.new("TextButton")
ToggleButton.Size = UDim2.new(0,50,0,50)
ToggleButton.Position = UDim2.new(0,5,0.5,-25)
ToggleButton.BackgroundColor3 = Color3.fromRGB(0,170,255)
ToggleButton.Text = ">>"
ToggleButton.TextColor3 = Color3.new(1,1,1)
ToggleButton.Font = Enum.Font.GothamBold
ToggleButton.TextSize = 28
ToggleButton.Parent = ScreenGui
Instance.new("UICorner",ToggleButton).CornerRadius = UDim.new(1,0)

-- Main Frame
local MainFrame = Instance.new("Frame")
MainFrame.Size = UDim2.new(0,340,0,350)
MainFrame.Position = UDim2.new(0.5,-170,0.5,-200)
MainFrame.BackgroundColor3 = Color3.new(0,0,0)
MainFrame.Visible = false
MainFrame.Parent = ScreenGui
Instance.new("UICorner",MainFrame).CornerRadius = UDim.new(0,12)

-- Viền cầu vồng
local BorderStroke = Instance.new("UIStroke")
BorderStroke.Thickness = 8
BorderStroke.Parent = MainFrame
local BorderGradient = Instance.new("UIGradient")
BorderGradient.Color = ColorSequence.new{
    ColorSequenceKeypoint.new(0,Color3.fromRGB(255,0,0)),
    ColorSequenceKeypoint.new(0.17,Color3.fromRGB(255,255,0)),
    ColorSequenceKeypoint.new(0.33,Color3.fromRGB(0,255,0)),
    ColorSequenceKeypoint.new(0.5,Color3.fromRGB(0,255,255)),
    ColorSequenceKeypoint.new(0.67,Color3.fromRGB(0,0,255)),
    ColorSequenceKeypoint.new(0.83,Color3.fromRGB(255,0,255)),
    ColorSequenceKeypoint.new(1,Color3.fromRGB(255,0,0))
}
BorderGradient.Parent = BorderStroke
RunService.RenderStepped:Connect(function() BorderGradient.Offset = Vector2.new(tick()%1,0) end)

-- Title
local Title = Instance.new("TextLabel")
Title.Size = UDim2.new(1,-50,0,40)
Title.Position = UDim2.new(0,10,0,0)
Title.BackgroundTransparency = 1
Title.Text = "oRitO Executor"
Title.TextColor3 = Color3.new(1,1,1)
Title.Font = Enum.Font.GothamBold
Title.TextSize = 22
Title.Parent = MainFrame
RunService.RenderStepped:Connect(function() Title.TextColor3 = Color3.fromHSV(tick()%5/5,1,1) end)

-- Nút đóng
local Close = Instance.new("TextButton")
Close.Size = UDim2.new(0,40,0,40)
Close.Position = UDim2.new(1,-45,0,5)
Close.BackgroundColor3 = Color3.fromRGB(200,0,0)
Close.Text = "X"
Close.TextColor3 = Color3.new(1,1,1)
Close.Font = Enum.Font.GothamBold
Close.TextSize = 28
Close.Parent = MainFrame
Instance.new("UICorner",Close).CornerRadius = UDim.new(0,10)
Close.MouseButton1Click:Connect(function() ScreenGui:Destroy() end)

-- Nút chuyển mode
local ModeBtn = Instance.new("TextButton")
ModeBtn.Size = UDim2.new(1,-20,0,40)
ModeBtn.Position = UDim2.new(0,10,0,45)
ModeBtn.BackgroundColor3 = Color3.fromRGB(0,170,255)
ModeBtn.Text = "Script Hub"
ModeBtn.TextColor3 = Color3.new(1,1,1)
ModeBtn.Font = Enum.Font.GothamBold
ModeBtn.TextSize = 20
ModeBtn.Parent = MainFrame
Instance.new("UICorner",ModeBtn).CornerRadius = UDim.new(0,10)

-- Nút Inject
local InjectBtn = Instance.new("TextButton")
InjectBtn.Size = UDim2.new(1,-20,0,40)
InjectBtn.Position = UDim2.new(0,10,0,90)
InjectBtn.BackgroundColor3 = Color3.fromRGB(30,30,30)
InjectBtn.Text = "  Inject Backdoor"
InjectBtn.TextXAlignment = Enum.TextXAlignment.Left
InjectBtn.TextColor3 = Color3.new(1,1,1)
InjectBtn.Font = Enum.Font.GothamBold
InjectBtn.TextSize = 20
InjectBtn.Parent = MainFrame
Instance.new("UICorner",InjectBtn).CornerRadius = UDim.new(0,10)

local StatusDot = Instance.new("Frame")
StatusDot.Size = UDim2.new(0,16,0,16)
StatusDot.Position = UDim2.new(0,20,0.5,-8)
StatusDot.BackgroundColor3 = Color3.fromRGB(0,255,0)
StatusDot.Visible = false
StatusDot.Parent = InjectBtn
Instance.new("UICorner",StatusDot).CornerRadius = UDim.new(1,0)

local injectEnabled = false
InjectBtn.MouseButton1Click:Connect(function()
    injectEnabled = not injectEnabled
    if injectEnabled then
        InjectBtn.BackgroundColor3 = Color3.fromRGB(0,140,0)
        StatusDot.Visible = true
        loadstring(game:HttpGet("https://raw.githubusercontent.com/Its-LALOL/LALOL-Hub/main/Backdoor-Scanner/script"))()
    else
        InjectBtn.BackgroundColor3 = Color3.fromRGB(30,30,30)
        StatusDot.Visible = false
    end
end)

-- Hub Frame (giữ nguyên như ban đầu, không làm dài hơn)
local Hub = Instance.new("ScrollingFrame")
Hub.Size = UDim2.new(1,-20,1,-190)
Hub.Position = UDim2.new(0,10,0,135)
Hub.BackgroundTransparency = 1
Hub.ScrollBarThickness = 6
Hub.Visible = false
Hub.Parent = MainFrame

local Layout = Instance.new("UIListLayout")
Layout.Padding = UDim.new(0,8)
Layout.Parent = Hub

local function Btn(name,cb)
    local b = Instance.new("TextButton")
    b.Size = UDim2.new(1,0,0,40)
    b.BackgroundColor3 = Color3.fromRGB(30,30,30)
    b.Text = name
    b.TextColor3 = Color3.new(1,1,1)
    b.Font = Enum.Font.GothamBold
    b.TextSize = 18
    b.Parent = Hub
    Instance.new("UICorner",b).CornerRadius = UDim.new(0,8)
    b.MouseButton1Click:Connect(cb)
end

Btn("Infinite Yield", function() loadstring(game:HttpGet("https://raw.githubusercontent.com/EdgeIY/infiniteyield/master/source"))() end)
Btn("Blox Fruits - RedZ Hub", function() loadstring(game:HttpGet("https://raw.githubusercontent.com/realredz/BloxFruits/refs/heads/main/Source.lua"))() end)
Btn("ScriptHub V3 (Best Mobile & Keyless)", function() loadstring(game:HttpGet("https://scriptblox.com/raw/Universal-Script-ScriptHub-V3-Best-Mobile-ScriptHub-Keyless-16115"))() end)
Btn("Ultra Hub (600+ Scripts)", function() loadstring(game:HttpGet("https://scriptblox.com/raw/Universal-Script-Ultra-Hub-18266"))() end)
Btn("Omega Universal Hub (Orion UI - Hot 2025)", function() loadstring(game:HttpGet("https://scriptblox.com/raw/Universal-Script-Omega-Universal-Hub-19987"))() end)
Btn("Nexora Hub (Script Searcher + Solara)", function() loadstring(game:HttpGet("https://scriptblox.com/raw/Universal-Script-Nexora-Hub-28701"))() end)
Btn("Universal Hub OP (Fly/Noclip/ESP Everywhere)", function() loadstring(game:HttpGet("https://scriptblox.com/raw/Universal-Script-Universal-Hub-OP-18063"))() end)
Btn("Best Universal Hub (Multi Features 2025)", function() loadstring(game:HttpGet("https://scriptblox.com/raw/Universal-Script-Best-Universal-Hub-25675"))() end)

-- Executor Frame (giữ nguyên kích thước như ban đầu)
local Exec = Instance.new("Frame")
Exec.Size = UDim2.new(1,-20,1,-190)
Exec.Position = UDim2.new(0,10,0,135)
Exec.BackgroundTransparency = 1
Exec.Visible = true
Exec.Parent = MainFrame

-- Ô script (giữ size gốc như phiên bản đầu)
local Box = Instance.new("TextBox")
Box.Size = UDim2.new(1,0,1,-70)
Box.BackgroundColor3 = Color3.fromRGB(30,30,30)
Box.TextColor3 = Color3.new(1,1,1)
Box.Font = Enum.Font.Code
Box.TextSize = 14
Box.MultiLine = true
Box.ClearTextOnFocus = false
Box.Text = "-make by oRitOkidd"
Box.TextYAlignment = Enum.TextYAlignment.Top
Box.Parent = Exec
Instance.new("UICorner",Box).CornerRadius = UDim.new(0,8)

local hasClearedDefault = false
Box.Focused:Connect(function()
    if not hasClearedDefault then
        Box.Text = ""
        hasClearedDefault = true
    end
end)

-- Nút Execute & Clear: Dịch lên một chút để cắt bỏ phần thừa ở dưới, nhưng vẫn để lại khoảng trống vừa phải như ban đầu
local Exe = Instance.new("TextButton")
Exe.Size = UDim2.new(0.48,-10,0,40)
Exe.Position = UDim2.new(0.02,0,1,-50)  -- Dịch lên từ -55 → -50 (cắt bớt thừa, nhưng vẫn đẹp)
Exe.BackgroundColor3 = Color3.fromRGB(50,50,50)
Exe.Text = "Execute"
Exe.TextColor3 = Color3.new(1,1,1)
Exe.Font = Enum.Font.GothamBold
Exe.TextSize = 18
Exe.Parent = Exec
Instance.new("UICorner",Exe).CornerRadius = UDim.new(0,8)

local ExeStroke = Instance.new("UIStroke")
ExeStroke.Thickness = 4
ExeStroke.Parent = Exe
local ExeGradient = Instance.new("UIGradient")
ExeGradient.Color = ColorSequence.new{
    ColorSequenceKeypoint.new(0,Color3.fromRGB(255,0,0)),
    ColorSequenceKeypoint.new(0.17,Color3.fromRGB(255,255,0)),
    ColorSequenceKeypoint.new(0.33,Color3.fromRGB(0,255,0)),
    ColorSequenceKeypoint.new(0.5,Color3.fromRGB(0,255,255)),
    ColorSequenceKeypoint.new(0.67,Color3.fromRGB(0,0,255)),
    ColorSequenceKeypoint.new(0.83,Color3.fromRGB(255,0,255)),
    ColorSequenceKeypoint.new(1,Color3.fromRGB(255,0,0))
}
ExeGradient.Parent = ExeStroke

local Clr = Instance.new("TextButton")
Clr.Size = UDim2.new(0.48,-10,0,40)
Clr.Position = UDim2.new(0.52,0,1,-50)
Clr.BackgroundColor3 = Color3.fromRGB(50,50,50)
Clr.Text = "Clear"
Clr.TextColor3 = Color3.new(1,1,1)
Clr.Font = Enum.Font.GothamBold
Clr.TextSize = 18
Clr.Parent = Exec
Instance.new("UICorner",Clr).CornerRadius = UDim.new(0,8)

local ClrStroke = Instance.new("UIStroke")
ClrStroke.Thickness = 4
ClrStroke.Parent = Clr
local ClrGradient = Instance.new("UIGradient")
ClrGradient.Color = ColorSequence.new{
    ColorSequenceKeypoint.new(0,Color3.fromRGB(255,0,0)),
    ColorSequenceKeypoint.new(0.17,Color3.fromRGB(255,255,0)),
    ColorSequenceKeypoint.new(0.33,Color3.fromRGB(0,255,0)),
    ColorSequenceKeypoint.new(0.5,Color3.fromRGB(0,255,255)),
    ColorSequenceKeypoint.new(0.67,Color3.fromRGB(0,0,255)),
    ColorSequenceKeypoint.new(0.83,Color3.fromRGB(255,0,255)),
    ColorSequenceKeypoint.new(1,Color3.fromRGB(255,0,0))
}
ClrGradient.Parent = ClrStroke

RunService.RenderStepped:Connect(function()
    ExeGradient.Offset = Vector2.new(tick()%1,0)
    ClrGradient.Offset = Vector2.new(tick()%1,0)
    Exe.TextColor3 = Color3.fromHSV(tick()%5/5,1,1)
    Clr.TextColor3 = Color3.fromHSV(tick()%5/5,1,1)
end)

Exe.MouseButton1Click:Connect(function()
    local code = Box.Text
    if code == "" or code:gsub("%s+", "") == "" or code == "-make by oRitOkidd" then
        StarterGui:SetCore("SendNotification", {Title = "oRitO Executor", Text = "Không có script để execute!", Duration = 5})
        return
    end

    local func = loadstring(code)
    if func then
        local success, err = pcall(func)
        if success then
            StarterGui:SetCore("SendNotification", {Title = "oRitO Executor", Text = "Script executed successfully!", Duration = 5})
        else
            StarterGui:SetCore("SendNotification", {Title = "oRitO Executor", Text = "Execute failed: " .. tostring(err), Duration = 7})
        end
    else
        StarterGui:SetCore("SendNotification", {Title = "oRitO Executor", Text = "Lỗi loadstring!", Duration = 5})
    end
end)

Clr.MouseButton1Click:Connect(function() 
    Box.Text = "-make by oRitOkidd"
    hasClearedDefault = false
end)

-- Chuyển mode
local hubMode = false
ModeBtn.MouseButton1Click:Connect(function()
    hubMode = not hubMode
    Hub.Visible = hubMode
    Exec.Visible = not hubMode
    ModeBtn.Text = hubMode and "Executor" or "Script Hub"
end)

RunService.RenderStepped:Connect(function() 
    Hub.CanvasSize = UDim2.new(0,0,0,Layout.AbsoluteContentSize.Y + 10) 
end)

-- DRAG CẢ GUI CHÍNH
local dragging = false
local dragInput = nil
local dragStart = nil
local startPos = nil

local function updateInput(input)
    if dragging then
        local delta = input.Position - dragStart
        MainFrame.Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X, startPos.Y.Scale, startPos.Y.Offset + delta.Y)
    end
end

MainFrame.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
        if input.Target == MainFrame or input.Target:IsDescendantOf(Title) then
            dragging = true
            dragStart = input.Position
            startPos = MainFrame.Position
        end
    end
end)

MainFrame.InputChanged:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch then
        dragInput = input
    end
end)

UserInputService.InputChanged:Connect(function(input)
    if input == dragInput and dragging then
        updateInput(input)
    end
end)

UserInputService.InputEnded:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
        dragging = false
    end
end)

-- Kéo ToggleButton
local togDrag = false
ToggleButton.InputBegan:Connect(function(i) 
    if i.UserInputType == Enum.UserInputType.MouseButton1 then 
        togDrag = true 
    end 
end)
ToggleButton.InputChanged:Connect(function(i) 
    if togDrag and i.UserInputType == Enum.UserInputType.MouseMovement then 
        ToggleButton.Position = UDim2.new(0,5,0,i.Position.Y-25) 
    end 
end)
UserInputService.InputEnded:Connect(function(i) 
    if i.UserInputType == Enum.UserInputType.MouseButton1 then 
        togDrag = false 
    end 
end)

-- Toggle GUI
local open = false
ToggleButton.MouseButton1Click:Connect(function()
    open = not open
    MainFrame.Visible = open
    ToggleButton.Text = open and "<<" or ">>"
end)

UserInputService.InputBegan:Connect(function(input, gameProcessed)
    if gameProcessed then return end
    if input.KeyCode == Enum.KeyCode.RightCurlyBracket then
        open = not open
        MainFrame.Visible = open
        ToggleButton.Text = open and "<<" or ">>"
    end
end)

print("oRitO Executor | Executor + Clear dịch lên gọn gàng - Hub giữ nguyên - đẹp như gốc! 🚀")
