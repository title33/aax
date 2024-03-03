

function TP(targetCFrame)
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = targetCFrame
end

function AA()
    game:GetService('VirtualUser'):CaptureController()
    game:GetService('VirtualUser'):Button1Down(Vector2.new(1280, 672))
end

function No()
    for _, v in ipairs(workspace.Lives:GetChildren()) do
        if not game:GetService("Players"):GetPlayerFromCharacter(v) then
            local cleanedName = string.gsub(v.Name, "%d+$", "")
            v.Name = tostring(cleanedName)
        end
    end
end

workspace.Lives.ChildAdded:Connect(function(model)
    task.wait()
    if not game:GetService("Players"):GetPlayerFromCharacter(model) then
        local cleanedName = string.gsub(model.Name, "%d+$", "")
        model.Name = cleanedName
    end
end)

function CheckLV()
    local MyLv = tonumber(game.Players.LocalPlayer.PlayerGui.MainUI.Interface.PlayerStatus.Frame.Level.TextLabel.Text:match('%d+'))
    
    if MyLv == 1 or MyLv <= 49 then
        Mon = "Bandit [LV.5]"
        CFQ = CFrame.new(-953.566528, 34.5999947, -552.164612, -0.0109250434, -3.3378329e-09, -0.999940336, 1.94075778e-09, 1, -3.35923622e-09, 0.999940336, -1.97734162e-09, -0.0109250434)
    elseif MyLv == 50 or MyLv <= 99 then
        Mon = "Bandit Leader [LV.15]"
        CFQ = CFrame.new(-1097.55042, 34.6000023, -492.550354, -0.0683717504, 2.67226739e-08, 0.997659922, 5.38579563e-08, 1, -2.30943531e-08, -0.997659922, 5.21529238e-08, -0.0683717504)
    elseif MyLv == 100 or MyLv <= 199 then
        Mon = "Clown Pirate [LV.50]"
        CFQ = CFrame.new(-71.5784531, 36.4347496, 50.7921715, 0.00707866857, 2.668971e-08, 0.999974966, -5.85915032e-08, 1, -2.62756199e-08, -0.999974966, -5.84040372e-08, 0.00707866857)
    elseif MyLv == 200 or MyLv <= 299 then
        Mon = "Marine [LV.300]"
        CFQ = CFrame.new(848.661377, 35.5073013, 1264.83777, -0.998497367, 5.36386899e-08, 0.0548002385, 5.90094018e-08, 1, 9.63871685e-08, -0.0548002385, 9.94760612e-08, -0.998497367)
    elseif MyLv == 300 or MyLv <= 399 then
        Mon = "Monkey [LV.750]"
        CFQ = CFrame.new(771.192871, 42.3243141, -1220.74805, -0.996942639, 2.59707669e-08, 0.0781369284, 2.55865924e-08, 1, -5.91784355e-09, -0.0781369284, -3.90049282e-09, -0.996942639)
    elseif MyLv == 400 or MyLv <= 499 then
        Mon = "Monkey King [LV.1000]"
        CFQ = CFrame.new(727.094971, 42.2545357, -1380.22131, -0.0418852083, 2.64795439e-08, 0.999122441, -2.36735005e-08, 1, -2.74952416e-08, -0.999122441, -2.48043701e-08, -0.0418852083)
    elseif MyLv == 500 or MyLv <= 599 then
        Mon = "Bomb Man [LV.1500]"
        CFQ = nil
    elseif MyLv == 600 or MyLv <= 699 then
        Mon = "Sand Man [LV.2000]"
        CFQ = nil
    elseif MyLv == 700 or MyLv <= 799 then
        Mon = "Snow Bandit [LV.1750]"
        CFQ = CFrame.new(1507.57898, 102.05999, -290.12558, -0.998586833, -8.202373e-09, -0.0531440228, -1.01186872e-08, 1, 3.57898209e-08, 0.0531440228, 3.62769903e-08, -0.998586833)
    elseif MyLv == 800 or MyLv <= 899 then
        Mon = "Snow Bandit Leader [LV.2350]"
        CFQ = nil
    elseif MyLv > 900 then
        Mon = "Snow Bandit [LV.1750]"
        CFQ = CFrame.new(1507.57898, 102.05999, -290.12558, -0.998586833, -8.202373e-09, -0.0531440228, -1.01186872e-08, 1, 3.57898209e-08, 0.0531440228, 3.62769903e-08, -0.998586833)
    end
end


_G.AutoFarmlv = true
spawn(function()
    while wait() do
        if _G.AutoFarmlv then
            pcall(function()
                CheckLV()
                if not game.Players.LocalPlayer.PlayerGui:FindFirstChild("QuestUI") then
                    repeat
                        task.wait()
                        TP(CFQ)
                    until not _G.AutoFarmlv or game.Players.LocalPlayer.PlayerGui:FindFirstChild("QuestUI")
                elseif game.Players.LocalPlayer.PlayerGui:FindFirstChild("QuestUI") then
                    CheckLV()
                    No()
                    for _,v in pairs(game:GetService("Workspace").Lives:GetChildren()) do
                        if v.Name == Mon and v.Humanoid.Health > 0  then
                            v.HumanoidRootPart.Size = Vector3.new(10,10,10)
                            v.HumanoidRootPart.Transparency = 0.9
                            v.Humanoid.WalkSpeed = 0
                            v.Humanoid.JumpPower = 0
                            repeat
                                task.wait()
                                AA()
                                TP(v.HumanoidRootPart.CFrame * CFrame.new(0,5,0) * CFrame.Angles(math.rad(-90),0,0))
                            until not _G.AutoFarmMob or v.Humanoid.Health <= 0
                        end
                    end
                end
            end)
        end
    end
end)




_G.bringmob = true
while _G.bringmob do 
    wait()
    pcall(function()
        for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
            for x,y in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
                if v.Name == Mon then
                    if y.Name == Mon then
                        v.HumanoidRootPart.CFrame = y.HumanoidRootPart.CFrame
                        v.HumanoidRootPart.Size = Vector3.new(60,60,60)
                        y.HumanoidRootPart.Size = Vector3.new(60,60,60)
                        v.HumanoidRootPart.Transparency = 1
                        v.HumanoidRootPart.CanCollide = false
                        y.HumanoidRootPart.CanCollide = false
                        v.Humanoid.WalkSpeed = 0
                        y.Humanoid.WalkSpeed = 0
                        v.Humanoid.JumpPower = 0
                        y.Humanoid.JumpPower = 0
                        if sethiddenproperty then
                            sethiddenproperty(game.Players.LocalPlayer, "SimulationRadius", math.huge)
                        end
                    end
                end
            end
        end
        No()  -- เพิ่ม No() เข้าไปในลูป while
    end)
end
