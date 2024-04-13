local Fluent = loadstring(game:HttpGet("https://github.com/dawid-scripts/Fluent/releases/latest/download/main.lua"))()
local SaveManager = loadstring(game:HttpGet("https://raw.githubusercontent.com/dawid-scripts/Fluent/master/Addons/SaveManager.lua"))()
local InterfaceManager = loadstring(game:HttpGet("https://raw.githubusercontent.com/dawid-scripts/Fluent/master/Addons/InterfaceManager.lua"))()

local Window = Fluent:CreateWindow({
    Title = "Fluent " .. Fluent.Version,
    SubTitle = "by dawid",
    TabWidth = 160,
    Size = UDim2.fromOffset(580, 460),
    Acrylic = true, -- The blur may be detectable, setting this to false disables blur entirely
    Theme = "Dark",
    MinimizeKey = Enum.KeyCode.LeftControl -- Used when theres no MinimizeKeybind
})

--Fluent provides Lucide Icons https://lucide.dev/icons/ for the tabs, icons are optional
local Tabs = {
    Main = Window:AddTab({ Title = "Main", Icon = "" }),
    Settings = Window:AddTab({ Title = "Settings", Icon = "settings" })
}

local Options = Fluent.Options

do
    Fluent:Notify({
        Title = "Notification",
        Content = "This is a notification",
        SubContent = "SubContent", -- Optional
        Duration = 5 -- Set to nil to make the notification not disappear
    })



    Tabs.Main:AddParagraph({
        Title = "Paragraph",
        Content = "This is a paragraph.\nSecond line!"
    })



    Tabs.Main:AddButton({
        Title = "Button",
        Description = "Ativado👑",
        Callback = function()
            Window:Dialog({
                Title = "STAR KING",
                Content = "This is a dialog",
                Buttons = {
                    {
                        Title = "Confirm",
                        Callback = function()
                            print("Confirmed the dialog.")
                        end
                    },
                    {
                        Title = "Cancel",
                        Callback = function()
                            print("Cancelled the dialog.")
                        end
                    }
                }
            })
        end
    })



    local Toggle = Tabs.Main:AddToggle("MyToggle", {Title = "Toggle", Default = false })

    Toggle:OnChanged(function()
        print("Toggle changed:", Options.MyToggle.Value)
    end)

    Options.MyToggle:SetValue(false)


    
    local Slider = Tabs.Main:AddSlider("Slider", {
        Title = "Slider",
        Description = "This is a slider",
        Default = 2,
        Min = 0,
        Max = 5,
        Rounding = 1,
        Callback = function(Value)
            print("Slider was changed:", Value)
        end
    })

    Slider:OnChanged(function(Value)
        print("Slider changed:", Value)
    end)

    Slider:SetValue(3)



    local Dropdown = Tabs.Main:AddDropdown("Dropdown", {
        Title = "Dropdown",
        Values = {"one", "two", "three", "four", "five", "six", "seven", "eight", "nine", "ten", "eleven", "twelve", "thirteen", "fourteen"},
        Multi = false,
        Default = 1,
    })

    Dropdown:SetValue("four")

    Dropdown:OnChanged(function(Value)
        print("Dropdown changed:", Value)
    end)


    
    local MultiDropdown = Tabs.Main:AddDropdown("MultiDropdown", {
        Title = "Dropdown",
        Description = "You can select multiple values.",
        Values = {"one", "two", "three", "four", "five", "six", "seven", "eight", "nine", "ten", "eleven", "twelve", "thirteen", "fourteen"},
        Multi = true,
        Default = {"seven", "twelve"},
    })

    MultiDropdown:SetValue({
        three = true,
        five = true,
        seven = false
    })

    MultiDropdown:OnChanged(function(Value)
        local Values = {}
        for Value, State in next, Value do
            table.insert(Values, Value)
        end
        print("Mutlidropdown changed:", table.concat(Values, ", "))
    end)



    local Colorpicker = Tabs.Main:AddColorpicker("Colorpicker", {
        Title = "Colorpicker",
        Default = Color3.fromRGB(96, 205, 255)
    })

    Colorpicker:OnChanged(function()
        print("Colorpicker changed:", Colorpicker.Value)
    end)
    
    Colorpicker:SetValueRGB(Color3.fromRGB(0, 255, 140))



    local TColorpicker = Tabs.Main:AddColorpicker("TransparencyColorpicker", {
        Title = "Colorpicker",
        Description = "but you can change the transparency.",
        Transparency = 0,
        Default = Color3.fromRGB(96, 205, 255)
    })

    TColorpicker:OnChanged(function()
        print(
            "TColorpicker changed:", TColorpicker.Value,
            "Transparency:", TColorpicker.Transparency
        )
    end)



    local Keybind = Tabs.Main:AddKeybind("Keybind", {
        Title = "KeyBind",
        Mode = "Toggle", -- Always, Toggle, Hold
        Default = "LeftControl", -- String as the name of the keybind (MB1, MB2 for mouse buttons)

        -- Occurs when the keybind is clicked, Value is `true`/`false`
        Callback = function(Value)
            print("Keybind clicked!", Value)
        end,

        -- Occurs when the keybind itself is changed, `New` is a KeyCode Enum OR a UserInputType Enum
        ChangedCallback = function(New)
            print("Keybind changed!", New)
        end
    })

    -- OnClick is only fired when you press the keybind and the mode is Toggle
    -- Otherwise, you will have to use Keybind:GetState()
    Keybind:OnClick(function()
        print("Keybind clicked:", Keybind:GetState())
    end)

    Keybind:OnChanged(function()
        print("Keybind changed:", Keybind.Value)
    end)

    task.spawn(function()
        while true do
            wait(1)

            -- example for checking if a keybind is being pressed
            local state = Keybind:GetState()
            if state then
                print("Keybind is being held down")
            end

            if Fluent.Unloaded then break end
        end
    end)

    Keybind:SetValue("MB2", "Toggle") -- Sets keybind to MB2, mode to Hold


    local Input = Tabs.Main:AddInput("Input", {
        Title = "Input",
        Default = "Default",
        Placeholder = "Placeholder",
        Numeric = false, -- Only allows numbers
        Finished = false, -- Only calls callback when you press enter
        Callback = function(Value)
            print("Input changed:", Value)
        end
    })

    Input:OnChanged(function()
        print("Input updated:", Input.Value)
    end)
