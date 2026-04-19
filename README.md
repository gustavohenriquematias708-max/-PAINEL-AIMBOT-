--[[ 
    👑 PAINEL DARK PREMIUM - REBORN EDITION
    - Nova Interface: ID 121980287187909
    - ESP Modernizado: Linhas Neon e Box Adaptativo
    - Botões: Estilo Minimalista Glossy
]]

local Players = game:GetService("Players")
local Player = Players.LocalPlayer
local Camera = workspace.CurrentCamera
local RunService = game:GetService("RunService")

-- Configurações Globais
getgenv().Aimbot_Lock = false
getgenv().Aimbot_Smooth = false
getgenv().ESP_Box = false
getgenv().ESP_Lines = false

local ScreenGui = Instance.new("ScreenGui", Player.PlayerGui)
ScreenGui.Name = "KZZ_REBORN_PANEL"
ScreenGui.ResetOnSpawn = false
ScreenGui.IgnoreGuiInset = true

-- 1. BASE PRINCIPAL
local MainFrame = Instance.new("Frame", ScreenGui)
MainFrame.Size = UDim2.new(0, 420, 0, 320)
MainFrame.Position = UDim2.new(0.5, -210, 0.5, -140)
MainFrame.BackgroundColor3 = Color3.fromRGB(15, 15, 15)
MainFrame.BorderSizePixel = 0
MainFrame.Active = true
MainFrame.Draggable = true
Instance.new("UICorner", MainFrame).CornerRadius = UDim.new(0, 10)

-- FUNDO PERSONALIZADO (ID NOVO)
local Bg = Instance.new("ImageLabel", MainFrame)
Bg.Size = UDim2.new(1, 0, 1, 0)
Bg.Image = "rbxassetid://121980287187909" -- Seu novo ID aplicado
Bg.ScaleType = Enum.ScaleType.Stretch
Bg.BackgroundTransparency = 0.1 
Bg.ZIndex = 1
Instance.new("UICorner", Bg).CornerRadius = UDim.new(0, 10)

-- OVERLAY ESCURO PARA MELHORAR LEITURA
local Overlay = Instance.new("Frame", MainFrame)
Overlay.Size = UDim2.new(1, 0, 1, 0)
Overlay.BackgroundColor3 = Color3.new(0,0,0)
Overlay.BackgroundTransparency = 0.4
Overlay.ZIndex = 2
Instance.new("UICorner", Overlay).CornerRadius = UDim.new(0, 10)

-- TÍTULO ESTILIZADO
local Title = Instance.new("TextLabel", MainFrame)
Title.Text = "SYSTEM REBORN v2"
Title.Size = UDim2.new(1, -100, 0, 40)
Title.Position = UDim2.new(0, 25, 0, 10)
Title.Font = Enum.Font.Ubuntu
Title.TextColor3 = Color3.fromRGB(255, 255, 255)
Title.TextSize = 18
Title.BackgroundTransparency = 1
Title.TextXAlignment = "Left"
Title.ZIndex = 5

-- BOTÕES SUPERIORES (X e -)
local function CreateHeaderBtn(txt, xOffset, color)
    local btn = Instance.new("TextButton", MainFrame)
    btn.Text = txt
    btn.Size = UDim2.new(0, 28, 0, 28)
    btn.Position = UDim2.new(1, xOffset, 0, 12)
    btn.BackgroundColor3 = color
    btn.BackgroundTransparency = 0.2
    btn.TextColor3 = Color3.new(1,1,1)
    btn.Font = Enum.Font.GothamBold
    btn.TextSize = 14
    btn.ZIndex = 6
    Instance.new("UICorner", btn).CornerRadius = UDim.new(0, 6)
    return btn
end
local CloseBtn = CreateHeaderBtn("✕", -40, Color3.fromRGB(150, 0, 0))
local MinBtn = CreateHeaderBtn("—", -75, Color3.fromRGB(40, 40, 40))

-- LISTA DE FUNÇÕES
local BtnContainer = Instance.new("ScrollingFrame", MainFrame)
BtnContainer.Size = UDim2.new(0, 370, 0, 220)
BtnContainer.Position = UDim2.new(0, 25, 0, 70)
BtnContainer.BackgroundTransparency = 1
BtnContainer.ZIndex = 5
BtnContainer.CanvasSize = UDim2.new(0, 0, 0, 250)
BtnContainer.ScrollBarThickness = 2

local Layout = Instance.new("UIListLayout", BtnContainer)
Layout.Padding = UDim.new(0, 10)

local function AddToggle(txt, var)
    local b = Instance.new("TextButton", BtnContainer)
    b.Size = UDim2.new(1, -10, 0, 40)
    b.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
    b.BackgroundTransparency = 0.5
    b.Text = "      " .. txt
    b.TextColor3 = Color3.fromRGB(200, 200, 200)
    b.Font = Enum.Font.Gotham
    b.TextSize = 13
    b.TextXAlignment = Enum.TextXAlignment.Left
    b.ZIndex = 6
    
    local Corner = Instance.new("UICorner", b)
    Corner.CornerRadius = UDim.new(0, 6)
    
    local Indicator = Instance.new("Frame", b)
    Indicator.Size = UDim2.new(0, 4, 1, 0)
    Indicator.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
    Indicator.BorderSizePixel = 0
    Indicator.BackgroundTransparency = 0.8

    b.MouseButton1Click:Connect(function()
        getgenv()[var] = not getgenv()[var]
        if getgenv()[var] then
            b.TextColor3 = Color3.fromRGB(255, 255, 255)
            b.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
            Indicator.BackgroundColor3 = Color3.fromRGB(0, 255, 150) -- Verde Neon ao ligar
            Indicator.BackgroundTransparency = 0
        else
            b.TextColor3 = Color3.fromRGB(200, 200, 200)
            b.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
            Indicator.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
            Indicator.BackgroundTransparency = 0.8
        end
    end)
