-- perplex ui
-- made by Portal (give credit nigger)
-- do not publish or take credit

LPH_NO_VIRTUALIZE = function(...) return (...) end;
LPH_ENCSTR = function(...) return (...) end; 
LPH_CRASH = function(...) return (...) end; 

__newindex = function() 
	LPH_CRASH() 
end 

hookfunction = function() 
	LPH_CRASH() 
end

clonefunction = function()
	LPH_CRASH() 
end 

__metatable = function()
	LPH_CRASH() 
end 

getupvalue = function()
	LPH_CRASH()
end 

clonefunction = function()
	LPH_CRASH()
end 

local font = Enum.Font.Ubuntu;
local Library = loadstring(LPH_ENCSTR(game:HttpGet("https://gist.githubusercontent.com/f1nobe7650/c2945e224e5f2e6fbb4fb23e559cb1ed/raw/1581ae702f2963af2cc5da6a0495c74d4d2b0e30/gistfile1.txt")))();
Library:ChangeAccent(Color3.fromRGB(9, 121, 105));
local InputService = game:GetService("UserInputService");
local TeleportService = game:GetService("TeleportService");
local RunService = game:GetService("RunService");
local Workspace = game:GetService("Workspace");
local Lighting = game:GetService("Lighting");
local Players = game:GetService("Players");
local HttpService = game:GetService("HttpService");
local StarterGui = game:GetService("StarterGui");
local ReplicatedStorage = game:GetService("ReplicatedStorage");
local TweenService = game:GetService("TweenService");
local VirtualUser = game:GetService("VirtualUser");
local PathFindingService = game:GetService("PathfindingService");
local utility = {Circle = nil, bodyParts = {}, target = nil, angle = 0, drawings = {}, folders = {}}
local framework = {connections = {}}
local flags = Library.Flags
local ESP = {}
local IgnoreList = {} 
local misc_flags = {resolver = false, cframe = false, target = false, speed = false, fly = false}
local HitReg = {}
local Visuals = {   
    ["Drawings"] = {},
	["Bases"] = {},
	["Base"] = {},
	["Settings"] = { 
		["Line"] = {
		    Thickness = 1,
		    Color = Color3.fromRGB(0, 255, 0)
	    },
		["Text"] = {
			Size = 13,
			Center = true,
			Outline = true,
			Font = Drawing.Fonts.Plex,
			Color = Color3.fromRGB(255, 255, 255)
		},
		["Square"] = {
			Thickness = 1,
			Color = Color3.fromRGB(255, 255, 255),
			Filled = false,
		},
		["Triangle"] = {
			Color = Color3.fromRGB(255, 255, 255),
			Filled = true,
			Visible = false,
			Thickness = 1,
		},
		["Image"] = {
			Transparency = 1,
			Data = game:HttpGet("https://raw.githubusercontent.com/portallol/luna/main/Gradient.png")
		}
	},
}
local NovaPart = game:GetObjects("rbxassetid://14745759584")[1]; NovaPart.Parent = ReplicatedStorage;
local Nova = NovaPart.Attachment 
local sfx = {["Bameware"] = "3124331820",["Skeet"] = "4753603610",["Bonk"] = "3765689841",["Lazer Beam"] = "130791043",["Windows XP Error"] = "160715357",["TF2 Hitsound"] = "3455144981",["TF2 Critical"] = "296102734",["TF2 Bat"] = "3333907347",['Bow Hit'] = "1053296915",['Bow'] = "3442683707",['OSU'] = "7147454322",['Minecraft Hit'] = "4018616850",['Steve'] = "5869422451",['1nn'] = "7349055654",['Rust'] = "3744371091",["TF2 Pan"] = "3431749479",["Neverlose"] = "8679627751",["Mario"] = "5709456554",}
local sfx_names = {"Bameware", "Skeet", "Bonk", "Lazer Beam", "Windows XP Error", "TF2 Hitsound", "TF2 Critical", "TF2 Bat", "Bow Hit", "Bow", "OSU", "Minecraft Hit", "Steve", "1nn", "Rust", "TF2 Pan", "Neverlose", "Mario"}
local LocalPlayer = Players.LocalPlayer; 
local Mouse, Camera = LocalPlayer:GetMouse(), Workspace.Camera
local viewportSize = Camera.ViewportSize
local hitmodule = game:GetObjects("rbxassetid://7255773215")[1]; hitmodule.Parent = ReplicatedStorage
local Math = loadstring(game:HttpGet("https://raw.githubusercontent.com/f1nobe7650/Lynx/main/Math.lua"))(); 
local NewVector2, NewVector3 = Vector2.new, Vector3.new
local Floor = math.floor 
local Find = table.find
local Round = math.round
local Cos = math.cos
local Sin = math.sin
local Pi = math.pi 
local Sqrt = math.sqrt
local Lighting_Save = {["ColorShift_Bottom"] = Lighting.ColorShift_Bottom, ["Ambient"]=Lighting.Ambient, ["OutdoorAmbient"]=Lighting.OutdoorAmbient, ["ColorShift_Top"]=Lighting.ColorShift_Top, ["FogColor"]=Lighting.FogColor, ["FogEnd"]=Lighting.FogEnd, ["FogStart"]=Lighting.FogStart, ["ClockTime"]=Lighting.ClockTime, ["Brightness"]=Lighting.Brightness}
local IgnoreList = {}
local Tween = {};
local crosshair_Lines = {}; 
local crosshair_Outlines = {}; 
local crosshair_LineAmount = 4;
local crosshair_SpinAngle = 0; 
local Offset = game:GetService("GuiService"):GetGuiInset().Y
local connections = {} 
local highlights = {} 
-- 
do 
    -- utility functions
    do 
        function utility:ValidateClient(Player)
            return Player and Player.Character and Player.Character:FindFirstChild("Humanoid") and true or false 
        end 
		--
		function utility:CreateBeam(Origin, End, Color1)
			local BeamPart = Instance.new("Part", Workspace)
			BeamPart.Name = "BeamPart"
			BeamPart.Transparency = 1
			--
			local Part = Instance.new("Part", BeamPart)
			Part.Size = NewVector3(1, 1, 1)
			Part.Transparency = 1
			Part.CanCollide = false
			Part.CFrame = typeof(Origin) == "CFrame" and Origin or CFrame.new(Origin)
			Part.Anchored = true
			local Attachment = Instance.new("Attachment", Part)
			local Part2 = Instance.new("Part", BeamPart)
			Part2.Size = NewVector3(1, 1, 1)
			Part2.Transparency = 1
			Part2.CanCollide = false
			Part2.CFrame = typeof(End) == "CFrame" and End or CFrame.new(End)
			Part2.Anchored = true
			Part2.Color = Color3.fromRGB(255, 255, 255)
			local Attachment2 = Instance.new("Attachment", Part2)
			local Beam = Instance.new("Beam", Part)
			Beam.FaceCamera = true
			Beam.Color = ColorSequence.new{
				ColorSequenceKeypoint.new(0.00, Color1),
				ColorSequenceKeypoint.new(1, Color1),
			}
			Beam.Attachment0 = Attachment
			Beam.Attachment1 = Attachment2
			Beam.LightEmission = 6
			Beam.LightInfluence = 1
			Beam.Width0 = 1
			Beam.Width1 = 0.6
			Beam.Texture = "rbxassetid://7151778302"
			Beam.LightEmission = 1
			Beam.LightInfluence = 1
			Beam.TextureMode = Enum.TextureMode.Wrap 
			Beam.TextureLength = 3 
			Beam.TextureSpeed = 3
			delay(flags["Tracers Life Time"], function()
				Part:Destroy()
				Part2:Destroy()
				BeamPart:Destroy()
			end)
		end  
		-- 
		function utility:generateAngles(numLines)
			local angles = {}
			local angleIncrement = 2 * math.pi / numLines
			
			for i = 1, numLines do
				local angle = (i - 1) * angleIncrement
				table.insert(angles, angle)
			end
			
			return angles
		end
		-- 
		function utility:Shift(Number)
			return math.acos(math.cos(Number * math.pi)) / math.pi
		end
        -- 
        function utility:calculateAimViewerEndPoint()
            if utility.target and utility.target.Character and flags["Aim Viewer Bypass"] then 
                local part = (flags["Jump Prediction"] and utility.target.Character.Humanoid.FloorMaterial == Enum.Material.Air and "RightFoot") or (flags["Nearest Part"] and partClosest) or flags["Single Hit Part"]
                local yOffset = utility.target.Character.Humanoid.FloorMaterial == Enum.Material.Air and flags["Manual Offset Value"] or 0 
                print(part, yOffset, checks) -- ENDED HERE
                --
                if (checks == true) then 
                    if flags["Resolver"] then  
                        local endpoint = utility.target.Character[tostring(part)].Position + offset + NewVector3(0, yOffset, 0)
                        Remote:FireServer("UpdateMousePos", endpoint) 
                    else 
                        local endpoint = utility.target.Character[tostring(part)].Position + (utility.target.Character.HumanoidRootPart.Velocity * prediction) + NewVector3(0, yOffset, 0)
                        Remote:FireServer("UpdateMousePos", endpoint) 
                    end   
                end   
            end 
        end     
        -- 
        function utility:getHeld() 
            if LocalPlayer.Character and LocalPlayer.Character:FindFirstChildWhichIsA("Tool") and LocalPlayer.Character then 
				return LocalPlayer.Character:FindFirstChildWhichIsA("Tool") or nil; 
			end
        end 
        --
        function utility:GetComponents(Player)
            if utility:ValidateClient(Player) then 
                return Player.Character, Player.Character:FindFirstChild("HumanoidRootPart"), Player.Character:FindFirstChild("Humanoid")
            end 
        end 
        --
        function utility:getClosestPlayerToCursor(Radius)
            local shortestDistance = Radius or math.huge

            local closestPlayer
            for i, v in pairs(Players:GetPlayers()) do
                if v ~= LocalPlayer and utility:ValidateClient(v) then
                    local pos, OnScreen = Camera:WorldToViewportPoint(v.Character.HumanoidRootPart.Position)
                    local magnitude = (Vector2.new(pos.X, pos.Y) - Vector2.new(Mouse.X, Mouse.Y)).magnitude
                        if magnitude < shortestDistance and OnScreen then
                            closestPlayer = v
                            shortestDistance = magnitude
                        end
                    end
                end 
            return closestPlayer
        end
        --
        function utility:RecalculateVelocity(Player)
            if utility:ValidateClient(Player) then
                local Character, RootPart, Humanoid = utility:GetComponents(Player)

                local currentPosition = RootPart.Position
                local currentTime = tick() 
                
                task.wait()
    
                local newPosition = RootPart.Position
                local newTime = tick()
                
                local distanceTraveled = (newPosition - currentPosition) 
    
                local timeInterval = newTime - currentTime
                local velocity = distanceTraveled / timeInterval
                currentPosition = newPosition
                currentTime = newTime
                return velocity
            end
        end
        -- 
        function utility:Highlight(Player, fillColor, fillTransparency, outlineColor, outlineTransparency) 
            highlights[Player] = Instance.new("Highlight")
            highlights[Player].Enabled = true
            highlights[Player].DepthMode = Enum.HighlightDepthMode.AlwaysOnTop
            highlights[Player].FillColor = fillColor or Color3.fromRGB(255,0,255)
            highlights[Player].OutlineColor = outlineColor or Color3.fromRGB(255,0,255)
            highlights[Player].Adornee = Player.Character
            highlights[Player].OutlineTransparency = outlineTransparency or 0.5
            highlights[Player].FillTransparency = fillTransparency or 0
            highlights[Player].Parent = game.CoreGui
             
            connections[Player] = Player.CharacterAdded:Connect(function()
                highlights[Player].Adornee = Player.Character
            end)

            return highlights[Player] 
        end 
        --
        function utility:drawObject(type, prop)
            local obj = Drawing.new(type)
            --
            if prop then
                for i,v in next, prop do
                    obj[i] = v;
                end
            end
            return obj  
        end
        --
        utility.folders["Part Chams"] = Instance.new("Folder", Workspace) 
        -- 
        function utility:characterClone(Player, Color, Material, Transparency, Parent)
            for i,v in pairs(Player.Character:GetChildren()) do 
				if table.find(utility.bodyParts, v.Name) and v:IsA("MeshPart") and v.Name ~= "HumanoidRootPart" then 
					if v.Name == "UpperTorso" or v.Name == "LowerTorso" then 
						local ClonedPart = Instance.new("Part")
						ClonedPart.Anchored = true 
						ClonedPart.CanCollide = false 
						ClonedPart.Position = v.Position
						ClonedPart.Parent = Parent
						ClonedPart.Material = Enum.Material[Material]
						ClonedPart.Transparency = Transparency 
						ClonedPart.Color = Color
						ClonedPart.Size = v.Size + Vector3.new(0.01,0.01,0.01)
						ClonedPart.Name = v.Name
						ClonedPart.Rotation = v.Rotation
						ClonedPart.Shape = "Block"
					else 
						local ClonedPart = Instance.new("MeshPart")
						ClonedPart.Anchored = true 
						ClonedPart.CanCollide = false 
						ClonedPart.Position = v.Position
						ClonedPart.Parent = Parent
						ClonedPart.Material = Enum.Material[Material]
						ClonedPart.Transparency = Transparency 
						ClonedPart.Color = Color
						ClonedPart.Size = v.Size + Vector3.new(0.01,0.01,0.01)
						ClonedPart.Name = v.Name
						ClonedPart.Rotation = v.Rotation
						ClonedPart.MeshId = v.MeshId
					end 
				end 
            end
        end 
        -- 
        function utility:Remove(Player)
            if connections[Player] then 
                connections[Player]:Disconnect();
            end 
            -- 
            if highlights[Player] then 
                highlights[Player].Parent = nil;
            end 
        end 
        --
        function utility:AngleToEdge(angle, inset) -- credits to whoever made this Im just porting over my old arrows 😭
            local pos
            local ox = Cos(angle)
            local oy = Sin(angle)
            local slope = oy / ox
            -- 
            local h_edge = viewportSize.x - inset
            local v_edge = viewportSize.y - inset
            if oy < 0 then
                v_edge = inset
            end
            if ox < 0 then
                h_edge = inset
            end
            local y = (slope * h_edge) + (viewportSize.y / 2) - slope * (viewportSize.x / 2)
            if y > 0 and y < viewportSize.y - inset then
                pos = Vector2.new(h_edge, y)
            else
                pos = Vector2.new(
                    (v_edge - viewportSize.y / 2 + slope * (viewportSize.x / 2)) / slope,
                    v_edge
                )
            end
            return pos
        end
        --
        function utility:Map(N, OldMin, OldMax, Min, Max) -- I love my 1 line funcs I use once ♥😻
            return (N - OldMin) / (OldMax - OldMin) * (Max - Min) + Min
        end
        --
        function utility:getRotate(Vec, Rads) -- I didnt make this math credits to whoever can code cool maths!
            local vec = Vec.Unit
            local sin = math.sin(Rads)
            local cos = math.cos(Rads)
            local x = (cos * vec.x) - (sin * vec.y)
            local y = (sin * vec.x) + (cos * vec.y)
            --
            return Vector2.new(x, y).Unit * Vec.Magnitude
        end
        --
        function utility:BoxCalculation(torso)
            local VTop = torso.Position + (torso.CFrame.UpVector * 1.8) + Camera.CFrame.UpVector;
            local VBottom = torso.Position - (torso.CFrame.UpVector * 2.5) - Camera.CFrame.UpVector;
        
            local Top, TopIsRendered = Camera:WorldToViewportPoint(VTop);
            local Bottom, BottomIsRendered = Camera:WorldToViewportPoint(VBottom);
        
            local Width = math.max(math.floor(math.abs(Top.x - Bottom.x)), 3);
            local Height = math.max(math.floor(math.max(math.abs(Bottom.y - Top.y), Width / 2)), 3);
            local BoxSize = NewVector2(math.floor(math.max(Height / 1.5, Width)), Height);
            local BoxPosition = NewVector2(math.floor(Top.x * 0.5 + Bottom.x * 0.5 - BoxSize.x * 0.5), math.floor(math.min(Top.y, Bottom.y)));
        
            return BoxSize, BoxPosition;
        end
        --
        local LastRayIgnoreUpdate, RayIgnoreList = 0, {}
		-- 
		function utility:checkRay(Instance, Distance, Position, Unit)
			local Pass = true;
			local Model = Instance;

			if Distance > 999 then return false; end

			if Instance.ClassName == 'Player' then
				Model = GetCharacter(Instance);
			end

			if not Model then
				Model = Instance.Parent;

				if Model.Parent == workspace then
					Model = Instance;
				end
			end

			if not Model then return false end

			local _Ray = Ray.new(Position, Unit * Distance)

			if tick() - LastRayIgnoreUpdate > 3 then
				LastRayIgnoreUpdate = tick()

				table.clear(RayIgnoreList)

				table.insert(RayIgnoreList, LocalPlayer.Character)
				table.insert(RayIgnoreList, Camera)
				
				if Mouse.TargetFilter then table.insert(RayIgnoreList, Mouse.TargetFilter) end

				if #IgnoreList > 64 then
					while #IgnoreList > 64 do
						table.remove(IgnoreList, 1)
					end
				end

				for i, v in pairs(IgnoreList) do table.insert(RayIgnoreList, v) end
			end

			local Hit = workspace:FindPartOnRayWithIgnoreList(_Ray, RayIgnoreList)

			if Hit and not Hit:IsDescendantOf(Model) then
				Pass = false;
				if Hit.Transparency >= .3 or not Hit.CanCollide and Hit.ClassName ~= Terrain then
					table.insert(IgnoreList, Hit)
				end
			end

			return Pass;
		end
        --
        function utility:GetOrigin()
            local Tool = utility:getHeld()
            -- 
            return (Tool ~= "None" and Tool.Handle.Position) or Camera.CFrame.Position
        end
        --
        function utility:Lerp(Value, MinColor, MaxColor)
            if Value <= 0 then return MaxColor end
            if Value >= 100 then return MinColor end
            --
            return Color3.new(
                MaxColor.R + (MinColor.R - MaxColor.R) * Value,
                MaxColor.G + (MinColor.G - MaxColor.G) * Value,
                MaxColor.B + (MinColor.B - MaxColor.B) * Value
            )
        end
    end 
	
    -- framework functions 
    do 
        function framework:selectTarget() 
			local deathLoop; 
			local deathLoopRestore; 
			-- 	
            if flags["Silent Enabled"] then 
                if misc_flags["target"] then 
                    utility.target = utility:getClosestPlayerToCursor(math.huge); 
                    -- 
                    if flags["Highlight Enabled"] then 
                        utility:Highlight(utility.target, flags["Highlight Fill Color"],  flags["Highlight Fill Color"].transparency, flags["Highlight Outline Color"], flags["Highlight Outline Color"].transparency);
                    end 
                    -- 
                    if flags["Notify"] then 
                        Notification:Notify({Title = "tonka", Description = "Locked onto: " .. utility.target.Name .. ""}, {OutlineColor = Library.Theme.Accent, Time = 2, Type = "default"});
                    end 
                    -- 
                    if flags["Back Track Enabled"] and flags["Back Track Method"] == "Follow" then 
                        utility:characterClone(utility.target, flags["Back Track Settings"], flags["Back Track Material"], flags["Back Track Settings"].transparency, utility.folders["Part Chams"])
                    end 
                    --
                    if flags["Spectate"] or not framework:checkForKillBot() then 
                        Camera.CameraSubject = utility.target.Character.Humanoid
                    end 

					--[[if not framework:checkForKillBot() and table.find(flags["Kill Bot Settings"], "Stomp on knock") then 
						deathLoop = utility.target.Character:WaitForChild("Humanoid").HealthChanged:Connect(function(newHealth)
							if not framework:checkForKillBot() then 
								LocalPlayer.Character.HumanoidRootPart.CFrame = utility.target.Character.UpperTorso.CFrame
							end 
						end) 
						-- 
						deathLoopRestore = utility.target.CharacterAdded:Connect(function(char)
							deathLoop = utility.target.Character:WaitForChild("Humanoid").HealthChanged:Connect(function(newHealth)
								if not framework:checkForKillBot() and Player.Character.BodyEffects["K.O"].Value then 
									LocalPlayer.Character.HumanoidRootPart.CFrame = utility.target.Character.UpperTorso.CFrame
								end 
							end)
						end) 
					end ]]
                else 
                    --NYAHHHHH :3
                    LocalPlayer.Character.Humanoid.AutoRotate = true;
                    Camera.CameraSubject = LocalPlayer.Character.Humanoid;
                    utility.folders["Part Chams"]:ClearAllChildren();
                    if utility.target then 
                        utility:Remove(utility.target);
                    end 
                    utility.drawings["Tracer"].Visible = false;
                    utility.target = nil;
                end 
            end 
        end  
		--
		function framework:detectHit()
			pcall(function()
				framework["connections"]["On-Hit-Raycast"] = Workspace.Ignored.Siren.Radius.DescendantAdded:Once(function(Beam)
					delay(0.05, function()
						if Beam.Name == "BULLET_RAYS" then 
							local Ray = Ray.new(Beam.Position, Beam.CFrame.LookVector * 200)
							local IgnoreList = {LocalPlayer.Character}
							local Hit, HitPosition = Workspace:FindPartOnRayWithIgnoreList(Ray, IgnoreList);
							-- 
							if Hit then
								local InstanceHit = Hit:FindFirstAncestorOfClass('Model')
								if not InstanceHit then return end 
								
								if InstanceHit:FindFirstChild("Humanoid") and InstanceHit:FindFirstChild("HumanoidRootPart") then 
									if flags["Hit Sounds"] then 
										HitReg:HitSound(sfx[flags["Hit Sounds Sound"]], flags["Hit Sounds Volume"], flags["Hit Sounds Pitch"])
									end 
									-- 
									if flags["Hit Chams"] then 
										local Folder = Instance.new("Folder", Workspace) 
										utility:characterClone(Players[InstanceHit.Name], flags["Hit Chams Settings"], flags["Hit Chams Material"], flags["Hit Chams Settings"].transparency, Folder);
										delay(flags["Hit Chams Fading Time"], function()
											Folder:Destroy()
										end)
									end
									-- 
									if flags["Hit Marker"] then 
										HitReg:HitMarker(4, flags["Hit Marker Settings"], flags["Hit Markers Time"])
									end 
									-- 
									if flags["3D Hit Marker"] then 
										HitReg:HitMarker3D(4, flags["3D Hit Markers Settings"], flags["Hit Markers Time"], HitPosition) 
									end 
									-- 
									if flags["Hit Effects"] then 
										HitReg:HitEffect(flags["Hit Effects Option"], Players[InstanceHit.Name].Character)
									end 
								end 
							end 	
						end 
					end) 
				end)
			end)	
		end 
		-- 
		function framework:worldVisuals() 
			if flags["Master Switch"] then 
				if flags["Clock Time Enabled"] and Lighting.ClockTime ~= flags["Clock Time"] then 
					Lighting.ClockTime = flags["Clock Time"]
				end 
				-- 
				if flags["Color Shift Bottom"] and Lighting.ColorShift_Bottom ~= flags["Color Shift Bottom Color"] then 
					Lighting.ColorShift_Bottom = flags["Color Shift Bottom Color"]
				end 

				if flags["Ambient"] and Lighting.Ambient ~= flags["Ambience Color"] then 
					Lighting.Ambient = flags["Ambience Color"]
				end 
				-- 
				if flags["Outdoor Ambience"] and Lighting.OutdoorAmbient ~= flags["Outdoor Ambience color"] then 
					Lighting.OutdoorAmbient = flags["Outdoor Ambience color"]
				end 
				-- 
				if flags["Brightness Enabled"] and Lighting.Brightness ~= flags["Brightness"] then 
					Lighting.Brightness = flags["Brightness"]
				end 
				-- 
				if flags["Color Shift Top"] and Lighting.ColorShift_Top ~= flags["Color Shift Top Color"]  then 
					Lighting.ColorShift_Top = flags["Color Shift Top Color"]
				end 
				-- 
				if flags["Fog"] and Lighting.FogColor ~= flags["Fog Color"] then 
					Lighting.FogColor = flags["Fog Color"]
				end 
			end 
		end 
		--
		function framework:cframeSpeed()
			if flags["Speed Enabled"] and misc_flags["speed"] then 
				local Character = LocalPlayer.Character 
				local Move_Direction = Character.Humanoid.MoveDirection
				-- 
				Character.HumanoidRootPart.CFrame = Character.HumanoidRootPart.CFrame + (Move_Direction * (flags["Speed"] / 25))
			end 
		end 
		-- 
		function framework:fly() 
			if flags["Fly Enabled"] and misc_flags["fly"] then 
				local FlyPosition = Vector3.new(0, 0, 0)
				local CCV = Camera.CFrame.lookVector
				-- 
				if InputService:IsKeyDown(Enum.KeyCode.W) then
					FlyPosition = FlyPosition + CCV
				end
				-- 
				if InputService:IsKeyDown(Enum.KeyCode.S) then
					FlyPosition = FlyPosition - CCV
				end
				-- 
				if InputService:IsKeyDown(Enum.KeyCode.D) then
					FlyPosition = FlyPosition + Vector3.new(-CCV.Z, 0, CCV.X)
				end
				-- 
				if InputService:IsKeyDown(Enum.KeyCode.A) then
					FlyPosition = FlyPosition + Vector3.new(CCV.Z, 0, -CCV.x)
				end
				-- 
				if InputService:IsKeyDown(Enum.KeyCode.Space) then
					FlyPosition = FlyPosition + Vector3.new(0, 1, 0)
				end
				-- 
				if InputService:IsKeyDown(Enum.KeyCode.LeftShift) then
					FlyPosition = FlyPosition - Vector3.new(0, 1, 0)
				end
				-- 
				if FlyPosition.Unit.y == FlyPosition.Unit.y then
					LocalPlayer.Character.HumanoidRootPart.Anchored = false 
					LocalPlayer.Character.HumanoidRootPart.Velocity = FlyPosition.Unit * flags["Fly Speed"]
				else 
					LocalPlayer.Character.HumanoidRootPart.Velocity = Vector3.new(0, 0, 0)
					LocalPlayer.Character.HumanoidRootPart.Anchored = true
				end 
			end 
		end 
		--
		function framework:translateBeam(Beam)
			local Part = Beam
			if Part ~= nil then 
				local Attachments = Part:GetChildren()
				if Attachments ~= nil and Attachments[1] ~= nil and Attachments[2] ~= nil then
					local Origin = Attachments[1].WorldCFrame
					local End = Attachments[2].WorldCFrame
					-- 
					utility:CreateBeam(Origin, End, flags["Bullet Tracers Color"])
					Part.Parent = nil 
				end 
			end 
		end
        --
        function framework:selectPrediction()
            local Prediction; 
            
            local Predictions = {
                0.113,
                0.115,
                0.117,
                0.11923283912031938191231281632312637123821763333312731833,
                0.121316378910319876472890149871624,
                0.124521314351673817351423414,
                0.131314253678192031927365421456789331,
                0.1355991245213413214231231123121,
                0.138312341526738912,
                0.146432786576847627781237813281381382038198391293,
                0.1512783311111111111111111111111111111111111,
                0.15132132132132132555555555555555,
            }

            if flags["Auto Prediction"] then 
                for i = 1, #Predictions do 
                    if game:GetService("Stats").Network.ServerStatsItem["Data Ping"]:GetValue() <= i * 10 then 
                        Prediction = Predictions[i]
                    end 
                end                 
            end 

            return Prediction or tonumber(flags["Manual Prediction Value"]) or 0.1413
        end 
        --
        function framework:calculateResolverOffset() 
            local Offset; 
            local Prediction = framework:selectPrediction() 
            -- 
            if flags["Resolver"] then 
                if flags["Resolver Method"] == "Recalculate Velocity" then 
                    Offset = utility:RecalculateVelocity(utility.target) * Prediction
                elseif flags["Resolver Method"] == "Suppress Velocity" then 
                    Offset = Vector3.new(utility.target.Character.HumanoidRootPart.Velocity.X, 0, utility.target.Character.HumanoidRootPart.Velocity.Z) * Prediction
                elseif flags["Resolver Method"] == "Move Direction" then 
                    Offset = utility.target.Character.Humanoid.MoveDirection * 19.64285714289 * Prediction
                end 
            end 
            --  
            return Offset 
        end 
        -- 
        function framework:calculateNearestPart(Player, List)
            local shortestDistance = math.huge
            local closestPart
            if Player.Character and Player.Character:FindFirstChild("Humanoid") and Player.Character:FindFirstChild("Head") and Player.Character.Humanoid.Health ~= 0 and Player.Character:FindFirstChild("HumanoidRootPart") then
                for i, v in pairs(Player.Character:GetChildren()) do
                    if v:IsA("BasePart") then 
                        local pos = Camera:WorldToViewportPoint(v.Position)
                        local magnitude = (Vector2.new(pos.X, pos.Y) - Vector2.new(Mouse.X, Mouse.Y+36)).magnitude
                            if magnitude < shortestDistance and table.find(List, v.Name) then
                                closestPart = v
                                shortestDistance = magnitude
                            end
                        end
                    end 
                return closestPart
            end
        end 
        -- 
        function framework:getChecks(Player, Friend, Wall, Knocked, Grabbed)
            local Checks = true 
            --  
            if Friend and LocalPlayer:IsFriendsWith(Player.UserId) then Checks = false end 
            if Wall then Checks = utility:checkRay(Player.Character.Head, (Camera.CFrame.Position - Player.Character.Head.Position).Magnitude, Camera.CFrame.Position, (Player.Character.Head.Position - Camera.CFrame.Position).unit) end 
            if Knocked and Player.Character.BodyEffects["K.O"].Value == true then Checks = false end 
            if Grabbed and Player.Character:FindFirstChild("GRABBING_CONSTRAINT") then Checks = false end 
            --
            return Checks
        end 
		-- 
		function framework:checkForKillBot()
			if misc_flags["target"] then  
				local Killbot = flags["Kill Bot"]; 
				-- 
				return (table.find(flags["Kill Bot Settings"], "Disable on knock") and utility.target.Character.BodyEffects and utility.target.Character.BodyEffects["K.O"].Value) or not Killbot 
			end 
		end 
    end 

    -- drawings 
    do 
        utility.drawings["Tracer"] = utility:drawObject("Line", {})
		
		-- drawing lines for crosshair
		do 
			for Index = 1, 4 do
				local line = utility:drawObject("Line",{
					Visible = false,
					Color = Color3.fromRGB(255,255,255),
					Thickness = 1,
					ZIndex = 2,
					Transparency = 1
				})
				--
				crosshair_Lines[Index] = line
				-- 
				local line_1 = utility:drawObject("Line",{
					Visible = false,
					Color = Color3.fromRGB(0, 0, 0),
					Thickness = 2.5,
					ZIndex = 1,
					Transparency = 1
				})
				--
				crosshair_Outlines[Index] = line_1
			end
		end 

        -- functions for drawing the mf esp :money_face: 
        function ESP:PlayerDraw(Type, Outline, Name, Filled)
            local drawing = Drawing.new(Type)
            for i, v in pairs(Visuals["Settings"][Type]) do
                drawing[i] = v
            end
            --
            if Outline then
                drawing.Color = Color3.new(0,0,0)
                drawing.Thickness = 3
            end
            --
            if Filled then 
                drawing.Filled = true 
            end 
            --
            return drawing
        end
        -- 
        function ESP:Add(Player)
            if not Visuals["Drawings"][Player] then
                Visuals["Drawings"][Player] = {
                    Name = ESP:PlayerDraw("Text", nil, "Name", false),
                    Tool = ESP:PlayerDraw("Text", nil, "Tool", false),
                    BoxOutline = ESP:PlayerDraw("Square", true, "BoxOutline", false),
                    Box = ESP:PlayerDraw("Square", nil, "Box",false),
                    HealthOutline = ESP:PlayerDraw("Square", false, "HealthOutline", false),
                    Health = ESP:PlayerDraw("Square", nil, "Health", false),
                    HealthText = ESP:PlayerDraw("Text",nil, "HealthText", false),
                    HealthBarGradient = ESP:PlayerDraw("Image", nil, "HealthBarGradient", false), 
                    BoxFill = ESP:PlayerDraw("Square", nil, "BoxFill", true),
                    ArmorBar = ESP:PlayerDraw("Square", nil, "ArmorBar", false),
                    ArmorBarOutline = ESP:PlayerDraw("Square", nil, "ArmorBarOutline", false),
                    ArrowOutline = ESP:PlayerDraw("Triangle", false, "ArrowOutline", false),
                    Arrow = ESP:PlayerDraw("Triangle", nil, "Arrow", false),
                    Flag = ESP:PlayerDraw("Text",nil, "Flag", false)
                }
                -- 
                Visuals["Drawings"][Player]["Corners"] = {}
                -- 
                for Index = 9, 16 do
                    Visuals["Drawings"][Player]["Corners"][Index] = ESP:PlayerDraw("Line", nil, "Corners", false)
                    Visuals["Drawings"][Player]["Corners"][Index].Thickness = 3
                end
                --
                for Index = 1, 8 do
                    Visuals["Drawings"][Player]["Corners"][Index] = ESP:PlayerDraw("Line", nil, "Corners", false)
                    Visuals["Drawings"][Player]["Corners"][Index].Thickness = 0 
                end
            end
        end
		--
		for _, Player in pairs(Players:GetPlayers()) do
			if Player ~= LocalPlayer then
				ESP:Add(Player)
			end
		end
    end 

	-- hitreg 
	do 
		function HitReg:HitMarker(Gap, Color, Time) 
			local Lines = {} 
			-- 
			for i = 1, 4 do 
				Lines[i] = utility:drawObject("Line", {Color = Color, Visible = true, Transparency = 1, Thickness = 1})
			end 
			-- 
			Lines[1].From = Vector2.new(Mouse.X + Gap, (Mouse.Y + 36) + Gap)
			Lines[1].To = Vector2.new(Mouse.X + (Gap * 2.5), (Mouse.Y + 36) + (Gap * 2.5))
			--
			Lines[2].From = Vector2.new(Mouse.X + Gap, (Mouse.Y + 36) - Gap)
			Lines[2].To = Vector2.new(Mouse.X + (Gap * 2.5), (Mouse.Y + 36) - (Gap * 2.5))
			--
			Lines[3].From = Vector2.new(Mouse.X - Gap, (Mouse.Y + 36) + Gap)
			Lines[3].To = Vector2.new(Mouse.X - (Gap * 2.5), (Mouse.Y + 36) + (Gap * 2.5))
			--
			Lines[4].From = Vector2.new(Mouse.X - Gap, (Mouse.Y + 36) - Gap)
			Lines[4].To = Vector2.new(Mouse.X - (Gap * 2.5), (Mouse.Y + 36) - (Gap * 2.5))
			-- 
			delay(Time, function()
				for i = Time, 0, -0.1 do
					task.wait()
					for _, Value in next, Lines do
						Value.Transparency = i
					end
				end
				-- 
				for _, Value in next, Lines do
					Value:Remove()
				end
			end)
		end 
		-- 
		function HitReg:HitMarker3D(Gap, Color, Time, Hit) 
			local Lines = {} 
			-- 
			for i = 1, 4 do 
				Lines[i] = utility:drawObject("Line", {Color = Color, Visible = true, Transparency = 1, Thickness = 1})
			end     
			-- 
			local Loop = RunService.RenderStepped:Connect(function()
				local Position3D, OnScreen = Camera:WorldToViewportPoint(Hit)
				-- 
				Lines[1].From = Vector2.new(Position3D.X + Gap, Position3D.Y + Gap)
				Lines[1].To = Vector2.new(Position3D.X + (Gap * 2.5), Position3D.Y + (Gap * 2.5))
				--
				Lines[2].From = Vector2.new(Position3D.X + Gap, Position3D.Y - Gap)
				Lines[2].To = Vector2.new(Position3D.X + (Gap * 2.5), Position3D.Y - (Gap * 2.5))
				--
				Lines[3].From = Vector2.new(Position3D.X - Gap, Position3D.Y + Gap)
				Lines[3].To = Vector2.new(Position3D.X - (Gap * 2.5), Position3D.Y + (Gap * 2.5))
				--
				Lines[4].From = Vector2.new(Position3D.X - Gap, Position3D.Y - Gap)
				Lines[4].To = Vector2.new(Position3D.X - (Gap * 2.5), Position3D.Y - (Gap * 2.5))
				-- 
				for _, Value in next, Lines do
					Value.Visible = OnScreen
				end
			end)
			-- 
			delay(Time, function()
				for i = Time, 0, -0.1 do
					task.wait()
					for _, Value in next, Lines do
						Value.Transparency = i
					end
				end
				-- 
				for _, Value in next, Lines do
					Value:Remove()
				end
				Loop:Disconnect()
			end)
		end 
		--
		function HitReg:HitEffect(Type, Character)
			local function convert(color)
				return color.r/5, color.g/5, color.b/5
			end 
			-- 
			local function Weld(x,y)
				local W = Instance.new("Weld")
				W.Part0 = x
				W.Part1 = y
				local CJ = CFrame.new(x.Position)
				local C0 = x.CFrame:inverse()*CJ
				local C1 = y.CFrame:inverse()*CJ
				W.C0 = C0
				W.C1 = C1
				W.Parent = x
			end
			-- 
			if Type == "Confetti" then 
				task.spawn(function()
					local Confetti_Amount = 20000
					local RootPart = Character.HumanoidRootPart
					local ConfettiClone = hitmodule:Clone()
					ConfettiClone.RainbowParticles.Rate = Confetti_Amount
					ConfettiClone.Parent = workspace
					ConfettiClone.CanCollide = false
					ConfettiClone.CFrame = RootPart.CFrame
					-- 
					for i = Confetti_Amount, 0 , -(Confetti_Amount/50) do 
						task.wait()
						ConfettiClone.RainbowParticles.Rate = i
					end 
					-- 
					delay(5, function()
						ConfettiClone:Destroy()
					end)
				end)
			else 
				local Effect = Nova:Clone() 
				Effect.Parent = Character.HumanoidRootPart
				--	
				for i,v in pairs(Effect:GetChildren()) do 
					v.Rate = 0
					v.Color = ColorSequence.new({ColorSequenceKeypoint.new(0, Color3.new(0, 0, 0)), ColorSequenceKeypoint.new(0.5, Color3.new(convert(flags["Hit Effect Settings"]))),ColorSequenceKeypoint.new(1, Color3.new(0, 0, 0)),})
					v:Emit()
				end 
				-- 	
				delay(2, function()
					Effect:Destroy()
				end)
			end 
		end 
		-- 
		function HitReg:HitSound(Id, Volume, Pitch)
			local Sound = Instance.new("Sound", Workspace); local PitchSound = Instance.new("PitchShiftSoundEffect", Sound)
			-- 
			Sound.SoundId = "rbxassetid://".. Id ..""
			Sound.Volume = Volume
			PitchSound.Octave = Pitch
			Sound:Play()
			Sound.Ended:Connect(function()
				Sound:Destroy()
				PitchSound:Destroy()
			end)	
		end 
	end 

    for i,v in pairs(LocalPlayer.Character:GetChildren()) do 
        if v:IsA("BasePart") then 
            table.insert(utility.bodyParts, v.Name)
        end 
    end 

	-- tweens 
	do
		Tween.EasingStyles = {
			[Enum.EasingStyle.Linear] = {
				[Enum.EasingDirection.In] = function(Delta)
					return Delta
				end,
				[Enum.EasingDirection.Out] = function(Delta)
					return Delta
				end,
				[Enum.EasingDirection.InOut] = function(Delta)
					return Delta
				end
			},
			[Enum.EasingStyle.Cubic] = {
				[Enum.EasingDirection.In] = function(Delta)
					return Delta ^ 3
				end,
				[Enum.EasingDirection.Out] = function(Delta)
					return ((Delta - 1) ^ 3) + 1
				end,
				[Enum.EasingDirection.InOut] = function(Delta)
					if 0 <= Delta and Delta <= 0.5 then
						return (4 * Delta ^ 3)
					elseif 0.5 <= Delta and Delta <= 1 then
						return (4 * (Delta - 1) ^ 3) + 1
					end
				end
			},
			[Enum.EasingStyle.Quad] = {
				[Enum.EasingDirection.In] = function(Delta)
					return Delta ^ 2
				end,
				[Enum.EasingDirection.Out] = function(Delta)
					return (-(Delta - 1) ^ 2) + 1
				end,
				[Enum.EasingDirection.InOut] = function(Delta)
					if 0 <= Delta and Delta <= 0.5 then
						return (2 * Delta ^ 2)
					elseif 0.5 <= Delta and Delta <= 1 then
						return -(2 * (Delta - 1) ^ 2) + 1
					end
				end
			},
			[Enum.EasingStyle.Quart] = {
				[Enum.EasingDirection.In] = function(Delta)
					return Delta ^ 4
				end,
				[Enum.EasingDirection.Out] = function(Delta)
					return (-(Delta - 1) ^ 4) + 1
				end,
				[Enum.EasingDirection.InOut] = function(Delta)
					if 0 <= Delta and Delta <= 0.5 then
						return (8 * Delta ^ 4)
					elseif 0.5 <= Delta and Delta <= 1 then
						return -(8 * (Delta - 1) ^ 4) + 1
					end
				end
			},
			[Enum.EasingStyle.Quint] = {
				[Enum.EasingDirection.In] = function(Delta)
					return Delta ^ 5
				end,
				[Enum.EasingDirection.Out] = function(Delta)
					return ((Delta - 1) ^ 5) + 1
				end,
				[Enum.EasingDirection.InOut] = function(Delta)
					if 0 <= Delta and Delta <= 0.5 then
						return (16 * Delta ^ 5)
					elseif 0.5 <= Delta and Delta <= 1 then
						return (16 * (Delta - 1) ^ 5) + 1
					end
				end
			},
			[Enum.EasingStyle.Sine] = {
				[Enum.EasingDirection.In] = function(Delta)
					return Sin(((Pi / 2) * Delta) - (Pi / 2)) + 1
				end,
				[Enum.EasingDirection.Out] = function(Delta)
					return Sin((Pi / 2) * Delta)
				end,
				[Enum.EasingDirection.InOut] = function(Delta)
					return (0.5 * Sin((Pi * Delta) - (Pi / 2))) + 0.5
				end
			},
			[Enum.EasingStyle.Exponential] = {
				[Enum.EasingDirection.In] = function(Delta)
					return (2 ^ ((10 * Delta) - 10)) - 0.001
				end,
				[Enum.EasingDirection.Out] = function(Delta)
					return 1.001 * (-2 ^ -(10 * Delta)) + 1
				end,
				[Enum.EasingDirection.InOut] = function(Delta)
					if 0 <= Delta and Delta <= 0.5 then
						return 0.5 * (2 ^ ((20 * Delta) - 10)) - 0.0005
					elseif 0.5 <= Delta and Delta <= 1 then
						return 0.50025 * (-2 ^ (-(20 * Delta) + 10)) + 1
					end
				end
			},
			[Enum.EasingStyle.Back] = {
				[Enum.EasingDirection.In] = function(Delta)
					return (Delta * Delta) * (Delta * (1.70158 + 1) - 1.70158)
				end,
				[Enum.EasingDirection.Out] = function(Delta)
					return ((Delta - 1) ^ 2) * ((Delta - 1) * (1.70158 + 1) + 1.70158) + 1
				end,
				[Enum.EasingDirection.InOut] = function(Delta)
					if 0 <= Delta and Delta <= 0.5 then
						return (2 * (Delta * Delta)) * ((2 * Delta) * (2.5949095 + 1) - 2.5949095)
					elseif 0.5 <= Delta and Delta <= 1 then
						return (0.5 * ((2 * Delta) - 2) ^ 2) * (((2 * Delta) - 2) * (2.5949095 + 1) + 2.5949095) + 1
					end
				end
			},
			[Enum.EasingStyle.Bounce] = {
				[Enum.EasingDirection.In] = function(Delta)
					if 0 <= Delta and Delta <= (1 / 2.75) then
						return 7.5625 * (Delta * Delta)
					elseif (1 / 2.75) <= Delta and Delta <= (2 / 2.75) then
						return 7.5625 * (Delta - (1.5 / 2.75)) ^ 2 + 0.75
					elseif (2 / 2.75) <= Delta and Delta <= (2.5 / 2.75) then
						return 7.5625 * (Delta - (2.25 / 2.75)) ^ 2 + 0.9375
					elseif (2.5 / 2.75) <= Delta and Delta <= 1 then
						return 7.5625 * (Delta - (2.625 / 2.75)) ^ 2 + 0.984375
					end
				end,
				[Enum.EasingDirection.Out] = function(Delta)
					if 0 <= Delta and Delta <= (0.25 / 2.75) then
						return -7.5625 * (1 - Delta - (2.625 / 2.75)) ^ 2 + 0.015625
					elseif (0.25 / 2.75) <= Delta and Delta <= (0.75 / 2.75) then
						return -7.5625 * (1 - Delta - (2.25 / 2.75)) ^ 2 + 0.0625
					elseif (0.75 / 2.75) <= Delta and Delta <= (1.75 / 2.75) then
						return -7.5625 * (1 - Delta - (1.5 / 2.75)) ^ 2 + 0.25
					elseif (1.75 / 2.75) <= Delta and Delta <= 1 then
						return 1 - 7.5625 * (1 - Delta) ^ 2
					end
				end,
				[Enum.EasingDirection.InOut] = function(Delta)
					if 0 <= Delta and Delta <= (0.125 / 2.75) then
						return 0.5 * (-7.5625 * (1 - (2 * Delta) - (2.625 / 2.75)) ^ 2 + 0.015625)
					elseif (0.125 / 2.75) <= Delta and Delta <= (0.375 / 2.75) then
						return 0.5 * (-7.5625 * (1 - (2 * Delta) - (2.25 / 2.75)) ^ 2 + 0.0625)
					elseif (0.375 / 2.75) <= Delta and Delta <= (0.875 / 2.75) then
						return 0.5 * (-7.5625 * (1 - (2 * Delta) - (1.5 / 2.75)) ^ 2 + 0.25)
					elseif (0.875 / 2.75) <= Delta and Delta <= 0.5 then
						return 0.5 * (1 - 7.5625 * (1 - (2 * Delta)) ^ 2)
					elseif 0.5 <= Delta and Delta <= (1.875 / 2.75) then
						return 0.5 + 3.78125 * ((2 * Delta) - 1) ^ 2
					elseif (1.875 / 2.75) <= Delta and Delta <= (2.375 / 2.75) then
						return 3.78125 * ((2 * Delta) - (4.25 / 2.75)) ^ 2 + 0.875
					elseif (2.375 / 2.75) <= Delta and Delta <= (2.625 / 2.75) then
						return 3.78125 * ((2 * Delta) - (5 / 2.75)) ^ 2 + 0.96875
					elseif (2.625 / 2.75) <= Delta and Delta <= 1 then
						return 3.78125 * ((2 * Delta) - (5.375 / 2.75)) ^ 2 + 0.9921875
					end
				end
			},
			[Enum.EasingStyle.Elastic] = {
				[Enum.EasingDirection.In] = function(Delta)
					return (-2 ^ (10 * (Delta - 1))) * Sin(((2 * Pi) * (Delta - 1 - (0.3 / 4))) / 0.3)
				end,
				[Enum.EasingDirection.Out] = function(Delta)
					return (2 ^ (-10 * Delta)) * Sin(((2 * Pi) * (Delta - (0.3 / 4))) / 0.3) + 1
				end,
				[Enum.EasingDirection.InOut] = function(Delta)
					if 0 <= Delta and Delta <= 0.5 then
						return -0.5 * (2 ^ ((20 * Delta) - 10)) * Sin(((2 * Pi) * ((2 * Delta) - 1.1125)) / 0.45)
					elseif 0.5 <= Delta and Delta <= 1 then
						return 0.5 * (2 ^ ((-20 * Delta) + 10)) * Sin(((2 * Pi) * ((2 * Delta) - 1.1125)) / 0.45) + 1
					end
				end
			},
			[Enum.EasingStyle.Circular] = {
				[Enum.EasingDirection.In] = function(Delta)
					return -Sqrt(1 - Delta ^ 2) + 1
				end,
				[Enum.EasingDirection.Out] = function(Delta)
					return Sqrt(-(Delta - 1) ^ 2 + 1)
				end,
				[Enum.EasingDirection.InOut] = function(Delta)
					if 0 <= Delta and Delta <= 0.5 then
						return -Sqrt(-Delta ^ 2 + 0.25) + 0.5
					elseif 0.5 <= Delta and Delta <= 1 then
						return Sqrt(-(Delta - 1) ^ 2 + 0.25) + 0.5
					end
				end
			}
		}
	end