end


-- Addons:
-- SaveManager (Allows you to have a configuration system)
-- InterfaceManager (Allows you to have a interface managment system)

-- Hand the library over to our managers
SaveManager:SetLibrary(Fluent)
InterfaceManager:SetLibrary(Fluent)

-- Ignore keys that are used by ThemeManager.
-- (we dont want configs to save themes, do we?)
SaveManager:IgnoreThemeSettings()

-- You can add indexes of elements the save manager should ignore
SaveManager:SetIgnoreIndexes({})

-- use case for doing it this way:
-- a script hub could have themes in a global folder
-- and game configs in a separate folder per game
InterfaceManager:SetFolder("FluentScriptHub")
SaveManager:SetFolder("FluentScriptHub/specific-game")

InterfaceManager:BuildInterfaceSection(Tabs.Settings)
SaveManager:BuildConfigSection(Tabs.Settings)


Window:SelectTab(1)

Fluent:Notify({
    Title = "Fluent",
    Content = "The script has been loaded.",
    Duration = 8
})

-- You can use the SaveManager:LoadAutoloadConfig() to load a config
-- which has been marked to be one that auto loads!
SaveManager:LoadAutoloadConfig()










local yo = game:GetService('Players').LocalPlayer
local folderData = game.ReplicatedStorage.Datas[yo.UserId]
local afk = game:service'VirtualUser'
local statsRequeridosFarm = 10000
local events = game.ReplicatedStorage.Package.Events
local equipRemote = game:GetService("ReplicatedStorage").Package.Events.equipskill 
local cargaAndBloqueo = true
local activadaSpeed = false
local statsPlayerFarmSa


print('nuevo script BY Vaquito, si usas mi script sabes que soy la vaca');

local millon = 1000000
local arregloAtaques = {
	{name = "God Slicer",requerido = millon * 60},
	{name = "Spirit Barrage",requerido = millon * 60},
	{name = "Super Dragon Fist",requerido = millon * 50},
	{name = "Flash Kick",requerido = millon / 2},
	{name = "Spirit Breaking Cannon",requerido = 200000},
	{name = "Mach Kick",requerido = 90000},
	{name = "High Power Rush",requerido = 65000},
	{name = "Meteor Crash",requerido = 28000},
	{name = "Wolf Fang Fist",requerido = 2000},
}
local ataquesEnergy = {
	{name = 'Soul Punisher',subName = 'Hak',fuerza = 40000000},
	{name = 'Destruction',subName = 'Hak',fuerza = 40000000},
	{name = 'Energy Volley',subName = 'voleys',fuerza = 4000},
}

