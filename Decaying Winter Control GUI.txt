local library = loadstring(game:HttpGet("https://raw.githubusercontent.com/oShyyyyy/Plaguecheat.cc-Roblox-Ui-library/main/Source.lua", true))()

getgenv().Esp = false
getgenv().factiontype = 1
getgenv().typename = nil
getgenv().tpwalking = false
getgenv().Controlling = false

local Main = library:AddWindow('Main')
local watermark = library:AddWatermark('');

local RunService = game:GetService("RunService")
local UIS = game:GetService("UserInputService")
local Players = game:GetService("Players")
local Player = Players.LocalPlayer

local ActiveHostiles = workspace:FindFirstChild("activeHostiles")

local e = Main:AddSection('Control NPC')

local f = Main:AddSection('ESP')

local ShadowColor = Color3.fromRGB(114, 47, 55)
local FunColor = Color3.fromRGB(255, 255, 0)
local normalscav = Color3.fromRGB(255, 165, 0)
local Mouse = Player:GetMouse()

local hb = RunService.Heartbeat




local GUIs = {}

-- local function resetChar()
--     local SpectatingPlayers = workspace:FindFirstChild("speccingPlayers")

--     Player = Players.LocalPlayer
--     local Character = workspace:FindFirstChild(Player.Name)

--     if Character then
--         local newClone = Character:Clone()
--         newClone.Parent = workspace

--         print("successful")
--         local CC = CharacterClone:Clone()

--         Character:Destroy()
--         CC.Parent = SpectatingPlayers
--         Player.Character = CC

        
--     else
--         print("not sure if successful")
--         local CC = CharacterClone:Clone()

--         CC.Parent = SpectatingPlayers
--         Player.Character = CC

--         local newClone = Player.Character:Clone()
--         newClone.Parent = workspace
--     end
--     --ClonedCharacter = player.Character:Clone()
-- end

function GetCharacter()
    return game.Players.LocalPlayer.Character
 end
   
 function Teleport(pos)
    local Char = GetCharacter()
    if Char then
        Char:MoveTo(pos)
    end
 end

local function Control()
    coroutine.wrap(function()
        for i, nameval in pairs(ActiveHostiles:GetDescendants()) do
            if nameval.Name == "ai_type" then
                if typename == nameval.Value then
                    local AI = nameval.Parent  

                    if not Contrlling then
                        local SpectatingCharacter = workspace.speccingPlayers:FindFirstChild(Player.Character.Name)

                        local Model = Instance.new("Model", workspace.speccingPlayers)
                        Model.Name = Player.Name

                        if SpectatingCharacter then
                            for i, v in pairs(SpectatingCharacter:GetChildren()) do
                                if v then
                                    local clones = v:Clone()
                                    clones.Parent = Model
                                end
                            end
                        end
                    end

                    

                    local Menu = game:GetService("Players").LocalPlayer.PlayerGui.mainHUD:Clone()

                    local storedCamera1, storedCamera2 = workspace.CurrentCamera.CameraSubject, workspace.CurrentCamera.CameraType

                    local controlling = AI
                    local friendly = true

                    local Players = game:GetService("Players")
                    local RunService = game:GetService("RunService")
                    local rs = game:GetService("ReplicatedStorage")

                    local playergui = Player.PlayerGui
                    local ms = Player:GetMouse()

                    local SpectatingPlayers = workspace:FindFirstChild("speccingPlayers")

                    local player = Players.LocalPlayer

                    player.Character = controlling

                    -- Setting Camera Up
                    workspace.CurrentCamera.CameraSubject = controlling
                    workspace.CurrentCamera.CameraType = "Custom"

                    controlling.Humanoid:GetPropertyChangedSignal("WalkToPoint"):Connect(function()
                        local CHum = controlling:FindFirstChildWhichIsA("Humanoid")
                        local CHumrp = controlling:FindFirstChild("HumanoidRootPart")
                        if CHum and CHumrp then
                            CHum.WalkToPoint = CHumrp.Position
                        end
                    end)

                    if controlling:FindFirstChild("HumanoidRootPart") then
                        local HumanoidRootPart = SpectatingPlayers[player.Name]:FindFirstChild("HumanoidRootPart")
                        
                        if HumanoidRootPart then
                            local BodyPosition = HumanoidRootPart:FindFirstChild("BodyPosition")
                            if BodyPosition then
                                BodyPosition:Destroy()
                            end
                            
                            HumanoidRootPart.Anchored = false
                            HumanoidRootPart.CFrame = controlling.HumanoidRootPart.CFrame - Vector3.new(0,10,0)
                        end
                        
                        task.wait(0.2)
                        
                            --[[spawn(function()
                                game:GetService('RunService').Stepped:connect(function()
                                    workspace.speccingPlayers[game.Players.LocalPlayer.Name].Humanoid:ChangeState(11)
                                    end)
                                end)--]]
                            
                        task.spawn(function()
                            local lp = Players.LocalPlayer
                            local c = SpectatingPlayers[lp.Name]
                            local hrp0 = c:FindFirstChild("HumanoidRootPart")
                            local hrp1 = hrp0:Clone()
                            
                            Controlling = true

                            c.Parent = nil
                            hrp0.Parent = hrp1
                            hrp0.RootJoint.Part0 = nil
                            hrp1.Parent = c
                            
                            local h = RunService.Heartbeat
                            
                            c.Parent = workspace

                            spawn(function()
                                hrp0.Transparency = 0.5
                                
                                while h:Wait() and c and c.Parent do
                                    hrp0.CFrame = hrp1.CFrame
                                    hrp0.Orientation += Vector3.new(0, 0, 180)
                                    hrp0.Position = controlling.HumanoidRootPart.Position - Vector3.new(0,10,0)
                                    hrp0.Velocity = hrp1.Velocity
                                end
                            end)
                        end)

                    end
                end
            end
        end
    end)()
