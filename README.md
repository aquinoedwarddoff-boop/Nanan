-- Edward Script - Batata Hub
local RS = game:GetService("RunService")
local Players = game:GetService("Players")
local TS = game:GetService("TweenService")

local plr = Players.LocalPlayer

-- AGUARDAR PLAYER CARREGAR
repeat task.wait() until plr.Character

local vooOn, espOn = false, false
local posSalva = nil

print("🥔 Iniciando loading...")

-- LOADING COM GUERRA DE BATATAS E AVIÃO (TELA PRETA)
local sg = Instance.new("ScreenGui")
sg.Name = "EdwardLoading"
sg.IgnoreGuiInset = true
sg.ResetOnSpawn = false
sg.DisplayOrder = 10
sg.Parent = plr:WaitForChild("PlayerGui")

print("🥔 ScreenGui criado")

-- TELA PRETA COMPLETA
local bg = Instance.new("Frame")
bg.Name = "TelaPreteTotal"
bg.Size = UDim2.new(1,0,1,0)
bg.Position = UDim2.new(0,0,0,0)
bg.BackgroundColor3 = Color3.new(0,0,0)
bg.BorderSizePixel = 0
bg.ZIndex = 1
bg.Parent = sg

print("🥔 Tela preta criada")

-- GUERRA DE BATATAS (10 segundos)
print("⚔️ Iniciando guerra de batatas...")

local batatas = {}

for i = 1, 8 do
    local batata = Instance.new("TextLabel")
    batata.Size = UDim2.new(0,70,0,70)
    batata.Position = UDim2.new(math.random(0,10)/10, 0, -0.15, 0)
    batata.BackgroundTransparency = 1
    batata.Text = "🥔"
    batata.TextSize = 55
    batata.Font = Enum.Font.GothamBold
    batata.Rotation = math.random(0,360)
    batata.ZIndex = 2
    batata.Parent = bg
    table.insert(batatas, batata)
    
    print("🥔 Batata " .. i .. " criada")
    
    task.spawn(function()
        local endY = math.random(4,8)/10
        local duration = math.random(15,25)/10
        
        local tween = TS:Create(batata, TweenInfo.new(duration, Enum.EasingStyle.Bounce, Enum.EasingDirection.In), {
            Position = UDim2.new(math.random(0,10)/10, 0, endY, 0),
            Rotation = math.random(360,720)
        })
        tween:Play()
        
        task.wait(duration)
        batata.Text = "💥"
        batata.TextSize = 80
        task.wait(0.4)
        TS:Create(batata, TweenInfo.new(0.3), {TextTransparency = 1}):Play()
    end)
end

-- TÍTULO "GUERRA DE BATATAS"
local titulo = Instance.new("TextLabel")
titulo.Size = UDim2.new(0,700,0,120)
titulo.Position = UDim2.new(0.5,-350,0.5,-60)
titulo.BackgroundTransparency = 1
titulo.Text = "⚔️ GUERRA DE BATATAS ⚔️"
titulo.TextColor3 = Color3.fromRGB(255,80,0)
titulo.TextSize = 48
titulo.Font = Enum.Font.GothamBold
titulo.TextStrokeTransparency = 0
titulo.TextStrokeColor3 = Color3.new(0,0,0)
titulo.ZIndex = 5
titulo.Parent = bg

print("⚔️ Título criado")

-- PISCAR TÍTULO
task.spawn(function()
    for i = 1, 6 do
        TS:Create(titulo, TweenInfo.new(0.4), {TextTransparency = 0.6}):Play()
        task.wait(0.4)
        TS:Create(titulo, TweenInfo.new(0.4), {TextTransparency = 0}):Play()
        task.wait(0.4)
    end
end)

