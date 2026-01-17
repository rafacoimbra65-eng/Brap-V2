local ScreenGui = Instance.new("ScreenGui")
local MainFrame = Instance.new("Frame")
local UICorner = Instance.new("UICorner")
local Title = Instance.new("TextLabel")
local LoadingBarBackground = Instance.new("Frame")
local LoadingBarFill = Instance.new("Frame")
local StatusLabel = Instance.new("TextLabel")
local Blur = Instance.new("BlurEffect", game.Lighting)

-- Botão Persistente Brap
local BrapButton = Instance.new("TextButton")
local ButtonUICorner = Instance.new("UICorner")

-- Janela Admin (Estilo Windows)
local Window = Instance.new("Frame")
local WindowCorner = Instance.new("UICorner")
local TitleBar = Instance.new("Frame")
local TitleBarText = Instance.new("TextLabel")
local CloseBtn = Instance.new("TextButton")
local Content = Instance.new("ScrollingFrame")
local UIList = Instance.new("UIListLayout")

-- Configurações de exibição
ScreenGui.Parent = game.CoreGui
ScreenGui.Name = "BrapV2_Final"
Blur.Size = 0

-- --- INTERFACE DE LOADING ---
MainFrame.Name = "LoadingFrame"
MainFrame.Parent = ScreenGui
MainFrame.BackgroundColor3 = Color3.fromRGB(25, 25, 25)
MainFrame.Position = UDim2.new(0.5, -125, 0.5, -45)
MainFrame.Size = UDim2.new(0, 250, 0, 90)
UICorner.Parent = MainFrame

Title.Parent = MainFrame
Title.Text = "Brap V2"
Title.Font = Enum.Font.Code
Title.TextColor3 = Color3.fromRGB(255, 255, 255)
Title.TextSize = 18
Title.Size = UDim2.new(1, 0, 0.4, 0)
Title.BackgroundTransparency = 1

LoadingBarBackground.Parent = MainFrame
LoadingBarBackground.BackgroundColor3 = Color3.fromRGB(45, 45, 45)
LoadingBarBackground.Position = UDim2.new(0.1, 0, 0.5, 0)
LoadingBarBackground.Size = UDim2.new(0.8, 0, 0, 2)

LoadingBarFill.Parent = LoadingBarBackground
LoadingBarFill.BackgroundColor3 = Color3.fromRGB(0, 150, 255)
LoadingBarFill.Size = UDim2.new(0, 0, 1, 0)

StatusLabel.Parent = MainFrame
StatusLabel.Position = UDim2.new(0, 0, 0.6, 0)
StatusLabel.Size = UDim2.new(1, 0, 0.3, 0)
StatusLabel.Text = "Initializing..."
StatusLabel.TextColor3 = Color3.fromRGB(180, 180, 180)
StatusLabel.Font = Enum.Font.SourceSans
StatusLabel.TextSize = 14
StatusLabel.BackgroundTransparency = 1

-- --- JANELA ADMIN ---
Window.Name = "AdminWindow"
Window.Parent = ScreenGui
Window.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
Window.Position = UDim2.new(0.5, -150, 0.5, -100)
Window.Size = UDim2.new(0, 300, 0, 250)
Window.Visible = false
Window.Active = true
Window.Draggable = true -- Movível com o mouse

WindowCorner.CornerRadius = UDim.new(0, 6)
WindowCorner.Parent = Window

TitleBar.Parent = Window
TitleBar.BackgroundColor3 = Color3.fromRGB(45, 45, 45)
TitleBar.Size = UDim2.new(1, 0, 0, 25)

TitleBarText.Parent = TitleBar
TitleBarText.Text = " Brap V2 Admin"
TitleBarText.TextColor3 = Color3.fromRGB(255, 255, 255)
TitleBarText.Size = UDim2.new(0.8, 0, 1, 0)
TitleBarText.BackgroundTransparency = 1
TitleBarText.TextXAlignment = Enum.TextXAlignment.Left

CloseBtn.Parent = TitleBar
CloseBtn.Text = "X"
CloseBtn.BackgroundColor3 = Color3.fromRGB(150, 0, 0)
CloseBtn.Position = UDim2.new(1, -25, 0, 0)
CloseBtn.Size = UDim2.new(0, 25, 1, 0)
CloseBtn.MouseButton1Click:Connect(function() Window.Visible = false end)

