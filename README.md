-- ============================================
-- SCRIPT STORAGE HUNTERS - AUTO FARM
-- Compatível com Arceus X, Delta, CodeX, etc.
-- ============================================

local player = game.Players.LocalPlayer
local gui = Instance.new("ScreenGui")
gui.Name = "StorageHunterGUI"
gui.Parent = player.PlayerGui

-- ====== INTERFACE PRINCIPAL ======
local mainFrame = Instance.new("Frame")
mainFrame.Size = UDim2.new(0, 400, 0, 550)
mainFrame.Position = UDim2.new(0.5, -200, 0.5, -275)
mainFrame.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
mainFrame.BackgroundTransparency = 0.05
mainFrame.BorderColor3 = Color3.fromRGB(200, 200, 200)
mainFrame.BorderSizePixel = 1
mainFrame.ClipsDescendants = true
mainFrame.Parent = gui

-- Sombra
local shadow = Instance.new("ImageLabel")
shadow.Size = UDim2.new(1, 20, 1, 20)
shadow.Position = UDim2.new(0, -10, 0, -10)
shadow.BackgroundTransparency = 1
shadow.Image = "rbxassetid://1316043626"
shadow.ImageColor3 = Color3.fromRGB(0, 0, 0)
shadow.ImageTransparency = 0.5
shadow.ZIndex = 0
shadow.Parent = mainFrame

-- ====== TÍTULO ======
local title = Instance.new("TextLabel")
title.Size = UDim2.new(1, 0, 0, 45)
title.BackgroundTransparency = 1
title.Text = "⚡ STORAGE HUNTER - AUTO"
title.TextColor3 = Color3.fromRGB(40, 40, 40)
title.TextSize = 20
title.Font = Enum.Font.GothamBold
title.Parent = mainFrame

-- ====== BOTÃO FECHAR ======
local closeBtn = Instance.new("TextButton")
closeBtn.Size = UDim2.new(0, 30, 0, 30)
closeBtn.Position = UDim2.new(1, -40, 0, 8)
closeBtn.BackgroundTransparency = 1
closeBtn.Text = "✕"
closeBtn.TextColor3 = Color3.fromRGB(150, 150, 150)
closeBtn.TextSize = 20
closeBtn.Font = Enum.Font.Gotham
closeBtn.Parent = mainFrame

closeBtn.MouseButton1Click:Connect(function()
    gui.Enabled = false
end)

-- ====== SCROLLING FRAME ======
local scrollFrame = Instance.new("ScrollingFrame")
scrollFrame.Size = UDim2.new(1, -20, 1, -60)
scrollFrame.Position = UDim2.new(0, 10, 0, 50)
scrollFrame.BackgroundTransparency = 1
scrollFrame.ScrollBarThickness = 4
scrollFrame.CanvasSize = UDim2.new(0, 0, 0, 700)
scrollFrame.Parent = mainFrame

-- Função para criar Label
local function createLabel(parent, text, yPos, color)
    local label = Instance.new("TextLabel")
    label.Size = UDim2.new(1, 0, 0, 25)
    label.Position = UDim2.new(0, 0, 0, yPos)
    label.BackgroundTransparency = 1
    label.Text = text
    label.TextColor3 = color or Color3.fromRGB(60, 60, 60)
    label.TextSize = 14
    label.Font = Enum.Font.Gotham
    label.TextXAlignment = Enum.TextXAlignment.Left
    label.Parent = parent
    return label
end

-- Função para criar TextBox
local function createTextBox(parent, defaultText, yPos, width)
    local box = Instance.new("TextBox")
    box.Size = UDim2.new(width or 0.5, 0, 0, 30)
    box.Position = UDim2.new(0.5, -10, 0, yPos)
    box.BackgroundColor3 = Color3.fromRGB(245, 245, 245)
    box.BorderColor3 = Color3.fromRGB(200, 200, 200)
    box.BorderSizePixel = 1
    box.Text = tostring(defaultText)
    box.TextColor3 = Color3.fromRGB(50, 50, 50)
    box.TextSize = 14
    box.Font = Enum.Font.Gotham
    box.Parent = parent
    return box
end

