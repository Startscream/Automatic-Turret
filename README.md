# Automatic-Turret
This turret will damage the closest humanoid to it, even if it's a dummy.

local aim = script.Parent

function findClosestTorso()
    local children = workspace:GetChildren()
    distance = 240
    target = nil    
    for i,v in pairs(children) do
        local h = v:FindFirstChild("Humanoid")
        local t = v:FindFirstChild("Troso") or v:FindFirstChild("UpperTroso")
        if h and t then
            if (aim.Position - t.Position).magnitude <= distance then
                if h.Health > 0 then
                    target = t
                    distance = (aim.Position - v.Position)
                end
            end
        end
    end
    return target
end

while wait(0.15) do
local target = findClosestTorso()
		if target then
				aim.CFrame = CFrame.new(aim.Position, t.Position)
				local bullet = Instance.new("Part")
					bullet.Parent = workspace
					bullet.Size = Vector3.new(0.2, 0.2, 1)
					bullet.Brickcolor = BrickColor.new("ReallyBlack")
					bullet.Velocity = 500
				bullet.Touched:Connect(function(part)
						local humanoid = part:FindFirstChild("Humanoid")
						if humanoid then
								humanoid:TakeDamage(25)
						end
				end)
		end
end