end

local function creategui(npc, color, text)
    coroutine.wrap(function()
        local BillboardGui = Instance.new("BillboardGui")
        local Name = Instance.new("TextLabel")
        local Dist = Instance.new("TextLabel")

        --Properties:

        BillboardGui.AlwaysOnTop = true
        BillboardGui.Name = "TestingLol"
        BillboardGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
        BillboardGui.Active = true
        BillboardGui.LightInfluence = 1.000
        BillboardGui.Size = UDim2.new(20, 0, 20, 0)
        BillboardGui.StudsOffsetWorldSpace = Vector3.new(0, 8, 0)
        BillboardGui.Parent = npc


        Name.Name = "Name"
        Name.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
        Name.BackgroundTransparency = 1.000
        Name.Position = UDim2.new(0, 0, 0.100000001, 0)
        Name.Size = UDim2.new(1, 0, 0.300000012, 0)
        Name.Font = Enum.Font.Gotham
        Name.Text = text
        Name.TextColor3 = color
        Name.TextScaled = false
        Name.TextSize = 10
        Name.TextWrapped = true
        Name.Parent = BillboardGui
    end)()
end

local function changecolor(npc, color)
    local GUI = npc:FindFirstChildOfClass("BillboardGui")
    if GUI then
        local Name = GUI:FindFirstChildOfClass("TextLabel")
        Name.TextColor3 = color
    end
end

