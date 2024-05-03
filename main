--Credit to xz#1111 for source
local Ui =
    loadstring(
    game:HttpGet(
        "https://raw.githubusercontent.com/drillygzzly/Roblox-UI-Libs/main/Abyss%20Lib/Abyss%20Lib%20Source.lua"
    )
)()
local Ui = Library

local LoadTime = tick()

local Loader = Library.CreateLoader("Showdown Football", Vector2.new(300, 300))

local Window = Library.Window("Showdown Football", Vector2.new(500, 620))

Window.SendNotification("Normal", "Press RightShift to open menu and close menu!", 10)

Window.Watermark("")
local Tab1 = Window:Tab("Main")
local Section1 = Tab1:Section("Game", "Left")

Section1:Toggle(
    {
        Title = "Ball Mag",
        Flag = "Toggle_1",
        Type = "Dangerous",
        Callback = function(v)
            print(v)

            local partName = "Football"
            teleportDistance = 20
            _G.on = v
            local function findPart()
                return workspace:FindFirstChild(partName)
            end
            local function distance(pos1, pos2)
                return (pos1 - pos2).magnitude
            end
            while _G.on == true do
                wait(0.1)

                if _G.on then
                    local part = findPart()
                    if part then
                        local partPosition = part.Position
                        local character = game.Players.LocalPlayer.Character
                        local rightArm = character and character:FindFirstChild("Right Arm")
                        local leftArm = character and character:FindFirstChild("Left Arm")
                        local rightHandPosition = rightArm and rightArm.Position
                        local leftHandPosition = leftArm and leftArm.Position
                        if rightHandPosition and leftHandPosition then
                            local distToRightHand = distance(partPosition, rightHandPosition)
                            local distToLeftHand = distance(partPosition, leftHandPosition)
                            if distToRightHand <= distToLeftHand and distToRightHand <= teleportDistance then
                                part.CFrame = CFrame.new(rightHandPosition)
                            elseif distToLeftHand <= teleportDistance then
                                part.CFrame = CFrame.new(leftHandPosition)
                            end
                        elseif rightHandPosition and distance(partPosition, rightHandPosition) <= teleportDistance then
                            part.CFrame = CFrame.new(rightHandPosition)
                        elseif leftHandPosition and distance(partPosition, leftHandPosition) <= teleportDistance then
                            part.CFrame = CFrame.new(leftHandPosition)
                        end
                    end
                end
            end
        end
    }
):Keybind(
    {
        Title = "KeybindToggle1",
        Flag = "Keybind_Toggle_1",
        Key = Enum.KeyCode.T,
        StateType = "Toggle"
    }
)

Section1:Slider(
    {
        Title = "Ball Mag Distance",
        Flag = "Ball Mag Distance",
        Symbol = "",
        Default = 20,
        Min = 1,
        Max = 500,
        Decimals = 1,
        Callback = function(v)
            print("Value = " .. v)
            teleportDistance = v
        end
    }
)

Section1:Button(
    {
        Title = "Tackle Player",
        Callback = function()
            print("Pressed!")

            local function tackleplr()
                for _, v in pairs(workspace:GetDescendants()) do
                    if v:IsA("Model") and v:FindFirstChild("Football") then
                        local playerName = v.Name
                        local plr = game.Players:FindFirstChild(playerName)
                        if plr then
                            print("Player Team:", plr.Team)
                            print("Local Player Team:", game.Players.LocalPlayer.Team)
                            if plr.Team ~= game.Players.LocalPlayer.Team then
                                local now = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame
                                repeat
                                    wait()
                                    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame =
                                        plr.Character.HumanoidRootPart.CFrame
                                until plr.Character.Humanoid.Health ~= 75
                                wait()
                                game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = now
                            else
                                warn("Player on your team")
                            end
                        end
                    end
                end
            end

            tackleplr()
        end
    }
)

Section1:Button(
    {
        Title = "Touchdown",
        Callback = function()
            print("Pressed!")
            local function td()
                local now = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame

                game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = workspace.Field.Endzone1.CFrame
                wait()
                game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = workspace.Field.Endzone2.CFrame
                wait(0.5)
                game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = now
            end
            if game.Players.LocalPlayer.Character:FindFirstChild("Football") then
                td()
            else
                warn("You don't have the football")
            end
        end
    }
)

Window:AddSettingsTab()
Window:SwitchTab(Tab1)
Window.ToggleAnime(false)
LoadTime = math.floor((tick() - LoadTime) * 1000)