-- EXPLOSÕES ALEATÓRIAS
task.spawn(function()
    for i = 1, 12 do
        task.wait(0.7)
        local boom = Instance.new("TextLabel")
        boom.Size = UDim2.new(0,120,0,120)
        boom.Position = UDim2.new(math.random(1,9)/10, 0, math.random(2,8)/10, 0)
        boom.BackgroundTransparency = 1
        boom.Text = "💥"
        boom.TextSize = 70
        boom.TextTransparency = 0
        boom.ZIndex = 3
        boom.Parent = bg
        
        TS:Create(boom, TweenInfo.new(0.6), {TextTransparency = 1, TextSize = 110}):Play()
        task.delay(0.6, function() boom:Destroy() end)
    end
end)

print("⚔️ Aguardando 10 segundos de guerra...")
task.wait(10)

-- FADE OUT GUERRA
print("⚔️ Fade out guerra...")
for _, batata in pairs(batatas) do
    TS:Create(batata, TweenInfo.new(0.5), {TextTransparency = 1}):Play()
end
TS:Create(titulo, TweenInfo.new(0.5), {TextTransparency = 1}):Play()
task.wait(0.6)

-- AVIÃO COM FAIXA "EDWARD SCRIPT"
print("✈️ Avião entrando...")

local aviao = Instance.new("TextLabel")
aviao.Size = UDim2.new(0,120,0,120)
aviao.Position = UDim2.new(-0.2,0,0.35,0)
aviao.BackgroundTransparency = 1
aviao.Text = "✈️"
aviao.TextSize = 90
aviao.Font = Enum.Font.GothamBold
aviao.Rotation = -10
aviao.ZIndex = 4
aviao.Parent = bg

local faixa = Instance.new("TextLabel")
faixa.Size = UDim2.new(0,500,0,80)
faixa.Position = UDim2.new(-0.6,0,0.38,0)
faixa.BackgroundTransparency = 1
faixa.Text = "EDWARD SCRIPT"
faixa.TextColor3 = Color3.fromRGB(255,215,0)
faixa.TextSize = 42
faixa.Font = Enum.Font.GothamBold
faixa.TextStrokeTransparency = 0
faixa.TextStrokeColor3 = Color3.new(0,0,0)
faixa.ZIndex = 4
faixa.Parent = bg

local rastro = Instance.new("TextLabel")
rastro.Size = UDim2.new(0,300,0,60)
rastro.Position = UDim2.new(-0.3,0,0.36,0)
rastro.BackgroundTransparency = 1
rastro.Text = "- - - - - - - - - -"
rastro.TextColor3 = Color3.fromRGB(180,180,180)
rastro.TextSize = 30
rastro.TextTransparency = 0.4
rastro.ZIndex = 3
rastro.Parent = bg

-- ANIMAR AVIÃO
TS:Create(aviao, TweenInfo.new(4.5, Enum.EasingStyle.Linear), {Position = UDim2.new(1.25,0,0.35,0)}):Play()
TS:Create(faixa, TweenInfo.new(4.5, Enum.EasingStyle.Linear), {Position = UDim2.new(1.15,0,0.38,0)}):Play()
TS:Create(rastro, TweenInfo.new(4.5, Enum.EasingStyle.Linear), {Position = UDim2.new(1.3,0,0.36,0)}):Play()

print("✈️ Avião voando...")
task.wait(4.5)

-- FADE OUT FINAL
print("🌟 Fade out final...")
TS:Create(bg, TweenInfo.new(0.7), {BackgroundTransparency = 1}):Play()
TS:Create(aviao, TweenInfo.new(0.7), {TextTransparency = 1}):Play()
TS:Create(faixa, TweenInfo.new(0.7), {TextTransparency = 1}):Play()
TS:Create(rastro, TweenInfo.new(0.7), {TextTransparency = 1}):Play()
task.wait(0.8)

sg:Destroy()
print("✅ Loading completo!")

-- Pequena pausa antes de carregar interface
task.wait(0.5)

-- GUI
local sg = Instance.new("ScreenGui", plr.PlayerGui)
sg.Name = "batata_hub"
sg.ResetOnSpawn = false