Content.Parent = Window
Content.Position = UDim2.new(0, 5, 0, 30)
Content.Size = UDim2.new(1, -10, 1, -35)
Content.BackgroundTransparency = 1
Content.CanvasSize = UDim2.new(0, 0, 1.5, 0)

UIList.Parent = Content
UIList.Padding = UDim.new(0, 5)

-- --- FUNÇÕES E BOTÕES ---
local function CreateButton(txt, color, func)
    local b = Instance.new("TextButton", Content)
    b.Text = txt
    b.Size = UDim2.new(1, 0, 0, 35)
    b.BackgroundColor3 = color
    b.TextColor3 = Color3.fromRGB(255, 255, 255)
    Instance.new("UICorner", b)
    b.MouseButton1Click:Connect(func)
end

-- YEYBRIP (fly)
local flying = false
CreateButton("YEYBRIP (fly)", Color3.fromRGB(0, 150, 255), function()
    flying = not flying
    if flying then
        local p = game.Players.LocalPlayer
        local char = p.Character or p.CharacterAdded:Wait()
        local hrp = char:WaitForChild("HumanoidRootPart")
        local bv = Instance.new("BodyVelocity", hrp)
        bv.MaxForce = Vector3.new(math.huge, math.huge, math.huge)
        task.spawn(function()
            while flying do
                local cam = workspace.CurrentCamera
                local dir = Vector3.new(0,0,0)
                local uis = game:GetService("UserInputService")
                if uis:IsKeyDown(Enum.KeyCode.W) then dir = dir + cam.CFrame.LookVector end
                if uis:IsKeyDown(Enum.KeyCode.S) then dir = dir - cam.CFrame.LookVector end
                if uis:IsKeyDown(Enum.KeyCode.A) then dir = dir - cam.CFrame.RightVector end
                if uis:IsKeyDown(Enum.KeyCode.D) then dir = dir + cam.CFrame.RightVector end
                bv.Velocity = dir * 30
                task.wait()
            end
            bv:Destroy()
        end)
    end
end)

-- YEPBRAP (Console Local)
CreateButton("YEPBRAP (Console)", Color3.fromRGB(60, 60, 60), function()
    print("Brap V2: Console Ativado para Testes Locais.")
end)

-- YEPBREP (Infinite Yield)
CreateButton("YEPBREP (Inf Yield)", Color3.fromRGB(0, 100, 200), function()
    loadstring(game:HttpGet("https://raw.githubusercontent.com/EdgeIY/infiniteyield/master/source"))()
end)

-- YEPBROP (DEX)
CreateButton("YEPBROP (DEX Explorer)", Color3.fromRGB(0, 150, 100), function()
    loadstring(game:HttpGet("https://raw.githubusercontent.com/infyiff/backup/main/dex.lua"))()
end)

-- --- BOTÃO "B" PERSISTENTE ---
BrapButton.Name = "BrapButton"
BrapButton.Parent = ScreenGui
BrapButton.BackgroundColor3 = Color3.fromRGB(25, 25, 25)
BrapButton.Size = UDim2.new(0, 30, 0, 30)
BrapButton.Position = UDim2.new(1, -40, 0, 10)
BrapButton.Text = "B"
BrapButton.TextColor3 = Color3.fromRGB(0, 255, 255)
BrapButton.Visible = false
Instance.new("UICorner", BrapButton).CornerRadius = UDim.new(0, 4)

BrapButton.MouseButton1Click:Connect(function()
    Window.Visible = not Window.Visible
end)

-- --- LÓGICA DE CARREGAMENTO ---
local function Load()
    game:GetService("TweenService"):Create(Blur, TweenInfo.new(0.5), {Size = 20}):Play()
    local steps = {"Loading Brap V2...", "Bypassing Data...", "Setting Stats...", "Ready!"}
    for i, msg in ipairs(steps) do
        StatusLabel.Text = msg
        LoadingBarFill:TweenSize(UDim2.new(i/#steps, 0, 1, 0), "Out", "Linear", 0.4)
        wait(0.6)
    end
    wait(0.5)
    game:GetService("TweenService"):Create(Blur, TweenInfo.new(0.5), {Size = 0}):Play()
    MainFrame:Destroy()
    Blur:Destroy()
    BrapButton.Visible = true
end

coroutine.wrap(Load)()
