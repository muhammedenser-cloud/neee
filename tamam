getgenv().SCRIPT_KEY = "KEYLESS"

local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humanoid = character:WaitForChild("Humanoid")
local rootPart = character:WaitForChild("HumanoidRootPart")
local runService = game:GetService("RunService")
local players = game:GetService("Players")
local camera = workspace.CurrentCamera
local starterGui = game:GetService("StarterGui")
local userInput = game:GetService("UserInputService")
local lighting = game:GetService("Lighting")
local tweenService = game:GetService("TweenService")
local replicatedStorage = game:GetService("ReplicatedStorage")
local debris = game:GetService("Debris")
local httpService = game:GetService("HttpService")
local teleportService = game:GetService("TeleportService")
local marketplaceService = game:GetService("MarketplaceService")
local virtualUser = game:GetService("VirtualUser")
local guiService = game:GetService("GuiService")
local coreGui = game:GetService("CoreGui")
local scriptContext = game:GetService("ScriptContext")
local physicsService = game:GetService("PhysicsService")
local pathfindingService = game:GetService("PathfindingService")
local collectionService = game:GetService("CollectionService")
local contextActionService = game:GetService("ContextActionService")

local Keys = {
    ToggleUI = Enum.KeyCode.RightControl,
    ToggleAimbot = Enum.KeyCode.Z,
    ToggleESP = Enum.KeyCode.X,
    ToggleAutoShoot = Enum.KeyCode.C,
    ToggleFly = Enum.KeyCode.V,
    ToggleSpeed = Enum.KeyCode.B,
    ToggleNoclip = Enum.KeyCode.N,
    ToggleBombJump = Enum.KeyCode.M,
    TeleportToGun = Enum.KeyCode.G,
    FlingMurderer = Enum.KeyCode.F,
    FlingSheriff = Enum.KeyCode.H,
    MassKill = Enum.KeyCode.K,
    ToggleTheme = Enum.KeyCode.T,
    ToggleSilentAim = Enum.KeyCode.Q,
    ToggleWallhack = Enum.KeyCode.W,
    ToggleNightVision = Enum.KeyCode.E,
    ToggleInfiniteEnergy = Enum.KeyCode.R,
    ToggleAutoHeal = Enum.KeyCode.Y,
    ToggleChams = Enum.KeyCode.I,
    ToggleTracers = Enum.KeyCode.O,
    ToggleRadar = Enum.KeyCode.P,
    ToggleSpinBot = Enum.KeyCode.L,
    ToggleAntiAim = Enum.KeyCode.U,
    ToggleFOV = Enum.KeyCode.J,
    ToggleTriggerBot = Enum.KeyCode.Semicolon,
    ToggleNoRecoil = Enum.KeyCode.Backslash,
    ToggleNoSpread = Enum.KeyCode.RightBracket,
    ToggleInstantReload = Enum.KeyCode.LeftBracket,
    ToggleAmmo = Enum.KeyCode.Period,
    ToggleGunESP = Enum.KeyCode.Comma,
    ToggleBoxESP = Enum.KeyCode.Slash,
    ToggleNameESP = Enum.KeyCode.Quote,
    ToggleHealthESP = Enum.KeyCode.Equals,
    ToggleDistanceESP = Enum.KeyCode.Minus,
    ToggleSkeletonESP = Enum.KeyCode.LeftShift,
    ToggleHeadshot = Enum.KeyCode.H,
    ToggleBodyshot = Enum.KeyCode.J,
    ToggleLegshot = Enum.KeyCode.K,
    ToggleArmshot = Enum.KeyCode.L
}

local function getEnemies()
    local list = {}
    for _, p in pairs(players:GetPlayers()) do
        if p ~= player and p.Character then
            table.insert(list, p)
        end
    end
    return list
end

local function getNearest()
    local nearest, dist = nil, math.huge
    for _, p in pairs(getEnemies()) do
        if p.Character and p.Character:FindFirstChild("HumanoidRootPart") then
            local pos = p.Character.HumanoidRootPart.Position
            local d = (rootPart.Position - pos).Magnitude
            if d < dist then dist = d; nearest = p end
        end
    end
    return nearest
end

local function getMurderer()
    for _, p in pairs(getEnemies()) do
        if p.Character and p.Character:FindFirstChild("Humanoid") then
            local hum = p.Character.Humanoid
            if hum:FindFirstChild("Murderer") or hum:FindFirstChild("Katil") or hum:FindFirstChild("Killer") or hum:FindFirstChild("KatilTag") or hum:FindFirstChild("IsMurderer") or hum:FindFirstChild("KillerTag") then
                return p
            end
        end
    end
    return nil
end

local function getSheriff()
    for _, p in pairs(getEnemies()) do
        if p.Character and p.Character:FindFirstChild("Humanoid") then
            local hum = p.Character.Humanoid
            if hum:FindFirstChild("Sheriff") or hum:FindFirstChild("Serif") or hum:FindFirstChild("Sherif") or hum:FindFirstChild("SheriffTag") or hum:FindFirstChild("SerifTag") or hum:FindFirstChild("IsSheriff") or hum:FindFirstChild("SherifTag") then
                return p
            end
        end
    end
    return nil
end

local function getHero()
    for _, p in pairs(getEnemies()) do
        if p.Character and p.Character:FindFirstChild("Humanoid") then
            local hum = p.Character.Humanoid
            if hum:FindFirstChild("Hero") or hum:FindFirstChild("Kahraman") or hum:FindFirstChild("HeroTag") then
                return p
            end
        end
    end
    return nil
end

local function getPlayerRole(p)
    if not p or not p.Character then return "Masum" end
    local hum = p.Character:FindFirstChild("Humanoid")
    if not hum then return "Masum" end
    if hum:FindFirstChild("Murderer") or hum:FindFirstChild("Katil") or hum:FindFirstChild("Killer") or hum:FindFirstChild("KatilTag") or hum:FindFirstChild("IsMurderer") or hum:FindFirstChild("KillerTag") then
        return "Katil"
    elseif hum:FindFirstChild("Sheriff") or hum:FindFirstChild("Serif") or hum:FindFirstChild("Sherif") or hum:FindFirstChild("SheriffTag") or hum:FindFirstChild("SerifTag") or hum:FindFirstChild("IsSheriff") or hum:FindFirstChild("SherifTag") then
        return "Serif"
    elseif hum:FindFirstChild("Hero") or hum:FindFirstChild("Kahraman") or hum:FindFirstChild("HeroTag") then
        return "Kahraman"
    else
        return "Masum"
    end
end

local function getPlayerColor(p)
    local role = getPlayerRole(p)
    if role == "Katil" then return Color3.new(1, 0, 0)
    elseif role == "Serif" then return Color3.new(0, 0.3, 1)
    elseif role == "Kahraman" then return Color3.new(1, 1, 0)
    else return Color3.new(0, 1, 0) end
end

local function getAliveEnemies()
    local list = {}
    for _, p in pairs(getEnemies()) do
        if p.Character then
            local hum = p.Character:FindFirstChild("Humanoid")
            if hum and hum.Health > 0 then table.insert(list, p) end
        end
    end
    return list
end

local function getGunPositions()
    local guns = {}
    for _, tool in pairs(workspace:GetDescendants()) do
        if tool:IsA("Tool") and tool:FindFirstChild("Handle") then
            local name = tool.Name:lower()
            if name:find("gun") or name:find("knife") or name:find("sword") or name:find("silah") then
                table.insert(guns, {tool = tool, pos = tool.Handle.Position})
            end
        end
    end
    return guns
end

local function getNearestGun()
    local guns = getGunPositions()
    if #guns > 0 then
        local nearest, dist = nil, math.huge
        for _, gun in pairs(guns) do
            local d = (rootPart.Position - gun.pos).Magnitude
            if d < dist then dist = d; nearest = gun end
        end
        return nearest
    end
    return nil