local batataBtn = Instance.new("TextButton", sg)
batataBtn.Size = UDim2.new(0,60,0,60)
batataBtn.Position = UDim2.new(0.5,-30,0.1,0)
batataBtn.BackgroundColor3 = Color3.fromRGB(30,30,35)
batataBtn.Text = "🥔"
batataBtn.TextSize = 35
batataBtn.Active = true
batataBtn.Draggable = true
batataBtn.Visible = false
Instance.new("UICorner", batataBtn).CornerRadius = UDim.new(1,0)

local batataStroke = Instance.new("UIStroke", batataBtn)
batataStroke.Color = Color3.fromRGB(0,200,255)
batataStroke.Thickness = 3

local main = Instance.new("Frame", sg)
main.Size = UDim2.new(0,220,0,240)
main.Position = UDim2.new(0.5,-110,0.5,-120)
main.BackgroundColor3 = Color3.fromRGB(20,20,25)
main.Active = true
main.Draggable = true
main.BackgroundTransparency = 0.1
Instance.new("UICorner", main).CornerRadius = UDim.new(0,12)

local mainStroke = Instance.new("UIStroke", main)
mainStroke.Color = Color3.fromRGB(0,200,255)
mainStroke.Thickness = 2

local header = Instance.new("Frame", main)
header.Size = UDim2.new(1,0,0,35)
header.BackgroundColor3 = Color3.fromRGB(15,15,20)
Instance.new("UICorner", header).CornerRadius = UDim.new(0,12)

local iconeBatata = Instance.new("TextLabel", header)
iconeBatata.Size = UDim2.new(0,30,0,30)
iconeBatata.Position = UDim2.new(0,8,0,2)
iconeBatata.BackgroundTransparency = 1
iconeBatata.Text = "☠️"
iconeBatata.TextSize = 20
iconeBatata.Font = Enum.Font.GothamBold

local top = Instance.new("TextLabel", header)
top.Size = UDim2.new(1,-80,1,0)
top.Position = UDim2.new(0,40,0,0)
top.BackgroundTransparency = 1
top.Text = "batata hub"
top.TextColor3 = Color3.fromRGB(0,200,255)
top.TextSize = 14
top.Font = Enum.Font.GothamBold
top.TextXAlignment = Enum.TextXAlignment.Left

local btnFechar = Instance.new("TextButton", header)
btnFechar.Size = UDim2.new(0,30,0,30)
btnFechar.Position = UDim2.new(1,-35,0,2)
btnFechar.BackgroundColor3 = Color3.fromRGB(220,50,50)
btnFechar.Text = "×"
btnFechar.TextColor3 = Color3.new(1,1,1)
btnFechar.TextSize = 22
btnFechar.Font = Enum.Font.GothamBold
Instance.new("UICorner", btnFechar).CornerRadius = UDim.new(0,6)

local abaAberta = true
btnFechar.MouseButton1Click:Connect(function()
    abaAberta = false
    main.Visible = false
    batataBtn.Visible = true
end)

batataBtn.MouseButton1Click:Connect(function()
    abaAberta = true
    main.Visible = true
    batataBtn.Visible = false
end)

local function btn(txt, y, col)
    local b = Instance.new("TextButton", main)
    b.Size = UDim2.new(0.9,0,0,40)
    b.Position = UDim2.new(0.05,0,0,y)
    b.BackgroundColor3 = col
    b.Text = txt
    b.TextColor3 = Color3.new(1,1,1)
    b.TextSize = 13
    b.Font = Enum.Font.GothamBold
    b.BackgroundTransparency = 0.15
    Instance.new("UICorner", b).CornerRadius = UDim.new(0,8)
    
    local stroke = Instance.new("UIStroke", b)
    stroke.Color = Color3.fromRGB(0,200,255)
    stroke.Thickness = 1
    stroke.Transparency = 0.7
    
    return b
end

local b1 = btn("🚀 VOO", 45, Color3.fromRGB(30,30,40))
local b2 = btn("👁 ESP", 95, Color3.fromRGB(30,30,40))
local b3 = btn("📍 SAVE", 145, Color3.fromRGB(30,30,40))
local b4 = btn("✈ GO", 195, Color3.fromRGB(30,30,40))