local multiQuest = {
	bossEarth = {
		{nombre= "SSJG Kakata",minimo = 50000000},
		{nombre= "Broccoli",minimo = 15500000},
		{nombre= "SSJB Wukong",minimo = 3000000},
		{nombre= "Kai-fist Master",minimo = 1825000},
		{nombre= "SSJ2 Wukong",minimo = 1475000},
		{nombre= "Perfect Atom",minimo = 1100000},
		{nombre= "Chilly",minimo = 800000},
		{nombre= "Super Vegetable",minimo = 227500},
		{nombre= "Mapa",minimo = 120000},
		{nombre= "Radish",minimo = 80000},
		{nombre= "Kid Nohag",minimo = 45000},
		{nombre= "Klirin",minimo = 10000},
	},
	bossBills = {
		{nombre= "Vekuta (SSJBUI)",minimo = 5875000000},
		{nombre= "Wukong Rose",minimo = 3950000000},
		{nombre= "Vekuta (LBSSJ4)",minimo = 1950000000},
		{nombre= "Wukong (LBSSJ4)",minimo = 985000000},
		{nombre= "Vegetable (LBSSJ4)",minimo = 685000000},
		{nombre= "Vis (20%)",minimo = 450000000},
		{nombre= "Vills (50%)",minimo = 285000000},
		{nombre= "Wukong (Omen)",minimo = 200000000},
		{nombre= "Vegetable (GoD in-training)",minimo = 175000000},
	}
}

local transformaciones = {
	fasesBug = {
		{name = "Godly SSJ2",fuerza = 8000000},
		{name = "LSSJ Kaioken",fuerza = 160000},
		{name = "SSJ2 Kaioken",fuerza = 50000},
		{name = "Mystic",fuerza = 200000},
		{name = "SSJ3	",fuerza = 95000},
		{name = "SSJ Kaioken",fuerza = 16000},
	},
	fases = {
		{name = "Blanco",fuerza = 120000000},
		{name = "Beast",fuerza = 180000000000000000000},
		{name = "SSJBUI",fuerza = 120000000},
		{name = "Ultra Ego",fuerza =  120000000},
		{name = "SSJB4",fuerza =50000000},
		{name = "LBSSJ4",fuerza = 100000000},
		{name = "True God of Creation",fuerza = 30000000},
		{name = "True God of Destruction",fuerza = 30000000},
		{name = "SSJR3",fuerza = 50000000},
		{name = "God of Creation",fuerza = 30000000},
		{name = "God of Destruction",fuerza = 30000000},
		{name = "Super Broly",fuerza = 4000000},
		{name = "Jiren Ultra Instinct",fuerza = 14000000},
		{name = "Mastered Ultra Instinct",fuerza = 14000000},
		{name = "Godly SSJ2",fuerza = 8000000},
		{name = "LSSJG",fuerza = 3000000},
		{name = "Ultra Instinct Omen",fuerza = 5000000},
		{name = "LSSJ4",fuerza = 1800000},
		{name = "SSJG4",fuerza = 1000000},
		{name = "Evil SSJ",fuerza = 4000000},
		{name = "Blue Evolution",fuerza = 3500000},
		{name = "LSSJ3",fuerza = 800000},
		{name = "Dark Rose",fuerza = 3500000},
		{name = "SSJ Berseker",fuerza = 3000000},
		{name = "Kefla SSJ2",fuerza = 3000000},
		{name = "True Rose",fuerza = 2400000},
		{name = "SSJ Blue Kaioken",fuerza = 2200000},
		{name = "SSJ5",fuerza = 550000},
		{name = "Mystic Kaioken",fuerza = 250000},
		{name = "SSJ Rose",fuerza = 1400000},
		{name = "SSJ Blue",fuerza = 1200000},
		{name = "LSSJ Kaioken",fuerza = 160000},
		{name = "Corrupt SSJ",fuerza = 700000},
		{name = "SSJ Rage",fuerza = 700000},
		{name = "SSJ2 Kaioken",fuerza = 50000},
		{name = "SSJ4",fuerza = 300000},
		{name = "Mystic",fuerza = 200000},
		{name = "LSSJ",fuerza = 140000},
		{name = "SSJ3",fuerza =95000},
		{name = "SSJ2 Majin",fuerza = 65000},
		{name = "Spirit SSJ",fuerza = 65000},
		{name = "SSJ Kaioken",fuerza = 16000},
	}
}