end

local function teleportToGun()
    local nearest = getNearestGun()
    if nearest then
        rootPart.CFrame = CFrame.new(nearest.pos + Vector3.new(0, 3, 0))
        starterGui:SetCore("SendNotification", {Title = "ByEnserHub", Text = "Silaha ışınlandın!", Duration = 2})
    else
        starterGui:SetCore("SendNotification", {Title = "ByEnserHub", Text = "Silah bulunamadı!", Duration = 2})
    end
end

local aimbotEnabled = false
local aimbotConnection = nil
local aimbotTarget = nil
local aimbotLocked = false
local aimbotSmoothness = 0.05
local aimbotFOV = 180
local aimbotTargetPart = "Head"
local aimbotAutoShoot = true
local aimbotPredictMovement = true
local aimbotPrediction = 0.5
local aimbotShootDelay = 0.02
local aimbotMaxDistance = 350
local aimbotMinDistance = 5
local aimbotOnlyMurderer = false
local aimbotIgnoreSheriff = false
local aimbotIgnoreInnocent = false
local aimbotShowFOV = true
local aimbotFOVCircle = nil
local aimbotFOVColor = Color3.new(1, 0, 0)
local aimbotFOVTransparency = 0.3

local function createFOVCircle()
    if aimbotFOVCircle then aimbotFOVCircle:Destroy() end
    if not aimbotEnabled or not aimbotShowFOV then return end
    local circle = Instance.new("Part")
    circle.Size = Vector3.new(aimbotFOV * 0.1, 0.1, aimbotFOV * 0.1)
    circle.Shape = Enum.PartType.Cylinder
    circle.Material = Enum.Material.Neon
    circle.BrickColor = BrickColor.new(aimbotFOVColor)
    circle.Transparency = aimbotFOVTransparency
    circle.Anchored = true
    circle.CanCollide = false
    circle.Parent = workspace
    local attachment = Instance.new("Attachment")
    attachment.Parent = circle
    local billboard = Instance.new("BillboardGui")
    billboard.Size = UDim2.new(2, 0, 2, 0)
    billboard.AlwaysOnTop = true
    billboard.Parent = circle
    local frame = Instance.new("Frame")
    frame.Size = UDim2.new(1, 0, 1, 0)
    frame.BackgroundTransparency = 1
    frame.Parent = billboard
    local fovLabel = Instance.new("TextLabel")
    fovLabel.Size = UDim2.new(1, 0, 1, 0)
    fovLabel.BackgroundTransparency = 1
    fovLabel.Text = "FOV: " .. aimbotFOV
    fovLabel.TextColor3 = aimbotFOVColor
    fovLabel.TextSize = 16
    fovLabel.Font = Enum.Font.GothamBold
    fovLabel.Parent = frame
    local function updateFOV()
        if not aimbotEnabled or not aimbotShowFOV then
            if aimbotFOVCircle then aimbotFOVCircle:Destroy(); aimbotFOVCircle = nil end
            return
        end
        local camPos = camera.CFrame.Position
        local lookVector = camera.CFrame.LookVector
        circle.CFrame = CFrame.new(camPos + lookVector * 10, camPos + lookVector * 20)
    end
    aimbotFOVCircle = circle
    runService.RenderStepped:Connect(updateFOV)
end

local function toggleAimbot()
    aimbotEnabled = not aimbotEnabled
    if aimbotEnabled then
        if aimbotConnection then aimbotConnection:Disconnect() end
        createFOVCircle()
        aimbotConnection = runService.RenderStepped:Connect(function()
            if aimbotEnabled then
                local target = nil
                if aimbotOnlyMurderer then
                    target = getMurderer()
                end
                if not target then
                    target = getNearest()
                end
                if aimbotIgnoreSheriff and target == getSheriff() then
                    target = getNearest()
                end
                if aimbotIgnoreInnocent and getPlayerRole(target) == "Masum" then
                    target = getNearest()
                end
                if target and target.Character then
                    local tRoot = target.Character:FindFirstChild("HumanoidRootPart")
                    local tHead = target.Character:FindFirstChild("Head")
                    local tTorso = target.Character:FindFirstChild("Torso") or target.Character:FindFirstChild("UpperTorso")
                    local tHumanoid = target.Character:FindFirstChild("Humanoid")
                    if tRoot and tHumanoid and tHumanoid.Health > 0 then
                        local distance = (rootPart.Position - tRoot.Position).Magnitude
                        if distance >= aimbotMinDistance and distance <= aimbotMaxDistance then
                            aimbotTarget = target
                            aimbotLocked = true
                            local aimPart = tHead or tRoot
                            if aimbotTargetPart == "Head" and tHead then
                                aimPart = tHead
                            elseif aimbotTargetPart == "Torso" and tTorso then
                                aimPart = tTorso
                            end
                            local targetPos = aimPart.Position
                            if aimbotPredictMovement then
                                local velocity = tRoot.Velocity or Vector3.new(0, 0, 0)
                                targetPos = targetPos + (velocity * aimbotPrediction)
                            end
                            local viewportPoint = camera:WorldToViewportPoint(targetPos)
                            local mouse = player:GetMouse()
                            local currentPos = Vector2.new(mouse.X, mouse.Y)
                            local targetPos2D = Vector2.new(viewportPoint.X, viewportPoint.Y)
                            local newPos = currentPos:Lerp(targetPos2D, aimbotSmoothness)
                            mouse.Move(newPos)
                            if aimbotAutoShoot then
                                local tool = character:FindFirstChildOfClass("Tool")
                                if tool and distance < 300 then
                                    tool:Activate()
                                    task.wait(aimbotShootDelay)
                                    tool:Activate()
                                    task.wait(aimbotShootDelay)
                                    tool:Activate()
                                    task.wait(aimbotShootDelay)
                                end
                            end
                        else
                            aimbotLocked = false
                        end
                    else
                        aimbotLocked = false
                    end
                else
                    aimbotLocked = false
                end
            end
        end)
        starterGui:SetCore("SendNotification", {Title = "ByEnserHub", Text = "Aimbot Aktif! [Z]", Duration = 2})
    else
        if aimbotConnection then aimbotConnection:Disconnect(); aimbotConnection = nil end
        if aimbotFOVCircle then aimbotFOVCircle:Destroy(); aimbotFOVCircle = nil end
        aimbotTarget = nil
        aimbotLocked = false
        starterGui:SetCore("SendNotification", {Title = "ByEnserHub", Text = "Aimbot Devre Dışı!", Duration = 2})
    end
end

local silentAim = false
local silentAimConnection = nil

local function toggleSilentAim()
    silentAim = not silentAim
    if silentAim then
        if silentAimConnection then silentAimConnection:Disconnect() end
        silentAimConnection = runService.RenderStepped:Connect(function()
            if silentAim then
                local target = getMurderer() or getNearest()
                if target and target.Character then
                    local tHead = target.Character:FindFirstChild("Head")
                    local tRoot = target.Character:FindFirstChild("HumanoidRootPart")
                    if tHead and tRoot then
                        local viewportPoint = camera:WorldToViewportPoint(tHead.Position)
                        local mouse = player:GetMouse()
                        mouse.Move(Vector2.new(viewportPoint.X, viewportPoint.Y))
                        local tool = character:FindFirstChildOfClass("Tool")
                        if tool then
                            tool:Activate()
                        end
                    end
                end
            end
        end)
        starterGui:SetCore("SendNotification", {Title = "ByEnserHub", Text = "Silent Aim Aktif! [Q]", Duration = 2})
    else
        if silentAimConnection then silentAimConnection:Disconnect(); silentAimConnection = nil end
        starterGui:SetCore("SendNotification", {Title = "ByEnserHub", Text = "Silent Aim Devre Dışı!", Duration = 2})
    end
end

local triggerBot = false
local triggerBotConnection = nil