-- Função para criar Toggle
local function createToggle(parent, labelText, yPos, defaultValue)
    local label = Instance.new("TextLabel")
    label.Size = UDim2.new(0.6, 0, 0, 30)
    label.Position = UDim2.new(0, 0, 0, yPos)
    label.BackgroundTransparency = 1
    label.Text = labelText
    label.TextColor3 = Color3.fromRGB(60, 60, 60)
    label.TextSize = 14
    label.Font = Enum.Font.Gotham
    label.TextXAlignment = Enum.TextXAlignment.Left
    label.Parent = parent
    
    local btn = Instance.new("TextButton")
    btn.Size = UDim2.new(0, 60, 0, 28)
    btn.Position = UDim2.new(0.7, 0, 0, yPos)
    btn.BackgroundColor3 = defaultValue and Color3.fromRGB(76, 175, 80) or Color3.fromRGB(200, 200, 200)
    btn.BorderColor3 = Color3.fromRGB(180, 180, 180)
    btn.BorderSizePixel = 1
    btn.Text = defaultValue and "ON" or "OFF"
    btn.TextColor3 = Color3.fromRGB(255, 255, 255)
    btn.TextSize = 12
    btn.Font = Enum.Font.GothamBold
    btn.Parent = parent
    
    btn.MouseButton1Click:Connect(function()
        local isOn = btn.Text == "ON"
        btn.Text = isOn and "OFF" or "ON"
        btn.BackgroundColor3 = isOn and Color3.fromRGB(200, 200, 200) or Color3.fromRGB(76, 175, 80)
    end)
    
    return btn
end

-- ====== CONFIGURAÇÕES ======
local y = 10

-- Valor Mínimo
createLabel(scrollFrame, "💎 VALOR MÍNIMO PARA ABRIR:", y)
local minBox = createTextBox(scrollFrame, "2000", y + 25)

y = y + 65
createLabel(scrollFrame, "💰 VALOR MÁXIMO PARA ABRIR:", y)
local maxBox = createTextBox(scrollFrame, "100000", y + 25)

y = y + 65
createLabel(scrollFrame, "🎯 VALOR MÍNIMO PARA VENDER:", y)
local sellMinBox = createTextBox(scrollFrame, "500", y + 25)

y = y + 65
createLabel(scrollFrame, "📝 ITEM DE BYPASS (nome exato):", y)
local bypassBox = createTextBox(scrollFrame, "Ex: Golden Egg", y + 25)

y = y + 65
createLabel(scrollFrame, "🚫 ITEM NUNCA VENDER (nome):", y)
local neverSellBox = createTextBox(scrollFrame, "Ex: Vehicle", y + 25)

-- Toggles
y = y + 70
local autoPickup = createToggle(scrollFrame, "📦 Auto-Pickup", y, true)
y = y + 40
local autoSell = createToggle(scrollFrame, "💰 Auto-Sell", y, true)
y = y + 40
local autoGrade = createToggle(scrollFrame, "🧹 Auto-Grade", y, true)
y = y + 40
local autoFreeze = createToggle(scrollFrame, "❄️ Auto-Congelar NPCs", y, false)
y = y + 40
local autoOpen = createToggle(scrollFrame, "🔓 Auto-Abrir Containers", y, true)

-- ====== BOTÃO SALVAR ======
y = y + 55
local saveBtn = Instance.new("TextButton")
saveBtn.Size = UDim2.new(0, 180, 0, 40)
saveBtn.Position = UDim2.new(0.5, -90, 0, y)
saveBtn.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
saveBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
saveBtn.Text = "💾 SALVAR CONFIG"
saveBtn.TextSize = 15
saveBtn.Font = Enum.Font.GothamBold
saveBtn.Parent = scrollFrame

-- ====== BOTÃO ATIVAR ======
y = y + 55
local startBtn = Instance.new("TextButton")
startBtn.Size = UDim2.new(0, 180, 0, 45)
startBtn.Position = UDim2.new(0.5, -90, 0, y)
startBtn.BackgroundColor3 = Color3.fromRGB(76, 175, 80)
startBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
startBtn.Text = "▶️ INICIAR AUTO FARM"
startBtn.TextSize = 16
startBtn.Font = Enum.Font.GothamBold
startBtn.Parent = scrollFrame

-- ====== STATUS ======
y = y + 60
local statusLabel = Instance.new("TextLabel")
statusLabel.Size = UDim2.new(1, 0, 0, 30)
statusLabel.Position = UDim2.new(0, 0, 0, y)
statusLabel.BackgroundTransparency = 1
statusLabel.Text = "🟢 Status: Aguardando..."
statusLabel.TextColor3 = Color3.fromRGB(60, 60, 60)
statusLabel.TextSize = 14
statusLabel.Font = Enum.Font.Gotham
statusLabel.Parent = scrollFrame

-- ====== VARIÁVEIS DO SCRIPT ======
local config = {
    minValue = 2000,
    maxValue = 100000,
    sellMinValue = 500,
    bypassItems = {},
    neverSellItems = {},
    autoPickup = true,
    autoSell = true,
    autoGrade = true,
    autoFreeze = false,
    autoOpen = true
}

local running = false
local containers = {}