-- VOO
local vooConn = nil
b1.MouseButton1Click:Connect(function()
    vooOn = not vooOn
    if vooOn then
        b1.Text = "✅ VOO ATIVO"
        b1.BackgroundColor3 = Color3.fromRGB(50,200,50)
        
        vooConn = RS.Heartbeat:Connect(function()
            local char = plr.Character
            if not char or not vooOn then return end
            local r = char:FindFirstChild("HumanoidRootPart")
            if r then
                local cam = workspace.CurrentCamera
                local vel = cam.CFrame.LookVector * 26
                pcall(function()
                    r.Velocity = vel
                end)
            end
        end)
    else
        b1.Text = "🚀 VOO"
        b1.BackgroundColor3 = Color3.fromRGB(30,30,40)
        if vooConn then vooConn:Disconnect() end
    end
end)

-- ESP
b2.MouseButton1Click:Connect(function()
    espOn = not espOn
    if espOn then
        b2.Text = "✅ ESP ATIVO"
        b2.BackgroundColor3 = Color3.fromRGB(50,200,50)
    else
        b2.Text = "👁 ESP"
        b2.BackgroundColor3 = Color3.fromRGB(30,30,40)
        for _,p in pairs(Players:GetPlayers()) do
            if p~=plr and p.Character then
                for _,v in pairs(p.Character:GetDescendants()) do
                    if v:IsA("Highlight") then v:Destroy() end
                end
            end
        end
    end
end)

-- SALVAR
b3.MouseButton1Click:Connect(function()
    local char = plr.Character
    if not char then return end
    local r = char:FindFirstChild("HumanoidRootPart")
    if r then
        posSalva = r.Position
        b3.Text = "✅ SALVO"
        b3.BackgroundColor3 = Color3.fromRGB(50,200,50)
        task.wait(1.5)
        b3.Text = "📍 SAVE"
        b3.BackgroundColor3 = Color3.fromRGB(30,30,40)
    end
end)

-- FLUTUAR
local flutuando = false
local flutuarConn = nil
b4.MouseButton1Click:Connect(function()
    if not posSalva then return end
    
    flutuando = not flutuando
    if flutuando then
        b4.Text = "⏳ INDO..."
        b4.BackgroundColor3 = Color3.fromRGB(255,165,0)
        
        local posAlvo = posSalva + Vector3.new(0, 5, 0)
        
        flutuarConn = RS.Heartbeat:Connect(function()
            if not flutuando then return end
            local char = plr.Character
            if not char then return end
            local r = char:FindFirstChild("HumanoidRootPart")
            if not r then return end
            
            local dist = (posAlvo - r.Position).Magnitude
            if dist < 3 then
                flutuando = false
                if flutuarConn then flutuarConn:Disconnect() end
                b4.Text = "✅ CHEGOU"
                b4.BackgroundColor3 = Color3.fromRGB(50,200,50)
                task.wait(1.5)
                b4.Text = "✈ GO"
                b4.BackgroundColor3 = Color3.fromRGB(30,30,40)
            else
                local dir = (posAlvo - r.Position).Unit
                pcall(function()
                    r.Velocity = dir * 28
                end)
            end
        end)
    else
        b4.Text = "✈ GO"
        b4.BackgroundColor3 = Color3.fromRGB(30,30,40)
        if flutuarConn then flutuarConn:Disconnect() end
    end
end)

-- ESP LOOP
task.spawn(function()
    while task.wait(0.5) do
        if espOn then
            for _,p in pairs(Players:GetPlayers()) do
                if p~=plr and p.Character and not p.Character:FindFirstChild("Highlight") then
                    pcall(function()
                        local h = Instance.new("Highlight", p.Character)
                        h.FillColor = Color3.fromRGB(255,0,0)
                        h.FillTransparency = 0.6
                        h.OutlineTransparency = 0.3
                    end)
                end
            end
        end
    end
end)

print("✅ Edward Script carregado!")