local function toggleTriggerBot()
    triggerBot = not triggerBot
    if triggerBot then
        if triggerBotConnection then triggerBotConnection:Disconnect() end
        triggerBotConnection = runService.Heartbeat:Connect(function()
            if triggerBot then
                local target = getMurderer() or getNearest()
                if target and target.Character then
                    local tHead = target.Character:FindFirstChild("Head")
                    if tHead then
                        local viewportPoint = camera:WorldToViewportPoint(tHead.Position)
                        local screenPos = Vector2.new(viewportPoint.X, viewportPoint.Y)
                        local mouse = player:GetMouse()
                        local mousePos = Vector2.new(mouse.X, mouse.Y)
                        local distance = (mousePos - screenPos).Magnitude
                        if distance < 50 then
                            local tool = character:FindFirstChildOfClass("Tool")
                            if tool then
                                tool:Activate()
                            end
                        end
                    end
                end
            end
        end)
        starterGui:SetCore("SendNotification", {Title = "ByEnserHub", Text = "Trigger Bot Aktif! [;]", Duration = 2})
    else
        if triggerBotConnection then triggerBotConnection:Disconnect(); triggerBotConnection = nil end
        starterGui:SetCore("SendNotification", {Title = "ByEnserHub", Text = "Trigger Bot Devre Dışı!", Duration = 2})
    end
end

local espEnabled = false
local espObjects = {}
local espConnections = {}
local espHighlightTransparency = 0.15
local espShowNames = true
local espShowHealth = true
local espShowDistance = true
local espShowBoxes = true
local espShowTracers = false
local espBoxColor = Color3.new(1, 1, 1)
local espTracerColor = Color3.new(1, 1, 0)
local espFontSize = 16
local espBillboardSize = UDim2.new(0, 150, 0, 50)
local espHealthBarHeight = 0.3
local espDistanceLabelHeight = 0.8
local espNameLabelHeight = 0.5
local espShowSelf = true
local espSelfColor = Color3.new(0, 1, 1)
local espSelfRole = "Kendin"

local function createESPForPlayer(p)
    if not p or not p.Character then return end
    local char = p.Character
    local hum = char:FindFirstChild("Humanoid")
    if not hum then return end
    local isSelf = (p == player)
    local role = isSelf and espSelfRole or getPlayerRole(p)
    local color = isSelf and espSelfColor or getPlayerColor(p)
    if isSelf and not espShowSelf then return end
    local highlight = Instance.new("Highlight")
    highlight.Adornee = char
    highlight.FillColor = color
    highlight.FillTransparency = espHighlightTransparency
    highlight.OutlineColor = espBoxColor
    highlight.OutlineTransparency = 0.1
    highlight.DepthMode = Enum.HighlightDepthMode.AlwaysOnTop
    highlight.Parent = char
    table.insert(espObjects, highlight)
    local head = char:FindFirstChild("Head") or char:FindFirstChild("HumanoidRootPart")
    if not head then return end
    local bill = Instance.new("BillboardGui")
    bill.Size = espBillboardSize
    bill.AlwaysOnTop = true
    bill.Parent = head
    table.insert(espObjects, bill)
    if espShowNames then
        local nameLabel = Instance.new("TextLabel")
        nameLabel.Size = UDim2.new(1, 0, espNameLabelHeight, 0)
        nameLabel.Position = UDim2.new(0, 0, 0, 0)
        nameLabel.BackgroundTransparency = 1
        nameLabel.Text = isSelf and ("[BEN] " .. p.Name) or p.Name
        nameLabel.TextColor3 = color
        nameLabel.TextSize = espFontSize
        nameLabel.Font = Enum.Font.GothamBold
        nameLabel.TextStrokeTransparency = 0
        nameLabel.TextStrokeColor3 = Color3.new(0, 0, 0)
        nameLabel.Parent = bill
        table.insert(espObjects, nameLabel)
    end
    if espShowHealth then
        local healthBar = Instance.new("Frame")
        healthBar.Size = UDim2.new(1, 0, espHealthBarHeight, 0)
        healthBar.Position = UDim2.new(0, 0, espNameLabelHeight, 0)
        healthBar.BackgroundColor3 = Color3.new(0, 1, 0)
        healthBar.BorderSizePixel = 0
        healthBar.Parent = bill
        table.insert(espObjects, healthBar)
        local healthFill = Instance.new("Frame")
        healthFill.Size = UDim2.new(hum.Health / hum.MaxHealth, 0, 1, 0)
        healthFill.BackgroundColor3 = Color3.new(0, 1, 0)
        healthFill.BorderSizePixel = 0
        healthFill.Parent = healthBar
        table.insert(espObjects, healthFill)
        local function updateHealth()
            if hum and healthFill then
                healthFill.Size = UDim2.new(hum.Health / hum.MaxHealth, 0, 1, 0)
                local ratio = hum.Health / hum.MaxHealth
                if ratio < 0.3 then healthFill.BackgroundColor3 = Color3.new(1, 0, 0)
                elseif ratio < 0.6 then healthFill.BackgroundColor3 = Color3.new(1, 1, 0)
                else healthFill.BackgroundColor3 = Color3.new(0, 1, 0) end
            end
        end
        local healthConn = hum.HealthChanged:Connect(updateHealth)
        table.insert(espConnections, healthConn)
    end
    if espShowDistance then
        local distLabel = Instance.new("TextLabel")
        distLabel.Size = UDim2.new(1, 0, 0.15, 0)
        distLabel.Position = UDim2.new(0, 0, espDistanceLabelHeight, 0)
        distLabel.BackgroundTransparency = 1
        distLabel.Text = ""
        distLabel.TextColor3 = Color3.new(1, 1, 1)
        distLabel.TextSize = 12
        distLabel.Font = Enum.Font.Gotham
        distLabel.Parent = bill
        table.insert(espObjects, distLabel)
        local function updateDistance()
            if hum and rootPart and distLabel then
                local tRoot = hum.Parent:FindFirstChild("HumanoidRootPart")
                if tRoot then
                    local dist = (rootPart.Position - tRoot.Position).Magnitude
                    distLabel.Text = math.floor(dist) .. "m"
                end
            end
        end
        local distConn = runService.Heartbeat:Connect(updateDistance)
        table.insert(espConnections, distConn)
    end
    if espShowBoxes then
        local box = Instance.new("SelectionBox")
        box.Adornee = char
        box.Color3 = espBoxColor
        box.Transparency = 0.5
        box.Parent = char
        table.insert(espObjects, box)
    end
    if espShowTracers and not isSelf then
        local tracer = Instance.new("Part")
        tracer.Size = Vector3.new(0.1, 0.1, 0.1)
        tracer.Anchored = true
        tracer.CanCollide = false
        tracer.Material = Enum.Material.Neon
        tracer.BrickColor = BrickColor.new(Color3.new(1, 1, 0))
        tracer.Parent = workspace
        table.insert(espObjects, tracer)
        local function updateTracer()
            if tracer and rootPart and head then
                local startPos = rootPart.Position + Vector3.new(0, 1, 0)
                local endPos = head.Position
                local midPos = (startPos + endPos) / 2
                local distance = (startPos - endPos).Magnitude
                tracer.CFrame = CFrame.new(midPos, endPos) * CFrame.new(0, 0, -distance / 2)
                tracer.Size = Vector3.new(0.1, 0.1, distance)
            end
        end
        local tracerConn = runService.Heartbeat:Connect(updateTracer)
        table.insert(espConnections, tracerConn)
    end
end

local function toggleESP()
    espEnabled = not espEnabled
    if espEnabled then
        for _, p in pairs(players:GetPlayers()) do
            if p ~= player and p.Character then
                createESPForPlayer(p)
            end
        end
        starterGui:SetCore("SendNotification", {Title = "ByEnserHub", Text = "ESP Aktif! [X]", Duration = 2})
    else
        for _, obj in pairs(espObjects) do obj:Destroy() end
        espObjects = {}
        for _, conn in pairs(espConnections) do conn:Disconnect() end
        espConnections = {}
        starterGui:SetCore("SendNotification", {Title = "ByEnserHub", Text = "ESP Devre Dışı!", Duration = 2})
    end