local function rebirthzzzz()
	return folderData.Rebirth.Value
end
local function strength()
	return folderData.Strength.Value
end
local function energy()
	return folderData.Energy.Value
end
local function defense()
	return folderData.Defense.Value
end
local function speed()
	return folderData.Speed.Value
end

local function selectedForm()	
	return game.Players.LocalPlayer.Status.SelectedTransformation.Value
end
local function valorFase()	
	return game.Players.LocalPlayer.Status.Transformation.Value
end

function characterInvisible()
	return yo.Character
end

function player()
	return yo.Character and yo.Character.Humanoid and yo.Character.Humanoid.Health > 0 and yo.Character:FindFirstChild("HumanoidRootPart")
end

function misionSeleccionada()
	return game:GetService("ReplicatedStorage").Datas[yo.UserId].Quest.Value
end

local function sigueEnemigo(enemigo)
	yo.Character.HumanoidRootPart.CFrame = enemigo	
end

local function kiRequerido()
	return game:GetService("Players").LocalPlayer.Character.Stats.Ki.MaxValue / 10
end
local function kiTotal()
	return game:GetService("Players").LocalPlayer.Character.Stats.Ki.MaxValue / 2
end
local function ki()
	return game.Workspace.Living[yo.Name].Stats.Ki.Value
end

function rebirth()
	
end

function ejecutarForma()
	while selectedForm() ~= valorFase() do
		pcall(function ()
			if ki() > (kiRequerido() + 10) then
				game:GetService("ReplicatedStorage").Package.Events.ta:InvokeServer()
				task.wait()
				game:GetService("ReplicatedStorage").Package.Events.AuraTrigger:InvokeServer()
			end
		end)
		wait()
	end
end

function transformarse(array)
	if strength() < 16000 then
		return
	end
	for i,v in pairs(transformaciones[array]) do
		if strength() >= v.fuerza then
			equipRemote:InvokeServer(v.name) 
			if equipRemote:InvokeServer(v.name) then 
				break 
			end
		end
	end
	ejecutarForma() 
end

function iniciarJuego()
	local player = game.Players.LocalPlayer
	local data = game.ReplicatedStorage.Datas[player.UserId]
	game:GetService("ReplicatedStorage").Package.Events.Start:InvokeServer()
	game.Players.LocalPlayer.Character.Humanoid.Health = 0
	if data.Strength.Value>=8000000 then
		wait(5)
		game:GetService("ReplicatedStorage").Package.Events.equipskill:InvokeServer("Godly SSJ2")
		game:GetService("ReplicatedStorage").Package.Events.ta:InvokeServer()
	else
		wait(4.95)
		game:GetService("ReplicatedStorage").Package.Events.equipskill:InvokeServer("Mystic")
		game:GetService("ReplicatedStorage").Package.Events.ta:InvokeServer()
	end
	task.wait()
end

function noTierraID()
	return game.placeId ~= 3311165597
end

local function valorMinimo()
	local valueMinimo = strength()

	if energy() < valueMinimo then
		valueMinimo = energy()
	end
	if defense() < valueMinimo then
		valueMinimo = defense()
	end
	if speed() < valueMinimo then
		valueMinimo = speed()
	end

	return valueMinimo
end

function detectarAtaque(name, subname, enemigo)
	local args = {
		[1] = name,
		[2] = {
			["FaceMouse"] = true,
			["MouseHit"] = enemigo
		},
		[3] = "Blacknwhite27"
	}
	game:GetService("ReplicatedStorage"):WaitForChild("Package"):WaitForChild("Events"):WaitForChild(subname):InvokeServer(unpack(args))
end



function ataqueMelee(vida) 
	for i,v in pairs(arregloAtaques) do
		if valorMinimo() > v.requerido and ki() >= kiRequerido() and vida then
			game:GetService("ReplicatedStorage").Package.Events.mel:InvokeServer(v.name, "Blacknwhite27")
		end
	end
end

function ataqueEnergy(enem, vida) 
	for i,v in pairs(ataquesEnergy) do
		pcall(function()
			if valorMinimo() > v.fuerza and vida and ki() >= kiRequerido() then
				detectarAtaque(v.name, v.subName, enem)
			end
		end)
		wait()
	end
end