-- ====== FUNÇÃO PARA ENCONTRAR CONTAINERS ======
local function FindContainers()
    local found = {}
    for _, obj in ipairs(workspace:GetChildren()) do
        -- Procura por containers no jogo Storage Hunters
        if obj:IsA("Model") and obj:FindFirstChild("Price") then
            local price = obj.Price.Value
            local name = obj.Name
            local area = obj:FindFirstChild("Area") and obj.Area.Value or "Desconhecida"
            local isOpened = obj:FindFirstChild("Opened") and obj.Opened.Value or false
            
            table.insert(found, {
                Object = obj,
                Name = name,
                Price = price,
                Area = area,
                IsOpened = isOpened
            })
        end
    end
    return found
end

-- ====== FUNÇÃO PARA CONGELAR NPCS ======
local function FreezeNPCs(container)
    for _, npc in ipairs(workspace:GetChildren()) do
        if npc:IsA("Model") and npc:FindFirstChild("Humanoid") then
            if (npc.HumanoidRootPart.Position - container.Position).Magnitude < 50 then
                npc.Humanoid.WalkSpeed = 0
                task.delay(10, function()
                    if npc and npc.Parent then
                        npc.Humanoid.WalkSpeed = 16
                    end
                end)
            end
        end
    end
end

-- ====== FUNÇÃO PARA PEGAR ITENS ======
local function AutoGradeItems(container)
    local playerChar = player.Character
    if not playerChar then return end
    
    for _, item in ipairs(workspace:GetChildren()) do
        if (item:IsA("Tool") or item:IsA("Part")) and item.Parent ~= player then
            if item:IsA("Tool") and item:FindFirstChild("Handle") then
                if (item.Handle.Position - container.Position).Magnitude < 30 then
                    item.Parent = player.Backpack
                end
            end
        end
    end
end

-- ====== FUNÇÃO PARA VENDER ITENS ======
local function AutoSellItems()
    local inventory = player.Backpack:GetChildren()
    local totalSold = 0
    
    for _, item in ipairs(inventory) do
        if item:IsA("Tool") then
            local itemName = item.Name
            
            -- Verifica se é item de Bypass (NUNCA vende)
            local isBypass = false
            for _, bypass in ipairs(config.bypassItems) do
                if itemName:find(bypass) then
                    isBypass = true
                    break
                end
            end
            
            -- Verifica se é item "Nunca Vender"
            local isNeverSell = false
            for _, never in ipairs(config.neverSellItems) do
                if itemName:find(never) then
                    isNeverSell = true
                    break
                end
            end
            
            -- Se for Bypass ou NeverSell, não vende
            if isBypass or isNeverSell then
                continue
            end
            
            -- Pega o valor do item
            local itemValue = item:GetAttribute("Value") or 0
            
            -- Vende se for maior que o valor mínimo
            if itemValue >= config.sellMinValue then
                totalSold = totalSold + itemValue
                item:Destroy()
            end
        end
    end
    
    if totalSold > 0 then
        statusLabel.Text = "💰 Vendeu: $" .. totalSold
    end
end

-- ====== FUNÇÃO PARA ABRIR CONTAINER ======
local function OpenContainer(containerObj)
    if not containerObj or not containerObj.Parent then return false end
    
    -- Verifica se já foi aberto
    if containerObj:FindFirstChild("Opened") and containerObj.Opened.Value then
        return false
    end
    
    local price = containerObj.Price.Value
    
    -- Verifica se está dentro do valor mínimo/máximo
    if price < config.minValue or price > config.maxValue then
        return false
    end
    
    -- Verifica itens de Bypass
    local hasBypass = false
    for _, child in ipairs(containerObj:GetChildren()) do
        if child:IsA("Tool") then
            for _, bypass in ipairs(config.bypassItems) do
                if child.Name:find(bypass) then
                    hasBypass = true
                    break
                end
            end
        end
    end
    
    -- Se não tiver Bypass e for menor que o mínimo, não abre
    if not hasBypass and price < config.minValue then
        return false
    end
    
    -- Auto-Freeze
    if config.autoFreeze and containerObj.PrimaryPart then
        FreezeNPCs(containerObj.PrimaryPart)
    end
    
    -- Tenta abrir o container (CLICK)
    local clickDetector = containerObj:FindFirstChildWhichIsA("ClickDetector")
    if clickDetector then
        clickDetector:FireClick(player)
        statusLabel.Text = "📦 Abrindo: " .. containerObj.Name
    else
        -- Tenta clicar na parte principal
        local primaryPart = containerObj.PrimaryPart or containerObj:FindFirstChild("Handle")
        if primaryPart then
            -- Simula clique
            game:GetService("VirtualInputManager"):SendMouseButtonEvent(primaryPart.Position, 1, true)
            task.wait(0.1)
            game:GetService("VirtualInputManager"):SendMouseButtonEvent(primaryPart.Position, 1, false)
        end
    end
    
    task.wait(1)
    
    -- Auto-Grade
    if config.autoGrade and containerObj.PrimaryPart then
        AutoGradeItems(containerObj.PrimaryPart)
    end
    
    -- Auto-Pickup (Bypass)
    if config.autoPickup then
        for _, item in ipairs(containerObj:GetChildren()) do
            if item:IsA("Tool") then
                for _, bypass in ipairs(config.bypassItems) do
                    if item.Name:find(bypass) then
                        item.Parent = player.Backpack
                        statusLabel.Text = "⭐ Bypass: " .. item.Name
                        break
                    end
                end
            end
        end
    end
    
    -- Auto-Sell
    if config.autoSell then
        task.wait(1.5)
        AutoSellItems()
    end
    
    -- Marca como aberto
    if containerObj:FindFirstChild("Opened") then
        containerObj.Opened.Value = true
    end
    
    return true