end

local autoShoot = false
local autoShootConnection = nil
local autoShootDelay = 0.02
local autoShootMaxDistance = 350
local autoShootMinDistance = 5
local autoShootOnlyMurderer = false
local autoShootIgnoreSheriff = false
local autoShootIgnoreInnocent = false
local autoShootBurstCount = 3
local autoShootBurstDelay = 0.05
local autoShootTarget = nil
local autoShootLocked = false
local autoShootPredictMovement = true
local autoShootPrediction = 0.3

local function toggleAutoShoot()
    autoShoot = not autoShoot
    if autoShoot then
        if autoShootConnection then autoShootConnection:Disconnect() end
        autoShootConnection = runService.Heartbeat:Connect(function()
            if autoShoot then
                local target = nil
                if autoShootOnlyMurderer then
                    target = getMurderer()
                end
                if not target then
                    target = getNearest()
                end
                if autoShootIgnoreSheriff and target == getSheriff() then
                    target = getNearest()
                end
                if autoShootIgnoreInnocent and getPlayerRole(target) == "Masum" then
                    target = getNearest()
                end
                if target and target.Character then
                    local tRoot = target.Character:FindFirstChild("HumanoidRootPart")
                    local tHumanoid = target.Character:FindFirstChild("Humanoid")
                    if tRoot and tHumanoid and tHumanoid.Health > 0 then
                        local distance = (rootPart.Position - tRoot.Position).Magnitude
                        if distance >= autoShootMinDistance and distance <= autoShootMaxDistance then
                            autoShootTarget = target
                            autoShootLocked = true
                            local tool = character:FindFirstChildOfClass("Tool")
                            if tool then
                                for i = 1, autoShootBurstCount do
                                    tool:Activate()
                                    task.wait(autoShootDelay)
                                end
                            end
                        else
                            autoShootLocked = false
                        end
                    else
                        autoShootLocked = false
                    end
                else
                    autoShootLocked = false
                end
            end
        end)
        starterGui:SetCore("SendNotification", {Title = "ByEnserHub", Text = "Auto Shoot Aktif! [C]", Duration = 2})
    else
        if autoShootConnection then autoShootConnection:Disconnect(); autoShootConnection = nil end
        starterGui:SetCore("SendNotification", {Title = "ByEnserHub", Text = "Auto Shoot Devre Dışı!", Duration = 2})
    end
end

local flying = false
local flyVel = Instance.new("BodyVelocity")
flyVel.MaxForce = Vector3.new(1e9, 1e9, 1e9)
local flyConnection = nil
local flySpeed = 50

local function toggleFly()
    flying = not flying
    if flying then
        flyVel.Parent = rootPart
        flyVel.Velocity = Vector3.new(0, flySpeed, 0)
        if flyConnection then flyConnection:Disconnect() end
        flyConnection = runService.Heartbeat:Connect(function()
            if flying and rootPart then
                flyVel.Velocity = Vector3.new(0, flySpeed, 0)
            end
        end)
        starterGui:SetCore("SendNotification", {Title = "ByEnserHub", Text = "Fly Aktif! [V]", Duration = 2})
    else
        flyVel:Destroy()
        if flyConnection then flyConnection:Disconnect(); flyConnection = nil end
        starterGui:SetCore("SendNotification", {Title = "ByEnserHub", Text = "Fly Devre Dışı!", Duration = 2})
    end
end

local speedBoost = false
local speedBoostConnection = nil
local speedBoostSpeed = 300
local speedBoostJumpMultiplier = 5

local function toggleSpeed()
    speedBoost = not speedBoost
    if speedBoost then
        if speedBoostConnection then speedBoostConnection:Disconnect() end
        speedBoostConnection = runService.Heartbeat:Connect(function()
            if speedBoost and humanoid and rootPart then
                local moveVector = humanoid.MoveDirection
                if moveVector.Magnitude > 0 then
                    rootPart.Velocity = moveVector * speedBoostSpeed + Vector3.new(0, rootPart.Velocity.Y, 0)
                end
                if humanoid:GetState() == Enum.HumanoidStateType.Jumping then
                    rootPart.Velocity = rootPart.Velocity + moveVector * (speedBoostSpeed * speedBoostJumpMultiplier)
                end
            end
        end)
        starterGui:SetCore("SendNotification", {Title = "ByEnserHub", Text = "Speed Boost Aktif! [B]", Duration = 2})
    else
        if speedBoostConnection then speedBoostConnection:Disconnect(); speedBoostConnection = nil end
        starterGui:SetCore("SendNotification", {Title = "ByEnserHub", Text = "Speed Boost Devre Dışı!", Duration = 2})
    end
end

local noclip = false
local noclipConnection = nil

local function toggleNoclip()
    noclip = not noclip
    if noclip then
        if noclipConnection then noclipConnection:Disconnect() end
        noclipConnection = runService.Stepped:Connect(function()
            if noclip and character then
                for _, part in pairs(character:GetDescendants()) do
                    if part:IsA("BasePart") then
                        part.CanCollide = false
                    end
                end
            end
        end)
        starterGui:SetCore("SendNotification", {Title = "ByEnserHub", Text = "No Clip Aktif! [N]", Duration = 2})
    else
        if noclipConnection then noclipConnection:Disconnect(); noclipConnection = nil end
        for _, part in pairs(character:GetDescendants()) do
            if part:IsA("BasePart") then
                part.CanCollide = true
            end
        end
        starterGui:SetCore("SendNotification", {Title = "ByEnserHub", Text = "No Clip Devre Dışı!", Duration = 2})
    end
end

local bombJump = false
local bombJumpConnection = nil
local bombJumpPower = 500
local bombJumpDelay = 0.2

local function toggleBombJump()
    bombJump = not bombJump
    if bombJump then
        if bombJumpConnection then bombJumpConnection:Disconnect() end
        bombJumpConnection = runService.Heartbeat:Connect(function()
            if bombJump and humanoid then
                if humanoid:GetState() == Enum.HumanoidStateType.Jumping then
                    humanoid.JumpPower = bombJumpPower
                    local explosion = Instance.new("Explosion")
                    explosion.BlastRadius = 10
                    explosion.BlastPressure = 500000
                    explosion.Position = rootPart.Position - Vector3.new(0, 2, 0)
                    explosion.Parent = workspace
                    task.wait(bombJumpDelay)
                    humanoid.JumpPower = 50
                end
            end
        end)
        starterGui:SetCore("SendNotification", {Title = "ByEnserHub", Text = "Bomb Jump Aktif! [M]", Duration = 2})
    else
        if bombJumpConnection then bombJumpConnection:Disconnect(); bombJumpConnection = nil end
        humanoid.JumpPower = 50
        starterGui:SetCore("SendNotification", {Title = "ByEnserHub", Text = "Bomb Jump Devre Dışı!", Duration = 2})
    end
end

local wallhack = false
local wallhackTransparency = 0.2
local wallhackObjects = {}

local function toggleWallhack()
    wallhack = not wallhack
    if wallhack then
        for _, v in pairs(workspace:GetDescendants()) do
            if v:IsA("BasePart") and v.Material ~= Enum.Material.Neon then
                v.LocalTransparencyModifier = wallhackTransparency
                table.insert(wallhackObjects, v)
            end
        end
        starterGui:SetCore("SendNotification", {Title = "ByEnserHub", Text = "Wallhack Aktif! [W]", Duration = 2})
    else
        for _, v in pairs(wallhackObjects) do
            v.LocalTransparencyModifier = 0
        end
        wallhackObjects = {}
        starterGui:SetCore("SendNotification", {Title = "ByEnserHub", Text = "Wallhack Devre Dışı!", Duration = 2})
    end