function iteradorQuest(array)
	print('Seccion iterador quest')
	local enemigo
	for _,jefe in pairs(multiQuest[array]) do 
		if valorMinimo() > jefe.minimo and player() then
			print('El elegigo')
			for indice, v in ipairs(game:GetService("Workspace").Living:GetChildren()) do 
				print('enemigo '..v.Name)
				if jefe.nombre == v.Name and v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") and yo and v.Humanoid.Health > 0 then
					print('Mision seleccionada y retornando enemigo')
					return v.Name 
				end
			end
		end
	end
end

function earth()
	pcall(function()
		local A_1 = "Earth"
		local Event = game:GetService("ReplicatedStorage").Package.Events.TP
		Event:InvokeServer(A_1)
	end)
end
function mundoBills()
	game:GetService("ReplicatedStorage").Package.Events.TP:InvokeServer("Vills Planet")
end

function validacionPlanetas()
	local billsTP = 210000000

	print('Validando el planeta')

	if noTierraID() then 
		while valorMinimo() < billsTP and noTierraID() do 
			print('Ir a la tierra')
			earth()
			wait()
		end
	else 
		if valorMinimo() >= billsTP  then 
			pcall(function()
				print('Llendo a bills')
				mundoBills()
			end)
		end
	end
end

local function masFuerza()
	if strength() < statsRequeridosFarm then
		local args = {[1] = "Blacknwhite27",[2] = 1}
		game:GetService("ReplicatedStorage").Package.Events.p:FireServer(unpack(args))
		print('Ejecutando golpeo')
	else
		print('Tienes suficiente fuerza!')
	end
end
local function masEnergy()
	if energy() < statsRequeridosFarm then
		local args = {[1] = 1,[2] = true,[3] = CFrame.new(12, 12, 12)}
		game:GetService("ReplicatedStorage").Package.Events.kb:FireServer(unpack(args))
		print('Ejecutando energy!')
	else
		print('Suficiente energy!')
	end
end
local function masDefensa()
	if defense() < statsRequeridosFarm then
		local args = {[1] = "Blacknwhite27"}
		game:GetService("ReplicatedStorage").Package.Events.def:InvokeServer(unpack(args))
		print('Ejecutando energy!')
	else
		print('Suficiente energy!')
	end
end
local function masSpeed() 
	keypress(Enum.KeyCode.LeftShift)
	print('Ejecutando Speed!')
end
local function cancelarSpeed() 
	keyrelease(Enum.KeyCode.LeftShift)
	print('Cancelando Speed!')
end
local function masCarga() 
	keypress(Enum.KeyCode.C)
	print('Carga!')
end
local function cancelarCarga() 
	keyrelease(Enum.KeyCode.C)
	print('Cancelando Carga!')
end

local function fly()
	local succes,fallo = pcall(function ()
		keypress(Enum.KeyCode.Space)
		task.wait()
		keyrelease(Enum.KeyCode.Space)
		task.wait()
		keypress(Enum.KeyCode.Space)
		task.wait()
		keyrelease(Enum.KeyCode.Space)
		task.wait()
	end)
	if fallo then
		warn('fly error '..fallo)
	end
end

local function ataquesParaStats()
	print('Atacando...')
	
	if speed() < statsRequeridosFarm and ki() >= kiRequerido() and not activadaSpeed and player() then
		masSpeed() 
		activadaSpeed = true
	end

    if (speed() >= statsRequeridosFarm and activadaSpeed) or (ki() < kiRequerido() and activadaSpeed) or (not player() and activadaSpeed) then
		cancelarSpeed() 
		cancelarSpeed() 
		activadaSpeed = false
	end

	masFuerza()
	task.wait()
	masEnergy()
	task.wait()
	masDefensa()
	task.wait()
end

local function aver(enlace)
    return loadstring(game:HttpGet(enlace))()
end

local function flyi()
	aver('https://raw.githubusercontent.com/CBJ-Yael/volarFly/main/validarFly.lua')
end

local function esperandoCargaxd()

	if (speed() >= statsRequeridosFarm and activadaSpeed) or (ki() < kiRequerido() and activadaSpeed) or (not player() and activadaSpeed) then
		cancelarSpeed() 
		cancelarSpeed() 
		activadaSpeed = false
	end

	masCarga() 
	repeat
		wait()
		warn('Esperando mas ki')
	until ki() >= kiTotal() or not player()
	warn('Ki completado o estas muerto!')
	task.wait()
	cancelarCarga()
	cancelarCarga()
