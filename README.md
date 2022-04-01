--> variables
local UIS = game:GetService("UserInputService")
local camera = game.Workspace.CurrentCamera
--> getting the closest player
function getClosest()
	local closestPlayer = nil
	local closesDist = math.huge
	for i,v in pairs(game.Players:GetPlayers()) do
		if v ~= game.Players.LocalPlayer then
			local Dist = (game.Players.LocalPlayer.Character.HumanoidRootPart.Position - v.Character.HumanoidRootPart.Position).magnitude
			if Dist < closesDist then
				closesDist = Dist
				closestPlayer = v
			end
		end
	end
	return closestPlayer
end


_G.aim = false
UIS.InputBegan:Connect(function(inp)
	if inp.KeyCode == Enum.KeyCode.Q  then
		_G.aim = true
		while wait() do
			camera.CFrame = CFrame.new(camera.CFrame.Position,getClosest().Character.Head.Position)
			if _G.aim == false then return end
		end
	end
end)

UIS.InputEnded:Connect(function(inp)
	if inp.KeyCode == Enum.KeyCode.Q then
		_G.aim = false
	end
end)