end

local nightVision = false

local function toggleNightVision()
    nightVision = not nightVision
    if nightVision then
        lighting.Brightness = 10
        lighting.Ambient = Color3.new(1, 1, 1)
        lighting.ColorShift_Top = Color3.new(0, 0.5, 0)
        lighting.ColorShift_Bottom = Color3.new(0, 0.5, 0)
        starterGui:SetCore("SendNotification", {Title = "ByEnserHub", Text = "Night Vision Aktif! [E]", Duration = 2})
    else
        lighting.Brightness = 2
        lighting.Ambient = Color3.new(0.5, 0.5, 0.5)
        lighting.ColorShift_Top = Color3.new(0, 0, 0)
        lighting.ColorShift_Bottom = Color3.new(0, 0, 0)
        starterGui:SetCore("SendNotification", {Title = "ByEnserHub", Text = "Night Vision Devre Dışı!", Duration = 2})
    end
end

local infiniteEnergy = false
local infiniteEnergyConnection = nil

local function toggleInfiniteEnergy()
    infiniteEnergy = not infiniteEnergy
    if infiniteEnergy then
        if infiniteEnergyConnection then infiniteEnergyConnection:Disconnect() end
        infiniteEnergyConnection = runService.Heartbeat:Connect(function()
            if infiniteEnergy then
                local stats = player:FindFirstChild("leaderstats")
                if stats then
                    local energy = stats:FindFirstChild("Energy") or stats:FindFirstChild("Mana")
                    if energy then
                        energy.Value = 999999
                    end
                end
            end
        end)
        starterGui:SetCore("SendNotification", {Title = "ByEnserHub", Text = "Infinite Energy Aktif! [R]", Duration = 2})
    else
        if infiniteEnergyConnection then infiniteEnergyConnection:Disconnect(); infiniteEnergyConnection = nil end
        starterGui:SetCore("SendNotification", {Title = "ByEnserHub", Text = "Infinite Energy Devre Dışı!", Duration = 2})
    end
end

local autoHeal = false
local autoHealConnection = nil

local function toggleAutoHeal()
    autoHeal = not autoHeal
    if autoHeal then
        if autoHealConnection then autoHealConnection:Disconnect() end
        autoHealConnection = runService.Heartbeat:Connect(function()
            if autoHeal and humanoid and humanoid.Health < humanoid.MaxHealth then
                humanoid.Health = humanoid.MaxHealth
            end
        end)
        starterGui:SetCore("SendNotification", {Title = "ByEnserHub", Text = "Auto Heal Aktif! [Y]", Duration = 2})
    else
        if autoHealConnection then autoHealConnection:Disconnect(); autoHealConnection = nil end
        starterGui:SetCore("SendNotification", {Title = "ByEnserHub", Text = "Auto Heal Devre Dışı!", Duration = 2})
    end
end

local function flingMurderer()
    local murderer = getMurderer()
    if murderer and murderer.Character then
        local tRoot = murderer.Character:FindFirstChild("HumanoidRootPart")
        local tHumanoid = murderer.Character:FindFirstChild("Humanoid")
        if tRoot and tHumanoid and tHumanoid.Health > 0 then
            local randomX = math.random(-99999, 99999)
            local randomZ = math.random(-99999, 99999)
            local randomY = math.random(50000, 99999)
            tRoot.Velocity = Vector3.new(randomX, randomY, randomZ)
            tHumanoid.PlatformStand = true
            local flingConnection
            flingConnection = runService.Heartbeat:Connect(function()
                if tRoot and tHumanoid and tHumanoid.Health > 0 then
                    local randomX2 = math.random(-99999, 99999)
                    local randomZ2 = math.random(-99999, 99999)
                    local randomY2 = math.random(50000, 99999)
                    tRoot.Velocity = Vector3.new(randomX2, randomY2, randomZ2)
                    if tRoot.Position.Y < 0 then
                        tRoot.Velocity = Vector3.new(randomX2, 99999, randomZ2)
                    end
                else
                    flingConnection:Disconnect()
                end
            end)
            task.wait(5)
            flingConnection:Disconnect()
            tHumanoid.PlatformStand = false
            starterGui:SetCore("SendNotification", {Title = "ByEnserHub", Text = "Katil uçuruldu! [F]", Duration = 2})
        end
    else
        starterGui:SetCore("SendNotification", {Title = "ByEnserHub", Text = "Katil bulunamadı!", Duration = 2})
    end
end

local function flingSheriff()
    local sheriff = getSheriff()
    if sheriff and sheriff.Character then
        local tRoot = sheriff.Character:FindFirstChild("HumanoidRootPart")
        local tHumanoid = sheriff.Character:FindFirstChild("Humanoid")
        if tRoot and tHumanoid and tHumanoid.Health > 0 then
            local randomX = math.random(-99999, 99999)
            local randomZ = math.random(-99999, 99999)
            local randomY = math.random(50000, 99999)
            tRoot.Velocity = Vector3.new(randomX, randomY, randomZ)
            tHumanoid.PlatformStand = true
            local flingConnection
            flingConnection = runService.Heartbeat:Connect(function()
                if tRoot and tHumanoid and tHumanoid.Health > 0 then
                    local randomX2 = math.random(-99999, 99999)
                    local randomZ2 = math.random(-99999, 99999)
                    local randomY2 = math.random(50000, 99999)
                    tRoot.Velocity = Vector3.new(randomX2, randomY2, randomZ2)
                    if tRoot.Position.Y < 0 then
                        tRoot.Velocity = Vector3.new(randomX2, 99999, randomZ2)
                    end
                else
                    flingConnection:Disconnect()
                end
            end)
            task.wait(5)
            flingConnection:Disconnect()
            tHumanoid.PlatformStand = false
            starterGui:SetCore("SendNotification", {Title = "ByEnserHub", Text = "Şerif uçuruldu! [H]", Duration = 2})
        end
    else
        starterGui:SetCore("SendNotification", {Title = "ByEnserHub", Text = "Şerif bulunamadı!", Duration = 2})
    end
end

local function massKill()
    local killed = 0
    for _, enemy in pairs(getAliveEnemies()) do
        if enemy and enemy.Character then
            local tRoot = enemy.Character:FindFirstChild("HumanoidRootPart")
            local tHumanoid = enemy.Character:FindFirstChild("Humanoid")
            if tRoot and tHumanoid and tHumanoid.Health > 0 then
                rootPart.CFrame = CFrame.new(tRoot.Position + Vector3.new(0, 2, 0))
                task.wait(0.02)
                local tool = character:FindFirstChildOfClass("Tool")
                if tool then
                    tool:Activate()
                    task.wait(0.02)
                    tool:Activate()
                    task.wait(0.02)
                    tool:Activate()
                    task.wait(0.02)
                end
                tHumanoid.Health = 0
                killed = killed + 1
                task.wait(0.02)
            end
        end
    end
    starterGui:SetCore("SendNotification", {Title = "ByEnserHub", Text = killed .. " kişi öldürüldü! [K]", Duration = 2})
end

local gunESP = false
local gunESPObjects = {}

local function toggleGunESP()
    gunESP = not gunESP
    if gunESP then
        for _, tool in pairs(workspace:GetDescendants()) do
            if tool:IsA("Tool") and tool:FindFirstChild("Handle") then
                local highlight = Instance.new("Highlight")
                highlight.Adornee = tool
                highlight.FillColor = Color3.new(1, 0.5, 0)
                highlight.FillTransparency = 0.3
                highlight.OutlineColor = Color3.new(1, 1, 1)
                highlight.DepthMode = Enum.HighlightDepthMode.AlwaysOnTop
                highlight.Parent = tool
                table.insert(gunESPObjects, highlight)
            end
        end
        starterGui:SetCore("SendNotification", {Title = "ByEnserHub", Text = "Gun ESP Aktif!", Duration = 2})
    else
        for _, obj in pairs(gunESPObjects) do obj:Destroy() end
        gunESPObjects = {}
        starterGui:SetCore("SendNotification", {Title = "ByEnserHub", Text = "Gun ESP Devre Dışı!", Duration = 2})
    end