end

local function acumularStats()
	repeat
		wait()
		print('Esperando vida....')
	until player() 
	task.wait()

	while valorMinimo() < statsRequeridosFarm do
		
		cargaAndBloqueo = false

		print('Tienes pocas estadisticas')

		
		if ki() >= kiRequerido() then
			ataquesParaStats()
		else
			esperandoCargaxd()
		end
	end
	print('Tienes estadisticas suficientes!')
	cargaAndBloqueo = true
end

local function validacionVida()
	aver('https://raw.githubusercontent.com/CBJ-Yael/holasaludos/main/saludos.lua')
end

function empezarQuest(array) 
	acumularStats() 
	task.wait()

	validacionPlanetas()

	local enemigo = iteradorQuest(array)

	print('Enemigo seleccionado')

	while misionSeleccionada() ~= enemigo and player() do
		wait()
		print('Ejecutando quest')
		events.Qaction:InvokeServer(game:GetService("Workspace").Others.NPCs[enemigo])
	end
end

function rival(array)
	local enemigo = iteradorQuest(array)

	for indice, v in ipairs(game:GetService("Workspace").Living:GetChildren()) do
		if enemigo == v.Name then
			return v
		end
	end
end

function mision()
	print('Seleccionando mision')
	if noTierraID() then
		print('Estas en bills')
		empezarQuest('bossBills')
	else
		print('Estas en la tierra')
		empezarQuest('bossEarth')
	end
end

function misionRival()
	local buscador

	if noTierraID() then
		buscador = rival('bossBills')
	else
		buscador = rival('bossEarth')
	end

	return buscador
end

function empezarFarm() 
	fly()
	while true do
		pcall(function()
			if player() then
				rebirth() 

				warn('estadisticas elegidas '..tostring(statsRequeridosFarm))

				transformarse('fases')

				print('Tranformacion ejecutada')
				mision()

				print('Mision seleccionada')

				local enemigo = misionRival()

				statsPlayerFarmSa = flyi

				print('Enemigo: '..enemigo.Name)

				local function frameEnemigo()
					return enemigo.HumanoidRootPart.CFrame
				end
				pcall(function ()
					validacionVida()
				end)
				local function vidaEnemigo()
					return enemigo.Humanoid.Health > 0
				end

				while enemigo:FindFirstChild("Humanoid") and vidaEnemigo() and player() do
					pcall(function()
						spawn(function() 
							sigueEnemigo(frameEnemigo() * CFrame.new(0, 0, 2))
							pcall(function ()
								statsPlayerFarmSa()
							end)
						end)
						spawn(function() 
							if ki() >= kiRequerido() and valorMinimo() >= 4000 then
								ataqueEnergy(frameEnemigo(), vidaEnemigo())
								wait(1)
							else
								game:GetService("ReplicatedStorage").Package.Events.p:FireServer("Blacknwhite27", 1)
							end
						end)
						spawn(function()
							if ki() >= kiRequerido() and valorMinimo() >= 2000 then
								ataqueMelee(vidaEnemigo())
							end
						end)
						spawn(function()
							if selectedForm() ~= valorFase() or selectedForm() == '' or valorFase() == '' then
                                transformarse('fases');
							end
						end)
					end)
					wait()
				end
				if misionSeleccionada() == '' then
					wait(2)
				end
				if yo.Character.Humanoid.Health <= 0 then
					repeat
						wait()
					until yo.Character.Humanoid.Health > 0
					wait(1)
					fly()
				end
			end
		end)
		wait()
	end
end


print('Loading game VERSION ACTUALIZADA 5.0.0'..' XD puto el que este viendo esto y me este ofendiendo el hijo de perra, bien que usas mi script verdad pedazo de mierda?')
wait(7)

yo.Idled:Connect(function() 
	afk:CaptureController()
	afk:ClickButton2(Vector2.new())
end)

iniciarJuego()
task.wait()

spawn(function()
	while true do
		if cargaAndBloqueo then
			pcall(function()
				spawn(function()
					local args = {[1] = "Blacknwhite27"}
					game:GetService("ReplicatedStorage").Package.Events.cha:InvokeServer(unpack(args))
				end)
	
				spawn(function()
					local args = {[1] = true}
					game:GetService("ReplicatedStorage").Package.Events.block:InvokeServer(unpack(args))
				end)
			end)
		end
		wait()
	end
end)
task.wait()

empezarFarm()
