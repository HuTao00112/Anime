if not game:IsLoaded() then
   game.Loaded:Wait()
end
local TeleportService = game:GetService("TeleportService")
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local Players = game:GetService("Players")
local Player = Players.LocalPlayer

local playerGui = Player:WaitForChild("PlayerGui")

local placeId = 7387924609


-- teleport the user
if game.PlaceId ~= placeId then
   TeleportService:Teleport(placeId)
end
 
task.wait(2)

ReplicatedStorage.Remotes.Equip:FireServer("Goku") -- Wherever you see this just change it to your character to change the character you wanan farm with.
getgenv().Autofarm = true
task.spawn(function()
   while getgenv().Autofarm and task.wait() do
       pcall(function()
           for i,v in next, Players:GetChildren() do
               if v.Character.Humanoid.Health > 0 and v.Character.Name ~= game.Players.LocalPlayer.Name then
                   repeat task.wait()
                   Player.Character.HumanoidRootPart.CFrame = v.Character.HumanoidRootPart.CFrame + (v.Character.HumanoidRootPart.CFrame.lookVector*-3)
                   until v.Character.Humanoid.Health <= 0 or not getgenv().Autofarm
               end
           end
       end)
   end
end)
 
   
while task.wait() do
   if Player:FindFirstChild("Backpack") and Player.Backpack:FindFirstChild("Goku") and Player.Backpack.CharacterNameHere:FindFirstChild("Combat") then
       Player.Backpack.CharacterNameHere.Combat:FireServer("Combo1") -- Change character name to any character you want to farm with
   end
end