end

local noRecoil = false
local noRecoilConnection = nil

local function toggleNoRecoil()
    noRecoil = not noRecoil
    if noRecoil then
        if noRecoilConnection then noRecoilConnection:Disconnect() end
        noRecoilConnection = runService.Heartbeat:Connect(function()
            if noRecoil then
                local tool = character:FindFirstChildOfClass("Tool")
                if tool then
                    local anim = tool:FindFirstChild("Animation")
                    if anim then
                        anim.Recoil = 0
                        anim.Spread = 0
                    end
                end
            end
        end)
        starterGui:SetCore("SendNotification", {Title = "ByEnserHub", Text = "No Recoil Aktif!", Duration = 2})
    else
        if noRecoilConnection then noRecoilConnection:Disconnect(); noRecoilConnection = nil end
        starterGui:SetCore("SendNotification", {Title = "ByEnserHub", Text = "No Recoil Devre Dışı!", Duration = 2})
    end
end

local noSpread = false
local noSpreadConnection = nil

local function toggleNoSpread()
    noSpread = not noSpread
    if noSpread then
        if noSpreadConnection then noSpreadConnection:Disconnect() end
        noSpreadConnection = runService.Heartbeat:Connect(function()
            if noSpread then
                local tool = character:FindFirstChildOfClass("Tool")
                if tool then
                    local anim = tool:FindFirstChild("Animation")
                    if anim then
                        anim.Spread = 0
                    end
                end
            end
        end)
        starterGui:SetCore("SendNotification", {Title = "ByEnserHub", Text = "No Spread Aktif!", Duration = 2})
    else
        if noSpreadConnection then noSpreadConnection:Disconnect(); noSpreadConnection = nil end
        starterGui:SetCore("SendNotification", {Title = "ByEnserHub", Text = "No Spread Devre Dışı!", Duration = 2})
    end
end

local instantReload = false
local instantReloadConnection = nil

local function toggleInstantReload()
    instantReload = not instantReload
    if instantReload then
        if instantReloadConnection then instantReloadConnection:Disconnect() end
        instantReloadConnection = runService.Heartbeat:Connect(function()
            if instantReload then
                local tool = character:FindFirstChildOfClass("Tool")
                if tool then
                    local ammo = tool:FindFirstChild("Ammo")
                    if ammo then
                        ammo.Value = ammo.MaxValue or 999
                    end
                end
            end
        end)
        starterGui:SetCore("SendNotification", {Title = "ByEnserHub", Text = "Instant Reload Aktif!", Duration = 2})
    else
        if instantReloadConnection then instantReloadConnection:Disconnect(); instantReloadConnection = nil end
        starterGui:SetCore("SendNotification", {Title = "ByEnserHub", Text = "Instant Reload Devre Dışı!", Duration = 2})
    end
end

local spinBot = false
local spinBotConnection = nil

local function toggleSpinBot()
    spinBot = not spinBot
    if spinBot then
        if spinBotConnection then spinBotConnection:Disconnect() end
        spinBotConnection = runService.RenderStepped:Connect(function()
            if spinBot and rootPart then
                rootPart.CFrame = rootPart.CFrame * CFrame.Angles(0, math.rad(10), 0)
            end
        end)
        starterGui:SetCore("SendNotification", {Title = "ByEnserHub", Text = "Spin Bot Aktif! [L]", Duration = 2})
    else
        if spinBotConnection then spinBotConnection:Disconnect(); spinBotConnection = nil end
        starterGui:SetCore("SendNotification", {Title = "ByEnserHub", Text = "Spin Bot Devre Dışı!", Duration = 2})
    end
end

local antiAim = false
local antiAimConnection = nil

local function toggleAntiAim()
    antiAim = not antiAim
    if antiAim then
        if antiAimConnection then antiAimConnection:Disconnect() end
        antiAimConnection = runService.RenderStepped:Connect(function()
            if antiAim and rootPart then
                rootPart.CFrame = CFrame.new(rootPart.Position, rootPart.Position + Vector3.new(0, 1, 0))
            end
        end)
        starterGui:SetCore("SendNotification", {Title = "ByEnserHub", Text = "Anti Aim Aktif! [U]", Duration = 2})
    else
        if antiAimConnection then antiAimConnection:Disconnect(); antiAimConnection = nil end
        starterGui:SetCore("SendNotification", {Title = "ByEnserHub", Text = "Anti Aim Devre Dışı!", Duration = 2})
    end
end

local tracers = false
local tracerObjects = {}
local tracerConnection = nil

local function toggleTracers()
    tracers = not tracers
    if tracers then
        if tracerConnection then tracerConnection:Disconnect() end
        tracerConnection = runService.Heartbeat:Connect(function()
            if tracers then
                for _, obj in pairs(tracerObjects) do obj:Destroy() end
                tracerObjects = {}
                for _, p in pairs(getEnemies()) do
                    if p.Character and p.Character:FindFirstChild("HumanoidRootPart") then
                        local tRoot = p.Character.HumanoidRootPart
                        local tracer = Instance.new("Part")
                        tracer.Size = Vector3.new(0.1, 0.1, 0.1)
                        tracer.Anchored = true
                        tracer.CanCollide = false
                        tracer.Material = Enum.Material.Neon
                        tracer.BrickColor = BrickColor.new(Color3.new(1, 0, 0))
                        tracer.Parent = workspace
                        table.insert(tracerObjects, tracer)
                        local function updateTracer()
                            if tracer and rootPart and tRoot then
                                local startPos = rootPart.Position + Vector3.new(0, 1, 0)
                                local endPos = tRoot.Position
                                local midPos = (startPos + endPos) / 2
                                local distance = (startPos - endPos).Magnitude
                                tracer.CFrame = CFrame.new(midPos, endPos) * CFrame.new(0, 0, -distance / 2)
                                tracer.Size = Vector3.new(0.1, 0.1, distance)
                            end
                        end
                        local conn = runService.Heartbeat:Connect(updateTracer)
                        table.insert(tracerObjects, conn)
                    end
                end
            end
        end)
        starterGui:SetCore("SendNotification", {Title = "ByEnserHub", Text = "Tracers Aktif! [O]", Duration = 2})
    else
        if tracerConnection then tracerConnection:Disconnect(); tracerConnection = nil end
        for _, obj in pairs(tracerObjects) do obj:Destroy() end
        tracerObjects = {}
        starterGui:SetCore("SendNotification", {Title = "ByEnserHub", Text = "Tracers Devre Dışı!", Duration = 2})
    end
end

local chams = false
local chamsObjects = {}

local function toggleChams()
    chams = not chams
    if chams then
        for _, p in pairs(getEnemies()) do
            if p.Character then
                local char = p.Character
                for _, part in pairs(char:GetDescendants()) do
                    if part:IsA("BasePart") then
                        local cham = Instance.new("Highlight")
                        cham.Adornee = part
                        cham.FillColor = Color3.new(0, 1, 1)
                        cham.FillTransparency = 0.3
                        cham.OutlineColor = Color3.new(0, 1, 1)
                        cham.OutlineTransparency = 0
                        cham.DepthMode = Enum.HighlightDepthMode.AlwaysOnTop
                        cham.Parent = part
                        table.insert(chamsObjects, cham)
                    end
                end
            end
        end
        starterGui:SetCore("SendNotification", {Title = "ByEnserHub", Text = "Chams Aktif! [I]", Duration = 2})
    else
        for _, obj in pairs(chamsObjects) do obj:Destroy() end
        chamsObjects = {}
        starterGui:SetCore("SendNotification", {Title = "ByEnserHub", Text = "Chams Devre Dışı!", Duration = 2})
    end