end

AddToggle("AIMBOT LOCK (HARD)", "Aimbot_Lock")
AddToggle("AIMBOT SMOOTH (LEGIT)", "Aimbot_Smooth")
AddToggle("ESP BOX NEON", "ESP_Box")
AddToggle("ESP TRACER (BELLY)", "ESP_Lines")

-- BOTÃO FLUTUANTE (NINJA)
local Floating = Instance.new("ImageButton", ScreenGui)
Floating.Size = UDim2.new(0, 60, 0, 60)
Floating.Position = UDim2.new(0.02, 0, 0.4, 0)
Floating.Image = "rbxassetid://121980287187909"
Floating.Visible = false
Floating.Draggable = true
Instance.new("UICorner", Floating).CornerRadius = UDim.new(1, 0)
Instance.new("UIStroke", Floating).Thickness = 2

MinBtn.MouseButton1Click:Connect(function() MainFrame.Visible = false Floating.Visible = true end)
Floating.MouseButton1Click:Connect(function() MainFrame.Visible = true Floating.Visible = false end)
CloseBtn.MouseButton1Click:Connect(function() ScreenGui:Destroy() end)

-- LÓGICA ESP (MELHORADA)
local function CreateESP(p)
    local function Update()
        local conn
        conn = RunService.RenderStepped:Connect(function()
            if not p.Parent then conn:Disconnect() return end
            
            if p.Character and p.Character:FindFirstChild("HumanoidRootPart") and p.Character:FindFirstChild("Humanoid") and p.Character.Humanoid.Health > 0 then
                local hrp = p.Character.HumanoidRootPart
                
                -- BOX ESP (GRADIENTE)
                local box = hrp:FindFirstChild("REBORN_Box") or Instance.new("BillboardGui", hrp)
                box.Name = "REBORN_Box"; box.AlwaysOnTop = true; box.Size = UDim2.new(4.5, 0, 6, 0)
                box.Enabled = getgenv().ESP_Box
                
                local frame = box:FindFirstChild("Main") or Instance.new("Frame", box)
                frame.Name = "Main"; frame.Size = UDim2.new(1,0,1,0); frame.BackgroundTransparency = 1
                local stroke = frame:FindFirstChild("Outline") or Instance.new("UIStroke", frame)
                stroke.Name = "Outline"; stroke.Thickness = 1.5; stroke.Color = Color3.fromRGB(0, 255, 200)

                -- LINHAS (TRACERS NA BARRIGA)
                local beam = hrp:FindFirstChild("REBORN_Beam") or Instance.new("Beam", hrp)
                beam.Name = "REBORN_Beam"
                beam.Width0 = 0.05; beam.Width1 = 0.05
                beam.Transparency = NumberSequence.new(0.3)
                beam.FaceCamera = true
                beam.Color = ColorSequence.new(Color3.fromRGB(255, 255, 255))
                beam.Enabled = getgenv().ESP_Lines

                local att0 = hrp:FindFirstChild("Att0") or Instance.new("Attachment", hrp)
                att0.Name = "Att0"; att0.Position = Vector3.new(0,0,0)
                
                local myHrp = Player.Character and Player.Character:FindFirstChild("HumanoidRootPart")
                if myHrp then
                    local att1 = myHrp:FindFirstChild("AttBase") or Instance.new("Attachment", myHrp)
                    att1.Name = "AttBase"; att1.Position = Vector3.new(0, -3, 0)
                    beam.Attachment0 = att0
                    beam.Attachment1 = att1
                end
            end
        end)
    end
    Update()
end

-- AIMBOT LÓGICA
local function GetClosest()
    local t, d = nil, 500
    for _, v in pairs(Players:GetPlayers()) do
        if v ~= Player and v.Character and v.Character:FindFirstChild("HumanoidRootPart") and v.Character.Humanoid.Health > 0 then
            local pos, vis = Camera:WorldToViewportPoint(v.Character.HumanoidRootPart.Position)
            if vis then
                local mag = (Vector2.new(pos.X, pos.Y) - Vector2.new(Camera.ViewportSize.X/2, Camera.ViewportSize.Y/2)).Magnitude
                if mag < d then d = mag; t = v.Character.HumanoidRootPart end
            end
        end
    end
    return t
end

RunService.RenderStepped:Connect(function()
    local target = GetClosest()
    if target then
        if getgenv().Aimbot_Lock then 
            Camera.CFrame = CFrame.new(Camera.CFrame.Position, target.Position)
        elseif getgenv().Aimbot_Smooth then 
            Camera.CFrame = Camera.CFrame:Lerp(CFrame.new(Camera.CFrame.Position, target.Position), 0.1) 
        end
    end
end)

-- INICIAR
for _, p in pairs(Players:GetPlayers()) do if p ~= Player then CreateESP(p) end end
Players.PlayerAdded:Connect(function(p) if p ~= Player then CreateESP(p) end end)