local function Loop()
    -- ESP --

    local char = workspace:FindFirstChild(Player.Name)
    local controlledchar = Player.Character

    local SpectatingPlayers = workspace:FindFirstChild("speccingPlayers")

    if Controlling and char then
        if controlledchar.Parent == nil then      
            local SpectatingCharacter = SpectatingPlayers:FindFirstChild(Player.Name)

            for i, v in pairs(SpectatingCharacter:GetChildren()) do
                if v:IsA("BasePart") and v.Name ~= "HumanoidRootPart" then
                    v.Parent = char
                end
            end

            SpectatingCharacter:Destroy()

            Player.Character = char
            char.Parent = SpectatingPlayers
        end
    end

    if Esp then
        for i, npc in pairs(ActiveHostiles:GetChildren()) do
            local ai_type = npc:FindFirstChild("ai_type")
            local faction = npc:FindFirstChild("faction")
    
            local check = npc:FindFirstChildOfClass("Highlight")
            local checkgui = npc:FindFirstChildOfClass("BillboardGui")

            if ai_type and not check and not checkgui and faction.Value == factiontype then
                if factiontype == 1 then
                    local hl = Instance.new("Highlight")
                    hl.OutlineColor = normalscav
                    hl.FillTransparency = 1
                    hl.Parent = npc

                    creategui(npc, normalscav, ai_type.Value)

                    if ai_type.Value == "BossFunRuiner" then
                        hl.OutlineColor = FunColor
                        changecolor(npc, FunColor)
                    end

                    if ai_type.Value == "ShadowSkinnerA" or ai_type.Value == "ShadowSkinnerB" or ai_type.Value == "ShadowSkinnerC" then
                        hl.OutlineColor = ShadowColor
                        changecolor(npc, ShadowColor)     
                    end      

                    for i, dude in pairs(ActiveHostiles:GetChildren()) do
                        local faction1 = dude:FindFirstChild("faction")
                
                        local check1 = dude:FindFirstChildOfClass("Highlight")
                        local check2 = dude:FindFirstChildOfClass("BillboardGui")
                        
                        if faction1 then
                            if faction1.Value == 2 and check1 and check2 then
                                check1:Destroy()
                                check2:Destroy()
                            end
                        end

                        
                    end
                else
                    local hl = Instance.new("Highlight")
                    hl.FillTransparency = 1
                    hl.OutlineColor = ShadowColor
                    hl.Parent = npc

                    creategui(npc, ShadowColor, ai_type.Value)

                    for i, dude in pairs(ActiveHostiles:GetChildren()) do
                        local faction1 = dude:FindFirstChild("faction")
                
                        local check1 = dude:FindFirstChildOfClass("Highlight")
                        local check2 = dude:FindFirstChildOfClass("BillboardGui")
            
                        if faction1 then
                            if faction1.Value == 1 and check1 and check2 then
                                check1:Destroy()
                                check2:Destroy()
                            end
                        end
                    end

                end
            end

        end
    else
        for i, npc in pairs(ActiveHostiles:GetChildren()) do
            local yes = npc:FindFirstChildOfClass("Highlight")
            local yes2 = npc:FindFirstChildOfClass("BillboardGui")
    
            if yes and yes2 then
                yes:Destroy()
                yes2:Destroy()
            end
        end
    end
    -- teleport walking

    coroutine.wrap(function()
        local chr = Players.LocalPlayer.Character
        local hum = chr and chr:FindFirstChildWhichIsA("Humanoid")
        while tpwalking and chr and hum and hum.Parent do
            local delta = hb:Wait()
            if hum.MoveDirection.Magnitude > 0 then
                chr:TranslateBy(hum.MoveDirection * 10 * delta * 10)
            end
        end
    end)()
end

f:AddLabel('Toggles the ESP, this will show you what to enter inside the Controlling Section.')

f:AddSeparateBar()

f:AddToggle('Esp', true, nil, function(v)
    Esp = v
end)

f:AddLabel('This specifies what the esp will show.')

f:AddDropdown('Esp Priority',{1, 2},'1',function(a) factiontype = tonumber(a) end)

f:AddSeparateBar()

f:AddKeyBind('Gui Toggle', Enum.KeyCode.Insert, function() 
    local CoreGui = game.CoreGui
    local PCR_1 = CoreGui:FindFirstChild("PCR_1")
    if PCR_1 then
        local frame = PCR_1:FindFirstChildOfClass("Frame")
        if frame then
            if not frame.Visible then
                frame.Visible = true
            else
                frame.Visible = false
            end
        end
    end
end)

e:AddLabel('Note; Turn on esp and enter the name inside the textbox. (Case Sensitive)')

e:AddTextBox('NPC_Name', nil, false, 3, function(a)
    typename = tostring(a)
end)

e:AddButton('Control NPC', Control)

e:AddLabel('Another note; Make sure to set spectate mode ON via settings at the menu before you control any npc.')

e:AddSeparateBar()

e:AddLabel('Miscellaneous')

e:AddToggle('Teleport Walk (Not recommended)', true, nil, function(v)
    tpwalking = v
end)

e:AddLabel('Ctrl + Click Tp is a feature of the GUI, use it instead of TP Walk.')

-- e:AddLabel('Note; Use Reset Character if bugged.')

-- e:AddButton('Reset Character', resetChar)

e:AddLabel('Made by - incorrectdecisions')
e:AddLabel('UI - oSheep')
e:AddLabel('Teleport Walk - Infinite Yield')
e:AddLabel('Original Control script - Ry')

UIS.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 and UIS:IsKeyDown(Enum.KeyCode.LeftControl) then
        Teleport(Mouse.Hit.p)
    end
 end)

RunService:BindToRenderStep("Tag", 1, Loop)