end

local radar = false
local radarFrame = nil
local radarLabels = {}
local radarConnection = nil

local function toggleRadar()
    radar = not radar
    if radar then
        if not radarFrame then
            radarFrame = Instance.new("Frame")
            radarFrame.Size = UDim2.new(0, 200, 0, 200)
            radarFrame.Position = UDim2.new(0.8, 0, 0.1, 0)
            radarFrame.BackgroundColor3 = Color3.new(0.05, 0.05, 0.05)
            radarFrame.BackgroundTransparency = 0.3
            radarFrame.BorderSizePixel = 0
            radarFrame.Parent = screenGui
            local radarCorner = Instance.new("UICorner")
            radarCorner.CornerRadius = UDim.new(0, 100)
            radarCorner.Parent = radarFrame
            local radarTitle = Instance.new("TextLabel")
            radarTitle.Size = UDim2.new(1, 0, 0.1, 0)
            radarTitle.Position = UDim2.new(0, 0, 0.9, 0)
            radarTitle.BackgroundTransparency = 1
            radarTitle.Text = "RADAR"
            radarTitle.TextColor3 = Color3.new(1, 0.3, 0.3)
            radarTitle.TextSize = 12
            radarTitle.Font = Enum.Font.GothamBold
            radarTitle.Parent = radarFrame
        end
        if radarConnection then radarConnection:Disconnect() end
        radarConnection = runService.Heartbeat:Connect(function()
            if radar and radarFrame then
                for _, label in pairs(radarLabels) do label:Destroy() end
                radarLabels = {}
                local center = radarFrame.AbsoluteSize / 2
                for _, p in pairs(getEnemies()) do
                    if p.Character and p.Character:FindFirstChild("HumanoidRootPart") then
                        local tRoot = p.Character.HumanoidRootPart
                        local relativePos = rootPart.CFrame:ToObjectSpace(tRoot.CFrame).Position
                        local x = relativePos.X / 2
                        local z = relativePos.Z / 2
                        local label = Instance.new("TextLabel")
                        label.Size = UDim2.new(0, 10, 0, 10)
                        label.Position = UDim2.new(0, center.X + x, 0, center.Y + z)
                        label.BackgroundTransparency = 1
                        label.Text = "•"
                        label.TextColor3 = getPlayerColor(p)
                        label.TextSize = 16
                        label.Font = Enum.Font.GothamBold
                        label.Parent = radarFrame
                        table.insert(radarLabels, label)
                    end
                end
            end
        end)
        starterGui:SetCore("SendNotification", {Title = "ByEnserHub", Text = "Radar Aktif! [P]", Duration = 2})
    else
        if radarConnection then radarConnection:Disconnect(); radarConnection = nil end
        if radarFrame then radarFrame:Destroy(); radarFrame = nil end
        for _, label in pairs(radarLabels) do label:Destroy() end
        radarLabels = {}
        starterGui:SetCore("SendNotification", {Title = "ByEnserHub", Text = "Radar Devre Dışı!", Duration = 2})
    end
end

local themeIndex = 1
local themes = {
    {bg = Color3.new(0.05, 0.05, 0.08), btn = Color3.new(0.15, 0.15, 0.2), text = Color3.new(1, 0.3, 0.3)},
    {bg = Color3.new(0.08, 0.05, 0.15), btn = Color3.new(0.2, 0.1, 0.3), text = Color3.new(0.8, 0.3, 1)},
    {bg = Color3.new(0.05, 0.15, 0.05), btn = Color3.new(0.1, 0.3, 0.1), text = Color3.new(0.3, 1, 0.3)},
    {bg = Color3.new(0.15, 0.15, 0.05), btn = Color3.new(0.3, 0.3, 0.1), text = Color3.new(1, 1, 0.3)},
    {bg = Color3.new(0.15, 0.05, 0.05), btn = Color3.new(0.3, 0.1, 0.1), text = Color3.new(1, 0.3, 0.3)},
    {bg = Color3.new(0.05, 0.05, 0.15), btn = Color3.new(0.1, 0.1, 0.3), text = Color3.new(0.3, 0.5, 1)},
    {bg = Color3.new(0.15, 0.05, 0.1), btn = Color3.new(0.3, 0.1, 0.2), text = Color3.new(1, 0.4, 0.8)},
    {bg = Color3.new(0.05, 0.1, 0.15), btn = Color3.new(0.1, 0.2, 0.3), text = Color3.new(0.3, 0.8, 1)}
}

local function toggleTheme()
    themeIndex = themeIndex + 1
    if themeIndex > #themes then themeIndex = 1 end
    local theme = themes[themeIndex]
    if mainFrame then mainFrame.BackgroundColor3 = theme.bg end
    if titleBar then titleBar.BackgroundColor3 = theme.bg + Color3.new(0.1, 0.05, 0.05) end
    if titleText then titleText.TextColor3 = theme.text end
    starterGui:SetCore("SendNotification", {Title = "ByEnserHub", Text = "Tema Değiştirildi! [T]", Duration = 2})
end

userInput.InputBegan:Connect(function(input, gameProcessed)
    if gameProcessed then return end
    local key = input.KeyCode
    if key == Keys.ToggleUI then
        if screenGui then
            screenGui.Enabled = not screenGui.Enabled
        end
    elseif key == Keys.ToggleAimbot then
        toggleAimbot()
    elseif key == Keys.ToggleSilentAim then
        toggleSilentAim()
    elseif key == Keys.ToggleTriggerBot then
        toggleTriggerBot()
    elseif key == Keys.ToggleESP then
        toggleESP()
    elseif key == Keys.ToggleAutoShoot then
        toggleAutoShoot()
    elseif key == Keys.ToggleFly then
        toggleFly()
    elseif key == Keys.ToggleSpeed then
        toggleSpeed()
    elseif key == Keys.ToggleNoclip then
        toggleNoclip()
    elseif key == Keys.ToggleBombJump then
        toggleBombJump()
    elseif key == Keys.TeleportToGun then
        teleportToGun()
    elseif key == Keys.FlingMurderer then
        flingMurderer()
    elseif key == Keys.FlingSheriff then
        flingSheriff()
    elseif key == Keys.MassKill then
        massKill()
    elseif key == Keys.ToggleTheme then
        toggleTheme()
    elseif key == Keys.ToggleWallhack then
        toggleWallhack()
    elseif key == Keys.ToggleNightVision then
        toggleNightVision()
    elseif key == Keys.ToggleInfiniteEnergy then
        toggleInfiniteEnergy()
    elseif key == Keys.ToggleAutoHeal then
        toggleAutoHeal()
    elseif key == Keys.ToggleGunESP then
        toggleGunESP()
    elseif key == Keys.ToggleNoRecoil then
        toggleNoRecoil()
    elseif key == Keys.ToggleNoSpread then
        toggleNoSpread()
    elseif key == Keys.ToggleInstantReload then
        toggleInstantReload()
    elseif key == Keys.ToggleSpinBot then
        toggleSpinBot()
    elseif key == Keys.ToggleAntiAim then
        toggleAntiAim()
    elseif key == Keys.ToggleTracers then
        toggleTracers()
    elseif key == Keys.ToggleChams then
        toggleChams()
    elseif key == Keys.ToggleRadar then
        toggleRadar()
    end
end)

local screenGui = Instance.new("ScreenGui")
screenGui.Name = "ByEnserHub"
screenGui.Parent = player.PlayerGui
screenGui.ResetOnSpawn = false

local mainFrame = Instance.new("Frame")
mainFrame.Size = UDim2.new(0, 280, 0, 550)
mainFrame.Position = UDim2.new(0, 10, 0, 10)
mainFrame.BackgroundColor3 = Color3.new(0.05, 0.05, 0.08)
mainFrame.BackgroundTransparency = 0.1
mainFrame.BorderSizePixel = 0
mainFrame.Parent = screenGui