end

-- ====== LOOP PRINCIPAL ======
local function MainLoop()
    while running do
        local found = FindContainers()
        
        -- Ordena por preço (menor primeiro)
        table.sort(found, function(a, b)
            return a.Price < b.Price
        end)
        
        -- Procura um container para abrir
        for _, containerData in ipairs(found) do
            if not containerData.IsOpened then
                local success = OpenContainer(containerData.Object)
                if success then
                    break -- Sai depois de abrir um
                end
                task.wait(0.5)
            end
        end
        
        task.wait(2)
    end
end

-- ====== EVENTOS DOS BOTÕES ======

-- Salvar Configurações
saveBtn.MouseButton1Click:Connect(function()
    config.minValue = tonumber(minBox.Text) or 2000
    config.maxValue = tonumber(maxBox.Text) or 100000
    config.sellMinValue = tonumber(sellMinBox.Text) or 500
    
    -- Bypass Items
    local bypassText = bypassBox.Text
    config.bypassItems = {}
    if bypassText ~= "" and bypassText ~= "Ex: Golden Egg" then
        for item in string.gmatch(bypassText, "([^,]+)") do
            table.insert(config.bypassItems, item:gsub("^%s*(.-)%s*$", "%1"))
        end
    end
    
    -- Never Sell Items
    local neverText = neverSellBox.Text
    config.neverSellItems = {}
    if neverText ~= "" and neverText ~= "Ex: Vehicle" then
        for item in string.gmatch(neverText, "([^,]+)") do
            table.insert(config.neverSellItems, item:gsub("^%s*(.-)%s*$", "%1"))
        end
    end
    
    -- Toggles
    config.autoPickup = autoPickup.Text == "ON"
    config.autoSell = autoSell.Text == "ON"
    config.autoGrade = autoGrade.Text == "ON"
    config.autoFreeze = autoFreeze.Text == "ON"
    config.autoOpen = autoOpen.Text == "ON"
    
    statusLabel.Text = "✅ Configurações salvas!"
    print("✅ Configurações salvas!")
    print("Bypass:", table.concat(config.bypassItems, ", "))
    print("Never Sell:", table.concat(config.neverSellItems, ", "))
end)

-- Iniciar/Parar
startBtn.MouseButton1Click:Connect(function()
    if running then
        running = false
        startBtn.Text = "▶️ INICIAR AUTO FARM"
        startBtn.BackgroundColor3 = Color3.fromRGB(76, 175, 80)
        statusLabel.Text = "⏸️ Parado"
    else
        -- Salva antes de começar
        saveBtn.MouseButton1Click:Fire()
        
        running = true
        startBtn.Text = "⏹️ PARAR"
        startBtn.BackgroundColor3 = Color3.fromRGB(244, 67, 54)
        statusLabel.Text = "🔄 Rodando..."
        
        -- Inicia o loop em uma thread separada
        task.spawn(MainLoop)
    end
end)

-- ====== DRAG PARA MOVER ======
local dragging = false
local dragStart, startPos

mainFrame.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.Touch then
        dragging = true
        dragStart = input.Position
        startPos = mainFrame.Position
    end
end)

mainFrame.InputEnded:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.Touch then
        dragging = false
    end
end)

game:GetService("UserInputService").TouchMoved:Connect(function(input)
    if dragging then
        local delta = input.Position - dragStart
        mainFrame.Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X, 
                                       startPos.Y.Scale, startPos.Y.Offset + delta.Y)
    end
end)

print("✅ Storage Hunters Auto-Farm carregado!")
print("Digite seus valores e clique em INICIAR!")