end
-- 
local crosshair_lineOffsets = utility:generateAngles(4); 
-- 
local Window = Library:Window({Size = UDim2.new(0,580,0,600)})
        local aiming = Window:Page({Name = "Aiming"})
		local esp = Window:Page({Name = "Visuals"})
		local misc = Window:Page({Name = "Misc"})
        local Config = Window:Page({Name = "Config"})
        --
        do -- Aimbot
			-- left
            local Main = aiming:Section({Name = "Main", Size = 330})
				Main:Toggle({Name = "Enabled", Flag = "Silent Enabled", Risk = true})
				Main:Keybind({Name = "Key", Flag = "Silent_Bind", Mode = "Toggle", callback = function()
					misc_flags["target"] = not misc_flags["target"]
					framework:selectTarget(); 
				end})
				-- 	
				Main:Toggle({Name = "Kill Bot", Flag = "Kill Bot", Risk = true})
				Main:Dropdown({Name = "Kill Bot", Flag = "Kill Bot Settings", Options = {"Disable on knock"}, Max = 9e9})
				-- 
				local Main_1 = aiming:Section({Name = "Settings", Size = 330})
				Main_1:Toggle({Name = "Look At", Flag = "Look At"})
				Main_1:Toggle({Name = "Auto Shoot", Flag = "Auto Shoot"})
				Main_1:Toggle({Name = "Spectate", Flag = "Spectate"})
				Main_1:Toggle({Name = "Notify", Flag = "Flag"})

				local Main_1 = aiming:Section({Name = "Methods", Size = 330})
				--Main_1:Toggle({Name = "Aim Viewer Bypass", Flag = "Aim Viewer Bypass"})
				Main_1:Toggle({Name = "Resolver", Flag = "Resolver"})
				Main_1:Dropdown({Name = "Resolver Method", Flag = "Resolver Method", Options = {"Recalculate Velocity", "Suppress Velocity", "Move Direction"}, Default = "Recalculate Velocity"})
				
				local Main_2 = aiming:Section({Name = "Visuals", Size = 330})
				local line1 = Main_2:Toggle({Name = "Line", Flag = "Line Enabled"})
				line1:Colorpicker({Default = Color3.fromRGB(255,0,0), Flag = "Line Settings"});
				Main_2:Slider({Name = "Thickness", Flag = 'Line Thickness', Min = 0, Max = 2, Default = 1, Decimals = 0.01, Callback = function()
					utility.drawings["Tracer"].Thickness = flags["Line Thickness"]
				end})
				local highlight = Main_2:Toggle({Name = "Highlight", Flag = "Highlight Enabled"})
				highlight:Colorpicker({Default = Color3.fromRGB(0,255,0), Alpha = 0.5, Flag = "Highlight Fill Color", Callback = function(a,b) print(a,b) end});
				highlight:Colorpicker({Default = Color3.fromRGB(0,125,0), Flag = "Highlight Outline Color"});
				local backtrack = Main_2:Toggle({Name = "Backtrack", Flag = "Back Track Enabled"})
				backtrack:Colorpicker({Default = Color3.fromRGB(255, 0, 0), alpha = 0.65, Flag = "Back Track Settings"});
				Main_2:Dropdown({Name = "Method", Flag = "Back Track Method", Options = {"Clone", "Follow"}, Default = "Follow"})
				Main_2:Dropdown({Name = "Material", Flag = "Back Track Material", Options = {"Neon", "Plastic", "ForceField"}, Default = "Neon"})
				Main_2:Slider({Name = "Delay", Flag = 'Back Track Delay', Min = 0, Max = 1, Default = 1, Decimals = 0.05})
			-- right 
			local Misc = aiming:Section({Name = "Prediction", Size = 330, Side = "Right"})
				Misc:Toggle({Name = "Auto Prediction", Flag = "Auto Prediction"})
				Misc:Toggle({Name = "Jump Prediction", Flag = "Jump Prediction"})
				Misc:Textbox({Name = "Prediction", Flag = "Manual Prediction Value", Placeholder = "Prediction"})
				Misc:Textbox({Name = "Jump Offset", Flag = "Manual Offset Value", Placeholder = "Jump Offset"})
				Misc:Dropdown({Name = "Hit-Part", Flag = "Single Hit Part", Options = utility.bodyParts, Default = "HumanoidRootPart"})
				Misc:Toggle({Name = "Nearest Part", Flag = "Nearest Part"})
				Misc:Dropdown({Name = "Closest Hit Part", Flag = "Closest Hit Part", Options = utility.bodyParts, Default = {"HumanoidRootPart"}, Max = 9e9})
				
				local Misc_1 = aiming:Section({Name = "Checks", Size = 330, Side = "Right"})
				Misc_1:Dropdown({Name = "Checks", Flag = "Silent Checks", Options = {"Knocked Check", "Wall Check", "Friend Check", "Grabbed Check"}, Max = 9e9})

				local Misc_2 = aiming:Section({Name = "Target Strafe", Size = 330, Side = "Right"})
				Misc_2:Toggle({Name = "Enabled", Flag = "Target Strafe Enabled", Risk = true})
				Misc_2:Slider({Name = "Radius", Flag = 'Target Strafe Distance', Min = -15, Max = 15, Default = 10, Decimals = 1})
				Misc_2:Slider({Name = "Speed", Flag = 'Target Strafe Speed', Min = -15, Max = 15, Default = 10, Decimals = 1})
				Misc_2:Slider({Name = "Height", Flag = 'Target Strafe Height', Min = -15, Max = 15, Default = 0, Decimals = 1})
		end
		-- 	
		do 
			-- left
			local Main = esp:Section({Name = "Main", Size = 330})
				Main:Toggle({Name = "Enabled", Flag = "PlayerESP_Enabled"})
				Main:Slider({Name = "Distance", Flag = 'PlayerESP_ArrowRadius', Min = 0, Max = 5000, Default = 5000, Decimals = 5})
				local box = Main:Toggle({Name = "Boxes", Flag = "PlayerESP_Box"})
				box:Colorpicker({Default = Color3.fromRGB(255, 255, 255), Flag = "PlayerESP_Box_Color1"});
				box:Colorpicker({Default = Color3.fromRGB(0, 0, 0), Flag = "PlayerESP_Box_Color2"});
				Main:Toggle({Name = "Box-Fill", Flag = "PlayerESP_BoxFill"}):Colorpicker({Default = Color3.fromRGB(255, 255, 255), Transparency = 0.7, Flag = "PlayerESP_BoxFill_Color"});
				Main:Dropdown({Name = "Box Type", Flag = "PlayerESP_Box_Type", Options = {"Bounding", "Corner"}, Default = "Bounding"})
				Main:Toggle({Name = "Name", Flag = "PlayerESP_Name"}):Colorpicker({Default = Color3.fromRGB(255, 255, 255), Flag = "PlayerESP_Name_Color"});
				Main:Toggle({Name = "Weapons", Flag = "PlayerESP_Weapon"}):Colorpicker({Default = Color3.fromRGB(255, 255, 255), Flag = "PlayerESP_Weapon_Color"});
				Main:Toggle({Name = "Flags", Flag = "PlayerESP_Flags"}):Colorpicker({Default = Color3.fromRGB(255, 255, 255), Flag = "PlayerESP_FlagsColor"});
				Main:Dropdown({Name = "Flags", Flag = "PlayerESP_Flag_Options", Options = {"Distance", "Knocked"}, Max = 9e9})

			local Main_1 = esp:Section({Name = "Arrows", Size = 330, Side = "Right"})
				local Arrow = Main_1:Toggle({Name = "Enabled", Flag = "PlayerESP_Arrows"})
				Main_1:Toggle({Name = "Dynamic", Flag = "PlayerESP_ArrowsDynamic"})
				Arrow:Colorpicker({Default = Color3.fromRGB(255, 255, 255), Flag = "PlayerESP_ArrowColor"});
				Arrow:Colorpicker({Default = Color3.fromRGB(255, 255, 255), Flag = "PlayerESP_ArrowOutline"});
				Main_1:Slider({Name = "Radius", Flag = 'PlayerESP_ArrowRadius', Min = 0, Max = 100, Default = 20, Decimals = 1})
				Main_1:Slider({Name = "Arrow Size", Flag = 'PlayerESP_ArrowSize', Min = 0, Max = 100, Default = 20, Decimals = 1})

			local Properties = esp:Section({Name = "Properties", Size = 330, Side = "Right"})
				local health = Properties:Toggle({Name = "Health Bar", Flag = "PlayerESP_HealthBar"})
				health:Colorpicker({Default = Color3.fromRGB(0,255,0), Flag = "PlayerESP_HealthBar_Color_Higher"});
				health:Colorpicker({Default = Color3.fromRGB(255,0,0), Flag = "PlayerESP_HealthBar_Color_Low"});
				Properties:Toggle({Name = "Gradient", Flag = "PlayerESP_HealthBarGradient"})
				Properties:Toggle({Name = "Health Number", Flag = "PlayerESP_HealthNumber"})
				Properties:Toggle({Name = "Armor Bar", Flag = "PlayerESP_ArmorBar"}):Colorpicker({Default = Color3.fromRGB(0,0,255), Flag = "PlayerESP_ArmorBarColor"});
			
			local Main_123 = esp:Section({Name = "Lighting", Size = 330, Side = "Left"})
				Main_123:Toggle({Name = "Master Switch", Flag = "Master Switch", Callback = function()
					for i,v in pairs(Lighting_Save) do 
						Lighting[i] = v 
					end 
				end})
				Main_123:Toggle({Name = "Clock Time", Flag = "Clock Time Enabled"})
				Main_123:Slider({Name = "Distance", Flag = 'Clock Time', Min = 0, Max = 24, Default = 12, Decimals = 0.1})
				Main_123:Toggle({Name = "Color Shift Bottom", Flag = "Color Shift Bottom"}):Colorpicker({Default = Color3.fromRGB(255, 255, 255), Flag = "Color Shift Bottom Color"});
				Main_123:Toggle({Name = "Ambient", Flag = "Ambient"}):Colorpicker({Default = Color3.fromRGB(255, 255, 255), Flag = "Ambience Color"});
				Main_123:Toggle({Name = "Outdoor Ambience", Flag = "Outdoor Ambience"}):Colorpicker({Default = Color3.fromRGB(255, 255, 255), Flag = "Outdoor Ambience color"});
				Main_123:Toggle({Name = "Brightness", Flag = "Brightness Enabled"})
				Main_123:Slider({Name = "Brightness", Flag = 'Brightness', Min = 0, Max = 20, Default = 3, Decimals = 1})
				Main_123:Toggle({Name = "Color Shift Top", Flag = "Color Shift Top"}):Colorpicker({Default = Color3.fromRGB(255, 255, 255), Flag = "Color Shift Top Color"});
				Main_123:Toggle({Name = "Fog", Flag = "Fog"}):Colorpicker({Default = Color3.fromRGB(255, 255, 255), Flag = "Fog Color"});

			local Main_2 = esp:Section({Name = "Crosshair", Size = 330, Side = "Right"})
				Main_2:Toggle({Name = "Crosshair", Flag = "Crosshair", Callback = function()
					for i = 1, #crosshair_Lines do
						crosshair_Lines[i].Visible = false; 
					end 
					--
					for i = 1, #crosshair_Outlines do
						crosshair_Outlines[i].Visible = false; 
					end 
				end}):Colorpicker({Default = Color3.fromRGB(255,255,255), Flag = "Crosshair Color", Callback = function()
					for i = 1, #crosshair_Lines do
						crosshair_Lines[i].Color = flags["Crosshair Color"]; 
					end 
				end});
				Main_2:Toggle({Name = "Always Rotating", Flag = "Crosshair Always Rotating"})
				Main_2:Slider({Name = "Speed", Flag = 'Crosshair Speed', Min = 0, Max = 24, Default = 12, Decimals = 0.1})
				Main_2:Slider({Name = "Gap Size", Flag = 'Crosshair Gap Size', Min = 0, Max = 30, Default = 12, Decimals = 1})
				Main_2:Slider({Name = "Length", Flag = 'Crosshair Length', Min = 0, Max = 30, Default = 12, Decimals = 1})
				Main_2:Slider({Name = "Thickness", Flag = 'Crosshair Thickness', Min = 0.1, Max = 5, Default = 1.5, Decimals = 0.1, Callback = function()
					for i = 1, #crosshair_Lines do
						crosshair_Lines[i].Thickness = flags["Crosshair Thickness"]; 
						crosshair_Outlines[i].Thickness = flags["Crosshair Thickness"] * 2.5; 
					end 
				end})
				Main_2:Slider({Name = "Sides", Flag = 'Crosshair Sides', Min = 1, Max = 10, Default = 4, Decimals = 1, callback = function()
					crosshair_LineAmount = flags["Crosshair Sides"]
					-- 
					crosshair_lineOffsets = utility:generateAngles(flags["Crosshair Sides"])
					--
					for i = 1, #crosshair_Lines do
						crosshair_Lines[i]:Remove(); 
						crosshair_Lines[i] = nil; 
					end 
					-- 
					for i = 1, #crosshair_Outlines do
						crosshair_Outlines[i]:Remove(); 
						crosshair_Outlines[i] = nil; 
					end 
					-- 
					do 
						for Index = 1, flags["Crosshair Sides"] do
							local line = utility:drawObject("Line",{
								Visible = false,
								Color = flags["Crosshair Color"],
								Thickness = flags["Crosshair Thickness"],
								ZIndex = 2,
								Transparency = 1
							})
							--
							crosshair_Lines[Index] = line
							--
							local line_1 = utility:drawObject("Line",{
								Visible = false,
								Color = Color3.fromRGB(0, 0, 0),
								Thickness = flags["Crosshair Thickness"] * 2.5,
								ZIndex = 1,
								Transparency = 1
							})
							-- 
							crosshair_Outlines[Index] = line_1
						end
					end 
				end})
				Main_2:Dropdown({Name = "Sizing Easing Style", Flag = "Crosshair Sizing Easing Style", Options = {"Off", "Linear", "Cubic", "Quad", "Quart", "Quint", "Sine", "Exponential", "Back", "Bounce", "Elastic", "Circular"}, Default = "Off"})
				Main_2:Dropdown({Name = "Speed Easing Style", Flag = "Crosshair Speed Easing Style", Options = {"Off", "Linear", "Cubic", "Quad", "Quart", "Quint", "Sine", "Exponential", "Back", "Bounce", "Elastic", "Circular"}, Default = "Off"})
		end 
		-- misc
		do 
			local Main = misc:Section({Name = "General", Size = 330})
				Main:Toggle({Name = "Speed", Flag = "Speed Enabled"}):Keybind({Name = "Speed", Flag = "Silent_Bind", Mode = "Toggle", Callback = function()
					misc_flags["speed"] = not misc_flags["speed"]
				end})
				Main:Slider({Name = "Speed", Flag = 'Speed', Min = 0, Max = 100, Default = 20, Decimals = 1})
				Main:Toggle({Name = "Fly", Flag = "Fly Enabled"}):Keybind({Name = "Fly", Flag = "Silent_Bind", Mode = "Toggle", Callback = function()
					misc_flags["fly"] = not misc_flags["fly"]
				end})	
				Main:Slider({Name = "Fly", Flag = 'Fly Speed', Min = 0, Max = 100, Default = 20, Decimals = 1})
				Main:Toggle({Name = "Bullet Tracers", Flag = "Bullet Tracers"}):Colorpicker({Default = Color3.fromRGB(255, 255, 255), Flag = "Bullet Tracers Color"});
				Main:Slider({Name = "Lifetime", Flag = 'Tracers Life Time', Min = 0, Max = 10, Default = 2, Decimals = 0.1})
			local Main_3 = misc:Section({Name = "Hit Effects", Size = 330, Side = "Right"})
				Main_3:Toggle({Name = "Hit Marker", Flag = "Hit Marker"}):Colorpicker({Default = Color3.fromRGB(255,255,255), Flag = "Hit Marker Settings"});
				Main_3:Toggle({Name = "3D Hit Marker", Flag = "3D Hit Marker"}):Colorpicker({Default = Color3.fromRGB(255,255,255), Flag = "3D Hit Marker Settings"});
				Main_3:Slider({Name = "Fading Time", Flag = 'Hit Markers Time', Min = 0.1, Max = 10.0, Default = 5.0, Decimals = 0.1})
				Main_3:Toggle({Name = "Hit Sounds", Flag = "Hit Sounds"})
				Main_3:Dropdown({Name = "Hit Sounds", Flag = "Hit Sounds Sound", Options = sfx_names, Default = "Neverlose"})
				Main_3:Slider({Name = "Volume", Flag = 'Hit Sounds Volume', Min = 0.1, Max = 10.0, Default = 5.0, Decimals = 0.1})
				Main_3:Slider({Name = "Pitch", Flag = 'Hit Sounds Pitch', Min = 0.1, Max = 10.0, Default = 1.0, Decimals = 0.1})
				Main_3:Toggle({Name = "Hit Effects", Flag = "Hit Effects"}):Colorpicker({Default = Color3.fromRGB(255,255,255), Flag = "Hit Effect Settings"});
				Main_3:Dropdown({Name = "Hit Effects", Flag = "Hit Effects Option", Options = {"Bubble", "Nova"}, Default = "Confetti"})
				Main_3:Toggle({Name = "Hit Chams", Flag = "Hit Chams"}):Colorpicker({Default = Color3.fromRGB(255,255,255), Flag = "Hit Chams Settings"});
				Main_3:Dropdown({Name = "Material", Flag = "Hit Chams Material", Options = {"ForceField", "Neon", "Plastic"}, Default = "Neon"})
				Main_3:Slider({Name = "Fading Time", Flag = 'Hit Chams Fading Time', Min = 0.1, Max = 10.0, Default = 5.0, Decimals = 0.1})
				--[[local Highlight = Main_3:Toggle({Name = "Highlight Hit Chams", Flag = "Highlight Hit Chams"})
				Highlight:Colorpicker({Default = Color3.fromRGB(255,255,255), Flag = "Hit Chams Fill"});
				Highlight:Colorpicker({Default = Color3.fromRGB(255,255,255), Flag = "Hit Chams Outline"});]]
		end
		-- 
        do -- Config
            local Menu = Config:Section({Name = "Menu", Size = 120})
            local Cfgs = Config:Section({Name = "Configs", Size = 200, Side = "Right"})
            --
			local abc = false 
            Menu:Keybind({Name = "Menu key", Flag = "MenuKey", Default = Enum.KeyCode.End, Mode = "Toggle", Callback = function() abc = not abc Library:SetOpen(abc) end})
            --Menu:Colorpicker({Name = "Accent", Flag = "MenuAccent", Default = Library.Accent, Callback = function(s) Library:ChangeAccent(s) end})
            --
            local CFGList = Cfgs:Dropdown({Name = "Cfg List", Flag = "SettingConfigurationList", Options = {}})
            Cfgs:Textbox({Flag = "SettingsConfigurationName", Placeholder = "Config name"})
            --
            local CurrentList = {};
            if not isfolder("Tonka") then 
                makefolder("Tonka")
            end 
            if not isfolder("Tonka/Configs") then 
                makefolder("Tonka/Configs")
            end 
            local function UpdateConfigList()
                local List = {};
                for idx, file in ipairs(listfiles("Tonka/Configs")) do
                    local FileName = file:gsub("Tonka/Configs\\", ""):gsub(".cfg", "")
                    List[#List + 1] = FileName;
                end;
    
                local IsNew = #List ~= #CurrentList
                if not IsNew then
                    for idx, file in ipairs(List) do
                        if file ~= CurrentList[idx] then
                            IsNew = true;
                            break;
                        end;
                    end;
                end;
    
                if IsNew then
                    CurrentList = List;
                    CFGList:Refresh(CurrentList);
                end;
            end;
            --
            Cfgs:Button({Name = "Create", Callback = function()
				local ConfigName = flags.SettingsConfigurationName;
				if ConfigName == "" or isfile("Tonka/Configs/" .. ConfigName .. ".cfg") then
					return;
				end;
				writefile("Tonka/Configs/" .. ConfigName .. ".cfg", "");
				UpdateConfigList();
            end})
            Cfgs:Button({Name = "Save", Callback = function()
				local SelectedConfig = flags.SettingConfigurationList;
				if SelectedConfig then
					writefile("Tonka/Configs/" .. SelectedConfig .. ".cfg", Library:GetConfig())
				end;lback = function()
				local SelectedConfig = flags.SettingConfigurationList;
				if SelectedConfig then
					Library:LoadConfig(readfile("Tonka/Configs/" .. SelectedConfig .. ".cfg"))
				end
            end})
            Cfgs:Button({Name = "Delete", Callback = function()
                local SelectedConfig = flags.SettingConfigurationList;
                if SelectedConfig then
                    delfile("Tonka/Configs/" .. SelectedConfig .. ".cfg")
                end
                UpdateConfigList();
            end})
            Cfgs:Button({Name = "Refresh", Callback = function()
                UpdateConfigList();
            end})
            UpdateConfigList();
            end})
            Cfgs:Button({Name = "Load", Cal
        end

--
do 
	getgenv().offset = nil; 
	local prediction; 
	local partClosest; 
	--
	local checks; 
	local antiCheattick = 0; 
	local CursorSize = 0; 
	framework["connections"]["Main Loop"] = RunService.Heartbeat:Connect(LPH_NO_VIRTUALIZE(function(Fps)
		-- 
		framework:worldVisuals()
		-- 
		if LocalPlayer.Character then 
			framework:cframeSpeed() 
			framework:fly()
		end 
		--
		if utility.target and utility:ValidateClient(utility.target) and misc_flags["target"] then
			prediction = framework:selectPrediction()
			--
			if flags["Resolver"] then 
				offset = framework:calculateResolverOffset(); 
			end       
			-- 
			if flags["Nearest Part"] then 
				partClosest = framework:calculateNearestPart(utility.target, flags["Closest Hit Part"]).Name
			end 
			--
			checks = framework:getChecks(utility.target, table.find(flags["Silent Checks"], "Friend Check"), table.find(flags["Silent Checks"], "Wall Check"), table.find(flags["Silent Checks"], "Knocked Check"), table.find(flags["Silent Checks"], "Grabbed Check"));
			-- 
			if flags["Line Enabled"] then 
				local Position, OnScreen = Camera:WorldToViewportPoint(utility.target.Character.HumanoidRootPart.Position);
				-- 
				utility.drawings["Tracer"].Visible = OnScreen and true or false  
				utility.drawings["Tracer"].From = Vector2.new(Mouse.X, Mouse.Y + 36)
				utility.drawings["Tracer"].To = Vector2.new(Position.X, Position.Y)
				utility.drawings["Tracer"].Color = flags["Line Settings"]
				utility.drawings["Tracer"].Transparency = flags["Line Settings"].transparency
			end
			--
			getgenv().Full = true
			if flags["Target Strafe Enabled"] or not framework:checkForKillBot() then 
				utility.angle = utility.angle + flags["Target Strafe Speed"]
				local strafe = utility.target.Character.HumanoidRootPart.CFrame * CFrame.Angles(0, math.rad(utility.angle), 0) * CFrame.new(0, flags["Target Strafe Height"], flags["Target Strafe Distance"])
				-- 
				if not framework:checkForKillBot() then 
					local OldVel
					local OldPos
					-- 
					local hrp = LocalPlayer.Character.HumanoidRootPart 
					local target_hrp = utility.target.Character.HumanoidRootPart 
					-- 
					hrp.CFrame = target_hrp.CFrame * CFrame.Angles(math.rad(utility.angle), math.rad(utility.angle), math.rad(utility.angle)) * CFrame.new(math.random(10, 15), math.random(10, 15), math.random(10, 15))
				else 
					LocalPlayer.Character.HumanoidRootPart.CFrame = strafe
				end
			end 
			-- 
			if flags["Back Track Enabled"] and flags["Back Track Method"] == "Follow" then 
				for _, Part in pairs(utility.folders["Part Chams"]:GetChildren()) do 
					if Part:IsA("BasePart") and table.find(utility.bodyParts, Part.Name) then 
						Part.Position = utility.target.Character[Part.Name].Position + utility.target.Character.HumanoidRootPart.Velocity * 0.1413
						Part.Rotation = utility.target.Character[Part.Name].Rotation
					end     
				end 
			end 
			-- 
			if flags["Look At"] then 
				LocalPlayer.Character.Humanoid.AutoRotate = false;
				local OldCframe = LocalPlayer.Character.PrimaryPart;
				local NearestRoot = utility.target.Character.HumanoidRootPart
				local NearestPos = CFrame.new(LocalPlayer.Character.PrimaryPart.Position, Vector3.new(NearestRoot.Position.X, OldCframe.Position.Y, NearestRoot.Position.Z));
				LocalPlayer.Character:SetPrimaryPartCFrame(NearestPos);
			end 
			-- 
			if flags["Auto Shoot"] or not framework:checkForKillBot() then 
				local Tool = utility:getHeld(); 
				if Tool then 
					Tool:Activate()
				end 
			end 
		end 
		-- 	
		if tick() - antiCheattick > 1 and LocalPlayer.Character then 
			antiCheattick = tick() 
			-- 
			for _, Script in pairs(LocalPlayer.Character:GetChildren()) do
				if Script:IsA("Script") and Script.Name ~= "Health" and Script.Name ~= "Sound" and Script:FindFirstChild("LocalScript") then
					Script:Destroy()
				end
			end
		end 		
	end))

	framework["connections"]["ESP Loop"] = RunService.RenderStepped:Connect(LPH_NO_VIRTUALIZE(function(Fps)
		if flags["PlayerESP_Enabled"] then  
			for _,Player in pairs(Players:GetPlayers()) do
				local PlayerDrawing = Visuals["Drawings"][Player]
				-- 
				if not PlayerDrawing then continue end
				-- 
				for _,Drawing in pairs(PlayerDrawing) do
					Drawing.Visible = false
				end
				-- 
				for _, Drawing in pairs(Visuals["Drawings"][Player]["Corners"]) do
					if Drawing then 
						Drawing.Visible = false 
					end 
				end 
				-- 
				local Character = Player.Character
				local RootPart, Humanoid, Head = Character and Character:FindFirstChild("HumanoidRootPart"), Character and Character:FindFirstChildOfClass("Humanoid"), Character and Character:FindFirstChild("Head")
				-- 
				if not Character or not RootPart or not Humanoid then continue end
				-- 
				local DistanceFromCharacter = (Camera.CFrame.Position - RootPart.Position).Magnitude
				local MaxDistance = flags["ESP Distance"] or 25000
				-- 
				local Pos, OnScreen = Camera:WorldToViewportPoint(RootPart.Position)
				if MaxDistance < DistanceFromCharacter then continue end 
				--
				if not OnScreen then
					if flags["PlayerESP_Enabled"] and flags["PlayerESP_Arrows"] then
						local Tri = PlayerDrawing.Arrow
						local Tri2 = PlayerDrawing.ArrowOutline
						-- 		
						local rootpartpos = RootPart.Position
						-- 
						Tri.Visible = true
						Tri2.Visible = true
						-- 
						local relativePos = Camera.CFrame:PointToObjectSpace(rootpartpos)
						local angle = math.atan2(-relativePos.y, relativePos.x)

						local size = Floor(viewportSize.x * 0.0078125)
						local max_size = Floor(viewportSize.x * 0.0260416666667)

						local distance = Vector3.new().Dot(relativePos.Unit, relativePos)
						local arrow_dist = flags["PlayerESP_ArrowRadius"]
						local arrow_size = flags["PlayerESP_ArrowsDynamic"] and utility:Map(distance, 1, 100, max_size, flags["PlayerESP_ArrowSize"]) or flags["PlayerESP_ArrowSize"]
						-- 
						arrow_size = arrow_size > max_size and max_size or arrow_size < size and size or arrow_size
						direction = Vector2.new(math.cos(angle), math.sin(angle))
						-- 
						local pos
						if arrow_dist ~= 101 then
							pos = ( direction * viewportSize.x * arrow_dist / 200) + (viewportSize * 0.5)
						end
						-- 
						if not pos or pos.y > viewportSize.y - 5 or pos.y < 5 then
							pos = utility:AngleToEdge(angle, 5)
						end
						-- 
						Tri.PointA = pos
						Tri2.PointA = pos  
						Tri.PointB = pos - utility:getRotate(direction, 0.5) * arrow_size 
						Tri2.PointB = pos - utility:getRotate(direction, 0.5) * arrow_size 
						Tri.PointC = pos - utility:getRotate(direction, -0.5) * arrow_size 
						Tri2.PointC = pos - utility:getRotate(direction, -0.5) * arrow_size
						-- 
						Tri.Color = flags["PlayerESP_ArrowColor"]
						Tri.Transparency = flags["PlayerESP_ArrowColor"].transparency
						-- 
						Tri2.Color = flags["PlayerESP_ArrowOutline"]
						Tri2.Transparency = flags["PlayerESP_ArrowOutline"].transparency
						Tri2.Filled = false
					end
				else
					local BoxSize, BoxPos = utility:BoxCalculation(RootPart)
					-- 
					if flags["PlayerESP_Box"] and flags["PlayerESP_Box_Type"] == "Corner" then -- // Corner Boxes
						BoxCenter = Math:RoundVector(NewVector2(BoxPos.X + BoxSize.X / 2, BoxPos.Y + BoxSize.Y / 2));
						TL = Math:RoundVector(NewVector2(BoxCenter.X - BoxSize.X / 2, BoxCenter.Y - BoxSize.Y / 2));
						BL = Math:RoundVector(NewVector2(BoxCenter.X - BoxSize.X / 2, BoxCenter.Y + BoxSize.Y / 2));
						TR = Math:RoundVector(NewVector2(BoxCenter.X + BoxSize.X / 2, BoxCenter.Y - BoxSize.Y / 2));
						BR = Math:RoundVector(NewVector2(BoxCenter.X + BoxSize.X / 2, BoxCenter.Y + BoxSize.Y / 2));
					end
					-- 
					if flags["PlayerESP_Enabled"] and flags["PlayerESP_Box"] then
						local Box = PlayerDrawing.Box
						local BoxOutline = PlayerDrawing.BoxOutline
						if flags["PlayerESP_Box_Type"] == "Corner" then 
							local BoxCorners, BoxColor1, BoxColor2 = Visuals["Drawings"][Player]["Corners"], flags["PlayerESP_Box_Color1"], flags["PlayerESP_Box_Color2"]
							-- Inlines
							do
								BoxCorners[1].Visible = true
								BoxCorners[1].From = TL
								BoxCorners[1].To = BoxCorners[1].From + NewVector2(0, BoxSize.X / 3)  
								BoxCorners[1].Color = BoxColor1
								--
								BoxCorners[2].Visible = true
								BoxCorners[2].From = TL + NewVector2(1, 0)
								BoxCorners[2].To = BoxCorners[2].From + NewVector2(BoxSize.X / 3, 0)
								BoxCorners[2].Color = BoxColor1
								--
								BoxCorners[3].Visible = true
								BoxCorners[3].From = TR
								BoxCorners[3].To = BoxCorners[3].From + NewVector2(-BoxSize.X / 3, 0)
								BoxCorners[3].Color = BoxColor1
								--
								BoxCorners[4].Visible = true
								BoxCorners[4].From = TR
								BoxCorners[4].To = BoxCorners[4].From + NewVector2(0, BoxSize.X / 3)
								BoxCorners[4].Color = BoxColor1
								--
								BoxCorners[5].Visible = true
								BoxCorners[5].From = BR + NewVector2(0, 1)
								BoxCorners[5].To = BoxCorners[5].From + NewVector2(0, -BoxSize.X / 3)
								BoxCorners[5].Color = BoxColor1
								--
								BoxCorners[6].Visible = true
								BoxCorners[6].From = BR
								BoxCorners[6].To = BoxCorners[6].From + NewVector2(-BoxSize.X / 3, 0)
								BoxCorners[6].Color = BoxColor1
								--
								BoxCorners[7].Visible = true
								BoxCorners[7].From = BL + NewVector2(0, 1)
								BoxCorners[7].To = BoxCorners[7].From + NewVector2(0, -BoxSize.X / 3)
								BoxCorners[7].Color = BoxColor1
								--
								BoxCorners[8].Visible = true
								BoxCorners[8].From = BL
								BoxCorners[8].To = BoxCorners[8].From + NewVector2(BoxSize.X / 3, 0)
								BoxCorners[8].Color = BoxColor1
							end
							-- // Outlines
							do
								BoxCorners[9].Visible = true
								BoxCorners[9].From = BoxCorners[1].From + NewVector2(0, -1)
								BoxCorners[9].To = BoxCorners[1].To + NewVector2(0, 1)
								BoxCorners[9].Color = BoxColor2
								--
								BoxCorners[10].Visible = true
								BoxCorners[10].From = BoxCorners[2].From
								BoxCorners[10].To = BoxCorners[2].To + NewVector2(1, 0)
								BoxCorners[10].Color = BoxColor2
								--
								BoxCorners[11].Visible = true
								BoxCorners[11].From = BoxCorners[3].From + NewVector2(2, 0)
								BoxCorners[11].To = BoxCorners[3].To + NewVector2(-1, 0)
								BoxCorners[11].Color = BoxColor2
								--
								BoxCorners[12].Visible = true
								BoxCorners[12].From = BoxCorners[4].From
								BoxCorners[12].To = BoxCorners[4].To + NewVector2(0, 1)
								BoxCorners[12].Color = BoxColor2
								--
								BoxCorners[13].Visible = true
								BoxCorners[13].From = BoxCorners[5].From
								BoxCorners[13].To = BoxCorners[5].To + NewVector2(0, -1)
								BoxCorners[13].Color = BoxColor2
								--
								BoxCorners[14].Visible = true
								BoxCorners[14].From = BoxCorners[6].From + NewVector2(2, 0)
								BoxCorners[14].To = BoxCorners[6].To + NewVector2(-1, 0)
								BoxCorners[14].Color = BoxColor2
								--
								BoxCorners[15].Visible = true
								BoxCorners[15].From = BoxCorners[7].From
								BoxCorners[15].To = BoxCorners[7].To + NewVector2(0, -1)
								BoxCorners[15].Color = BoxColor2
								--
								BoxCorners[16].Visible = true
								BoxCorners[16].From = BoxCorners[8].From + NewVector2(-1, 0)
								BoxCorners[16].To = BoxCorners[8].To + NewVector2(1, 0)
								BoxCorners[16].Color = BoxColor2
							end
						else 
							Box.Size = BoxSize
							Box.Position = BoxPos
							Box.Visible = true
							Box.Color = flags["PlayerESP_Box_Color1"]
							BoxOutline.Size = BoxSize
							BoxOutline.Color = flags["PlayerESP_Box_Color2"]
							BoxOutline.Position = BoxPos
							BoxOutline.Visible = true
						end 
					end
					-- 
					if flags["PlayerESP_Enabled"] and flags["PlayerESP_Name"] then
						local Name = PlayerDrawing.Name
						Name.Text = ""..Player.Name..""
						Name.Position = NewVector2(BoxSize.X / 2 + BoxPos.X, BoxPos.Y - 16)
						Name.Color = flags["PlayerESP_Name_Color"]
						Name.Visible = true
					end
					-- 
					if flags["PlayerESP_Enabled"] and flags["PlayerESP_HealthBar"] then
						local Health         = PlayerDrawing.Health
						local HealthOutline  = PlayerDrawing.HealthOutline
						local HealthText     = PlayerDrawing.HealthText
						local HealthBarGradient = PlayerDrawing.HealthBarGradient
						local ArmorBarOutline = PlayerDrawing.ArmorBarOutline
						local Armor_Bar = PlayerDrawing.ArmorBar
						
						local Color = utility:Lerp(Humanoid.Health / Humanoid.MaxHealth, flags["PlayerESP_HealthBar_Color_Higher"], flags["PlayerESP_HealthBar_Color_Low"])
						local HealthSize = (Floor(BoxSize.Y * (Humanoid.Health / Humanoid.MaxHealth)))
						local Height = ((BoxPos.Y + BoxSize.Y) - HealthSize) 
						-- 
						Health.Size = NewVector2(1, HealthSize)
						Health.Position = NewVector2(BoxPos.X - 2 - 1, Height)
						Health.Color = Color
						Health.Visible = true
						Health.Filled = true 
						-- 
						HealthOutline.Size = NewVector2(3, BoxSize.Y + 2)
						HealthOutline.Position = NewVector2(BoxPos.X - 2 - 2, BoxPos.Y - 1)
						HealthOutline.Visible = true 
						HealthOutline.Color = Color3.fromRGB(0, 0, 0)
						HealthOutline.Filled = true 
						-- 
						if flags["PlayerESP_HealthBarGradient"] then 
							HealthBarGradient.Size = NewVector2(2 + 2, BoxSize.Y + 2)
							HealthBarGradient.Position = NewVector2(BoxPos.X - (2 * 2) - 1, BoxPos.Y - 1)
							HealthBarGradient.Visible = true 
						end 
						-- 
						if flags["PlayerESP_Enabled"] and flags["PlayerESP_HealthNumber"] then
							HealthText.Text = "".. Floor(Humanoid.Health) .. ""
							HealthText.Color = Color
							HealthText.Visible = true
							-- 
							local HealthNumberPos = NewVector2((BoxPos.X + 1), BoxPos.Y + BoxSize.Y)
							HealthText.Position = NewVector2(HealthOutline.Position.X - (2 + 8), HealthNumberPos.Y - (Humanoid.Health / Humanoid.MaxHealth) * BoxSize.Y)
						end 
						--
						if flags["PlayerESP_ArmorBar"] and Character.BodyEffects.Armor.Value > 0 then 
							local AmourSize = (Floor(BoxSize.Y * (Character.BodyEffects.Armor.Value / 200)))
							local Height_2 = ((BoxPos.Y + BoxSize.Y) - AmourSize) 
							
							Armor_Bar.Visible = true 
							Armor_Bar.Color = Color3.fromRGB(0,0,255)
							Armor_Bar.Filled = true
							Armor_Bar.Size = NewVector2(1, AmourSize)
							Armor_Bar.Position = NewVector2(BoxPos.X - 2 - 5, Height_2)
							Armor_Bar.ZIndex = 999999

							ArmorBarOutline.Visible = true 
							ArmorBarOutline.Color = Color3.fromRGB(0,0,0)
							ArmorBarOutline.Size = NewVector2(3, BoxSize.Y + 2)
							ArmorBarOutline.Position = NewVector2(BoxPos.X - 2 - 6, BoxPos.Y - 1)
							ArmorBarOutline.Filled = true
							
							local HealthNumberPos = NewVector2((BoxPos.X + 1), BoxPos.Y + BoxSize.Y)
							HealthText.Position = NewVector2(HealthOutline.Position.X - (2 + 13), HealthNumberPos.Y - (Humanoid.Health / Humanoid.MaxHealth) * BoxSize.Y)
						else 
							Armor_Bar.Visible = false 
							ArmorBarOutline.Visible = false 
						end
					end
					-- 
					if flags["PlayerESP_Enabled"] and flags["PlayerESP_Weapon"] then
						local Tool = PlayerDrawing.Tool
						local BottomOffset = BoxSize.Y + BoxPos.Y + 1
						local Equipped = Player.Character:FindFirstChildOfClass("Tool") and Player.Character:FindFirstChildOfClass("Tool").Name or ""
						Tool.Text = ""..Equipped..""
						Tool.Position = NewVector2(BoxSize.X / 2 + BoxPos.X, BottomOffset)
						Tool.Color = flags["PlayerESP_Weapon_Color"]
						Tool.Visible = true
						BottomOffset = BottomOffset + 15
					end
					-- 
					if flags["PlayerESP_Enabled"] and flags["PlayerESP_BoxFill"] then 
						local BoxFill = PlayerDrawing.BoxFill
						BoxFill.Size = BoxSize
						BoxFill.Position = BoxPos
						BoxFill.Visible = true
						BoxFill.Color = flags["PlayerESP_BoxFill_Color"]
						BoxFill.Transparency = 1 - flags["PlayerESP_BoxFill_Color"].transparency
					end 
					-- 
					if flags["PlayerESP_Enabled"] and flags["PlayerESP_Flags"] then
						local Flag = PlayerDrawing.Flag
						local FlagStr = ""
						-- 
						if Find(flags["PlayerESP_Flag_Options"], "Distance") then
							FlagStr ..= ("%sm\n"):format(Round(DistanceFromCharacter))
						end
						-- 
						if Find(flags["PlayerESP_Flag_Options"], "Knocked") and Player.Character.BodyEffects then
							FlagStr ..= ("%s\n"):format(tostring(Player.Character.BodyEffects["K.O"].Value and "KNOCKED" or ""))
						end
						--
						Flag.Text = FlagStr
						Flag.Position = NewVector2(BoxSize.X + BoxPos.X + 14, BoxPos.Y - 4)
						Flag.Visible = true
						Flag.Color = flags["PlayerESP_FlagsColor"]
					end 
				end 
			end
		else 
			for _,Player in pairs(Players:GetPlayers()) do
				local PlayerDrawing = Visuals["Drawings"][Player]
				-- 
				if not PlayerDrawing then continue end
				-- 
				for _,Drawing in pairs(PlayerDrawing) do
					Drawing.Visible = false
				end
				-- 
				for _, Drawing in pairs(Visuals["Drawings"][Player]["Corners"]) do
					if Drawing then 
						Drawing.Visible = false 
					end 
				end 
			end 
		end
		--
		crosshair_SpinAngle = flags["Crosshair Always Rotating"] and crosshair_SpinAngle + math.rad((flags["Crosshair Speed"] * 10) * Fps) or 0;  
		--
		if flags["Crosshair"] then 
			local Radius = flags["Crosshair Length"] * 5
			local Gap = flags["Crosshair Gap Size"] 
			CursorSize += 0.025
			-- 
			local SmoothAngle = flags["Crosshair Speed Easing Style"] ~= "Off" and Tween.EasingStyles[Enum.EasingStyle[flags["Crosshair Speed Easing Style"]]][Enum.EasingDirection.InOut](utility:Shift(crosshair_SpinAngle)) * (Pi * Pi/2) or crosshair_SpinAngle
			local Dynamic = Cos(CursorSize)
			local SmoothSize =  flags["Crosshair Sizing Easing Style"] ~= "Off" and ((Radius / 2) * (Tween.EasingStyles[Enum.EasingStyle[flags["Crosshair Sizing Easing Style"]]][Enum.EasingDirection.In](utility:Shift(Dynamic)))) or 0 
			local localRadius = Radius - SmoothSize
			--
			for i = 1, #crosshair_Lines do 
				local Positions = Vector2.new(Cos(SmoothAngle + crosshair_lineOffsets[i]), (Sin(SmoothAngle + crosshair_lineOffsets[i])))
				local Mouse_Position = Vector2.new(Mouse.X, Mouse.Y + Offset)
				-- 
				crosshair_Lines[i].From = Mouse_Position + Vector2.new(Positions.X, Positions.Y) * Gap 
				crosshair_Lines[i].To = crosshair_Lines[i].From + Vector2.new(Positions.X, Positions.Y) * localRadius
				-- 
				crosshair_Outlines[i].From = Mouse_Position + Vector2.new(Positions.X, Positions.Y) * (Gap - 1)
				crosshair_Outlines[i].To = crosshair_Lines[i].From + Vector2.new(Positions.X, Positions.Y) * (localRadius + 1)
				-- 
				crosshair_Lines[i].Visible = true 
				crosshair_Outlines[i].Visible = true 
			end 
		end 
	end))

	framework["connections"]["ESP Player Find Loop"] = Players.PlayerAdded:Connect(LPH_NO_VIRTUALIZE(function(Player)
		ESP:Add(Player)
	end))

	framework["connections"]["ESP Player Removed Loop"] = Players.PlayerRemoving:Connect(LPH_NO_VIRTUALIZE(function(Player)
		if Visuals["Drawings"][Player] or Visuals["Drawings"][Player]["Corners"] then
			for Index, Drawing in pairs(Visuals["Drawings"][Player]) do
				if Drawing and Index ~= "Corners" then 
					Drawing:Remove()
				end 
			end        
			--
			for Index = 1, 16 do
				Visuals["Drawings"][Player]["Corners"][Index]:Remove()
			end
			-- 
			Visuals["Drawings"][Player]["Corners"] = nil
			Visuals["Drawings"][Player] = nil
		end
		-- 
		--[[if flags["PlayerESP_Chams"] then 
			utility:Cham_Remove(Player)
		end ]]
	end))
	--
	framework["connections"]["Detect Rays"] = Workspace.Ignored.Siren.Radius.DescendantAdded:Connect(LPH_NO_VIRTUALIZE(function(a)
		pcall(function()
			if flags["Bullet Tracers"] then 
				if Workspace.Ignored.Siren.Radius:FindFirstChild("BULLET_RAYS") then 
					framework:translateBeam(Workspace.Ignored.Siren.Radius.BULLET_RAYS)
				end 
			end 
		end)
	end))
	-- Aim Viewer Bypass and Hit Detection
	do 
		local function Aimbot() 
		end 	

		local function Ammo()
			framework:detectHit()
		end 	

		framework["connections"]["Anti Aim Viewer"] = {} 
		framework["connections"]["hit detection >_<"] = {}
		for i, v in pairs(LocalPlayer.Backpack:GetChildren()) do
			if v:IsA("Tool") and v:FindFirstChild("Ammo") then
				if not framework["connections"]["Anti Aim Viewer"][v] then 
					framework["connections"]["Anti Aim Viewer"][v] = v.Activated:Connect(Aimbot)
				end 
				--
				if not framework["connections"]["hit detection >_<"][v] then 
					framework["connections"]["hit detection >_<"][v] = v.Ammo:GetPropertyChangedSignal("Value"):Connect(Ammo)
				end 
			end
		end
		for i, v in pairs(LocalPlayer.Character:GetChildren()) do
			if v:IsA("Tool") and v:FindFirstChild("Ammo") then
				if not framework["connections"]["Anti Aim Viewer"][v] then 
					framework["connections"]["Anti Aim Viewer"][v] = v.Activated:Connect(Aimbot)
				end 
				--
				if not framework["connections"]["hit detection >_<"][v] then 
					framework["connections"]["hit detection >_<"][v] = v.Ammo:GetPropertyChangedSignal("Value"):Connect(Ammo)
				end 
			end
		end
		LocalPlayer.Character.ChildAdded:connect(function(v)
			if v:IsA("Tool") and v:FindFirstChild("Ammo") then
				if not framework["connections"]["Anti Aim Viewer"][v] then 
					framework["connections"]["Anti Aim Viewer"][v] = v.Activated:Connect(Aimbot)
				end 
				--
				if not framework["connections"]["hit detection >_<"][v] then 
					framework["connections"]["hit detection >_<"][v] = v.Ammo:GetPropertyChangedSignal("Value"):Connect(Ammo)
				end 
			end
		end)
		LocalPlayer.CharacterAdded:connect(function(v)
			for i = 1, #framework["connections"]["Anti Aim Viewer"], 1 do
				framework["connections"]["Anti Aim Viewer"][i]:Disconnect()
				framework["connections"]["Anti Aim Viewer"][i] = nil
				framework["connections"]["hit detection >_<"][i]:Disconnect()
				framework["connections"]["hit detection >_<"][i] = nil
			end
			v.ChildAdded:connect(function(v)
				if v:IsA("Tool") and v:FindFirstChild("Ammo") then
					if not framework["connections"]["Anti Aim Viewer"][v] then 
						framework["connections"]["Anti Aim Viewer"][v] = v.Activated:Connect(Aimbot)
					end 
					--
					if not framework["connections"]["hit detection >_<"][v] then 
						framework["connections"]["hit detection >_<"][v] = v.Ammo:GetPropertyChangedSignal("Value"):Connect(Ammo)
					end 
				end
			end)
		end)
	end 	
	-- // Clone Chams
	task.spawn(function()
		while true do 
			task.wait(flags["Back Track Delay"]/2)
			if utility.target and utility:ValidateClient(utility.target) then 
				if flags["Back Track Enabled"] and flags["Back Track Method"] == "Clone" then
					utility:characterClone(utility.target, flags["Back Track Settings"], flags["Back Track Material"], flags["Back Track Settings"].transparency, utility.folders["Part Chams"]);
					task.wait(flags["Back Track Delay"]/2)
					utility.folders["Part Chams"]:ClearAllChildren(); 
				end     
			end 
		end 
	end)

	local Old; 
	Old = hookmetamethod(game, "__namecall", LPH_NO_VIRTUALIZE(function(self, ...)
		if tostring(self.Name) == "MainEvent" then 
			local Args = {...}
			-- 
			if getnamecallmethod() == "FireServer" and Args[1] == "UpdateMousePos" then 
				if utility.target and utility.target.Character and misc_flags["target"] then 
					local part = (flags["Jump Prediction"] and utility.target.Character.Humanoid.FloorMaterial == Enum.Material.Air and "RightFoot") or (flags["Nearest Part"] and partClosest) or flags["Single Hit Part"]
					local yOffset = utility.target.Character.Humanoid.FloorMaterial == Enum.Material.Air and flags["Manual Offset Value"] or 0 
					--
					if (checks == true) then 
						if flags["Resolver"] then  
							Args[2] = utility.target.Character[tostring(part)].Position + offset + NewVector3(0, yOffset, 0)
						else 
							Args[2] = utility.target.Character[tostring(part)].Position + (utility.target.Character.HumanoidRootPart.Velocity * prediction) + NewVector3(0, yOffset, 0)
						end   
					end   

				end 
			end 
			--
			return Old(self, unpack(Args))
		end 
		-- 
		return Old(self, ...)
	end))
end