local mainCorner = Instance.new("UICorner")
mainCorner.CornerRadius = UDim.new(0, 10)
mainCorner.Parent = mainFrame

local titleBar = Instance.new("Frame")
titleBar.Size = UDim2.new(1, 0, 0, 40)
titleBar.BackgroundColor3 = Color3.new(0.2, 0.05, 0.05)
titleBar.BackgroundTransparency = 0
titleBar.Parent = mainFrame

local titleCorner = Instance.new("UICorner")
titleCorner.CornerRadius = UDim.new(0, 10)
titleCorner.Parent = titleBar

local titleText = Instance.new("TextLabel")
titleText.Size = UDim2.new(0.7, 0, 1, 0)
titleText.Position = UDim2.new(0.05, 0, 0, 0)
titleText.BackgroundTransparency = 1
titleText.Text = "ByEnserHub"
titleText.TextColor3 = Color3.new(1, 0.3, 0.3)
titleText.TextSize = 18
titleText.Font = Enum.Font.GothamBold
titleText.TextXAlignment = Enum.TextXAlignment.Left
titleText.Parent = titleBar

local minimizeBtn = Instance.new("TextButton")
minimizeBtn.Size = UDim2.new(0, 30, 0, 30)
minimizeBtn.Position = UDim2.new(0.7, 0, 0, 5)
minimizeBtn.BackgroundColor3 = Color3.new(0.3, 0.3, 0.3)
minimizeBtn.BackgroundTransparency = 0
minimizeBtn.Text = "_"
minimizeBtn.TextColor3 = Color3.new(1, 1, 1)
minimizeBtn.TextSize = 18
minimizeBtn.Font = Enum.Font.GothamBold
minimizeBtn.Parent = titleBar

local minCorner = Instance.new("UICorner")
minCorner.CornerRadius = UDim.new(0, 5)
minCorner.Parent = minimizeBtn

local closeBtn = Instance.new("TextButton")
closeBtn.Size = UDim2.new(0, 30, 0, 30)
closeBtn.Position = UDim2.new(0.88, 0, 0, 5)
closeBtn.BackgroundColor3 = Color3.new(1, 0.2, 0.2)
closeBtn.BackgroundTransparency = 0
closeBtn.Text = "X"
closeBtn.TextColor3 = Color3.new(1, 1, 1)
closeBtn.TextSize = 16
closeBtn.Font = Enum.Font.GothamBold
closeBtn.Parent = titleBar

local closeCorner = Instance.new("UICorner")
closeCorner.CornerRadius = UDim.new(0, 5)
closeCorner.Parent = closeBtn

local isMinimized = false
minimizeBtn.MouseButton1Click:Connect(function()
    isMinimized = not isMinimized
    if isMinimized then
        mainFrame.Size = UDim2.new(0, 280, 0, 40)
        scrollFrame.Visible = false
        minimizeBtn.Text = "+"
    else
        mainFrame.Size = UDim2.new(0, 280, 0, 550)
        scrollFrame.Visible = true
        minimizeBtn.Text = "_"
    end
end)

closeBtn.MouseButton1Click:Connect(function()
    screenGui:Destroy()
end)

local scrollFrame = Instance.new("ScrollingFrame")
scrollFrame.Size = UDim2.new(1, -10, 1, -50)
scrollFrame.Position = UDim2.new(0, 5, 0, 45)
scrollFrame.BackgroundTransparency = 1
scrollFrame.Parent = mainFrame
scrollFrame.CanvasSize = UDim2.new(0, 0, 0, 0)

local y = 5
local function addButton(text, func, color, key)
    local btn = Instance.new("TextButton")
    btn.Size = UDim2.new(1, -10, 0, 32)
    btn.Position = UDim2.new(0, 5, 0, y)
    btn.Text = text .. " [" .. key .. "]"
    btn.BackgroundColor3 = color or Color3.new(0.15, 0.15, 0.2)
    btn.BackgroundTransparency = 0
    btn.TextColor3 = Color3.new(1, 1, 1)
    btn.TextSize = 12
    btn.Font = Enum.Font.Gotham
    btn.BorderSizePixel = 0
    btn.Parent = scrollFrame
    local btnCorner = Instance.new("UICorner")
    btnCorner.CornerRadius = UDim.new(0, 5)
    btnCorner.Parent = btn
    btn.MouseButton1Click:Connect(function() pcall(func) end)
    y = y + 37
    scrollFrame.CanvasSize = UDim2.new(0, 0, 0, y + 10)
end

addButton("🎯 Aimbot", toggleAimbot, Color3.new(0.3, 0.1, 0.1), "Z")
addButton("🔇 Silent Aim", toggleSilentAim, Color3.new(0.2, 0.1, 0.3), "Q")
addButton("🔫 Trigger Bot", toggleTriggerBot, Color3.new(0.3, 0.2, 0.1), ";")
addButton("👤 ESP", toggleESP, Color3.new(0.1, 0.2, 0.1), "X")
addButton("🔫 Auto Shoot", toggleAutoShoot, Color3.new(0.2, 0.1, 0.2), "C")
addButton("🦅 Fly", toggleFly, Color3.new(0.1, 0.2, 0.3), "V")
addButton("💨 Speed", toggleSpeed, Color3.new(0.2, 0.3, 0.1), "B")
addButton("🌀 No Clip", toggleNoclip, Color3.new(0.2, 0.1, 0.3), "N")
addButton("💥 Bomb Jump", toggleBombJump, Color3.new(0.3, 0.2, 0.1), "M")
addButton("🔫 Teleport Gun", teleportToGun, Color3.new(0.1, 0.3, 0.2), "G")
addButton("🔄 Fling Katil", flingMurderer, Color3.new(0.3, 0.1, 0.1), "F")
addButton("🔄 Fling Şerif", flingSheriff, Color3.new(0.1, 0.1, 0.3), "H")
addButton("💀 Mass Kill", massKill, Color3.new(0.3, 0.1, 0.1), "K")
addButton("🎨 Tema", toggleTheme, Color3.new(0.2, 0.1, 0.3), "T")
addButton("👁️ Wallhack", toggleWallhack, Color3.new(0.1, 0.1, 0.3), "W")
addButton("🌙 Night Vision", toggleNightVision, Color3.new(0.1, 0.1, 0.2), "E")
addButton("♾️ Infinite Energy", toggleInfiniteEnergy, Color3.new(0.1, 0.3, 0.3), "R")
addButton("❤️ Auto Heal", toggleAutoHeal, Color3.new(0.1, 0.3, 0.1), "Y")
addButton("🔫 Gun ESP", toggleGunESP, Color3.new(0.3, 0.2, 0.1), ",")
addButton("🛡️ No Recoil", toggleNoRecoil, Color3.new(0.1, 0.2, 0.2), "\\")
addButton("🎯 No Spread", toggleNoSpread, Color3.new(0.2, 0.3, 0.2), "]")
addButton("🔄 Instant Reload", toggleInstantReload, Color3.new(0.3, 0.1, 0.2), "[")
addButton("🔄 Spin Bot", toggleSpinBot, Color3.new(0.2, 0.1, 0.4), "L")
addButton("🎯 Anti Aim", toggleAntiAim, Color3.new(0.3, 0.2, 0.2), "U")
addButton("📡 Tracers", toggleTracers, Color3.new(0.1, 0.3, 0.3), "O")
addButton("💎 Chams", toggleChams, Color3.new(0.1, 0.2, 0.3), "I")
addButton("📡 Radar", toggleRadar, Color3.new(0.2, 0.3, 0.3), "P")

print("ByEnserHub Yüklendi!")
starterGui:SetCore("SendNotification", {Title = "ByEnserHub", Text = "27 Özellik Yüklendi! [RightCtrl]", Duration = 3})
