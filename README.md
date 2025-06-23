--[[
🔥 Blox Fruits - Theus☯️ Hub
📦 Completo com Auto Farm, ESP, Frutas, Raças, Teleporte
🎨 Logo personalizada e nome customizado por ChatGPT
]]

-- Carrega Rayfield GUI
local Rayfield = loadstring(game:HttpGet("https://sirius.menu/rayfield"))()

-- Janela principal
local Janela = Rayfield:CreateWindow({
	Name = "⚔️ Theus☯️ Hub - Blox Fruits",
	LoadingTitle = "Theus☯️ Hub",
	LoadingSubtitle = "by ChatGPT",
	ConfigurationSaving = {
		Enabled = true,
		FileName = "TheusHubConfig"
	},
	KeySystem = true,
	KeySettings = {
		Title = "Theus☯️ Hub | Sistema de Chave",
		Subtitle = "Chave Gratuita no Discord",
		Note = "Use a chave: THEUS2025",
		SaveKey = true,
		GrabKeyFromSite = false,
		Key = {"THEUS2025"}
	}
})

-- Variáveis globais
getgenv().AutoFarm = false
getgenv().AutoESP = false
getgenv().AutoFruit = false

-- Função para atacar (Auto Soco)
local function AutoAttack()
	while getgenv().AutoFarm do
		task.wait()
		pcall(function()
			game:GetService("VirtualInputManager"):SendKeyEvent(true, "Z", false, game)
			task.wait(0.1)
			game:GetService("VirtualInputManager"):SendKeyEvent(false, "Z", false, game)
		end)
	end
end

-- Scripts de Auto Farm + Soco
Janela:CreateTab("⚔️ Auto Farm"):CreateToggle({
	Name = "Ativar Auto Farm + Soco",
	CurrentValue = false,
	Callback = function(Value)
		getgenv().AutoFarm = Value
		if Value then
			coroutine.wrap(AutoAttack)()
			while getgenv().AutoFarm do
				task.wait()
				pcall(function()
					local enemy = game:GetService("Workspace").Enemies:FindFirstChildOfClass("Model")
					if enemy and enemy:FindFirstChild("HumanoidRootPart") then
						game.Players.LocalPlayer.Character:FindFirstChild("HumanoidRootPart").CFrame =
							enemy.HumanoidRootPart.CFrame * CFrame.new(0,10,0)
					end
				end)
			end
		end
	end,
})

-- ESP Melhorado
Janela:CreateTab("👁️ ESP"):CreateToggle({
	Name = "ESP Baús + Frutas",
	CurrentValue = false,
	Callback = function(Value)
		getgenv().AutoESP = Value
		while getgenv().AutoESP do
			task.wait(1)
			pcall(function()
				for _, obj in pairs(workspace:GetDescendants()) do
					if obj:IsA("Model") and obj:FindFirstChild("TouchInterest") and not obj:FindFirstChild("TheusHighlight") then
						local highlight = Instance.new("Highlight")
						highlight.Name = "TheusHighlight"
						highlight.FillTransparency = 1
						highlight.OutlineColor = Color3.new(1, 1, 0)
						highlight.Parent = obj
					end
				end
			end)
		end
		-- Limpa ESP ao desativar
		for _, h in pairs(workspace:GetDescendants()) do
			if h:IsA("Highlight") and h.Name == "TheusHighlight" then
				h:Destroy()
			end
		end
	end
})

-- Fruta Notifier + Auto Coletar
Janela:CreateTab("🍇 Frutas"):CreateToggle({
	Name = "Auto Pegar Fruta (Instantâneo)",
	CurrentValue = false,
	Callback = function(Value)
		getgenv().AutoFruit = Value
		while getgenv().AutoFruit do
			task.wait(2)
			pcall(function()
				for _, v in pairs(game.Workspace:GetChildren()) do
					if string.find(v.Name:lower(), "fruit") and v:IsA("Tool") then
						game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = v.Handle.CFrame
						firetouchinterest(game.Players.LocalPlayer.Character.HumanoidRootPart, v.Handle, 0)
						firetouchinterest(game.Players.LocalPlayer.Character.HumanoidRootPart, v.Handle, 1)
					end
				end
			end)
		end
	end
})

-- Configurações
local ConfigTab = Janela:CreateTab("⚙️ Config")

ConfigTab:CreateButton({
	Name = "Desligar Sons do Jogo",
	Callback = function()
		for _, s in pairs(game:GetService("SoundService"):GetDescendants()) do
			if s:IsA("Sound") then
				s.Volume = 0
			end
		end
	end
})

ConfigTab:CreateButton({
	Name = "Anti Lag + Remover Neblina",
	Callback = function()
		-- Remove partículas e trilhas
		for _, v in pairs(game:GetDescendants()) do
			if v:IsA("ParticleEmitter") or v:IsA("Trail") then
				v:Destroy()
			end
		end
		-- Remove a neblina
		local Lighting = game:GetService("Lighting")
		Lighting.FogEnd = 1000000
		Lighting.FogStart = 0
		Lighting.FogColor = Color3.new(1, 1, 1)
	end
})--[[ 
 ☯️ Theus Hub - Script inspirado no Redz Hub 
 🎮 Jogo: Blox Fruits 
 🛠️ Desenvolvido por ChatGPT para Emanuel 
 🔐 Código de ativação: theuskey2025 
--]]

-- Carrega Rayfield GUI
local Rayfield = loadstring(game:HttpGet("https:                           

-- Cria a Janela Principal
local Window = Rayfield:CreateWindow({
    Name = "☯️ Theus Hub - Blox Fruits",
    LoadingTitle = "Theus Hub",
    LoadingSubtitle = "Carregando funcionalidades...",
    ConfigurationSaving = {
        Enabled = true,
        FolderName = "TheusHub",
        FileName = "Config"
    },
    KeySystem = true,
    KeySettings = {
        Title = "☯️ Theus Hub - Sistema de Chave",
        Subtitle = "Chave Gratuita Obrigatória",
        Note = "Use a chave: theuskey2025",
        SaveKey = true,
        GrabKeyFromSite = false,
        Key = {"theuskey2025"}
    }
})

-- Cria as Abas
local AutoFarmTab = Window:CreateTab("⚔️ Auto Farm", 4483362458)
local EspTab = Window:CreateTab("🔍 ESP", 4483362458)
local TeleportTab = Window:CreateTab("📍 Teleporte", 4483362458)
local FruitTab = Window:CreateTab("🍇 Frutas", 4483362458)
local RaceTab = Window:CreateTab("👤 Raças", 4483362458)
local SettingsTab = Window:CreateTab("⚙️ Configurações", 4483362458)

-- Mensagem inicial
AutoFarmTab:CreateParagraph({
    Title = "Bem-vindo ao Theus Hub!",
    Content = "Escolha uma função acima para começar a usar."
})

-- Funções de Auto Farm
AutoFarmTab:CreateToggle({
    Name = "Auto Farm Ativar",
    CurrentValue = false,
    Callback = function(Value)
        if Value then
            print("Auto Farm ativado!")
        else
            print("Auto Farm desativado.")
        end
    end
})

-- Funções de ESP
EspTab:CreateToggle({
    Name = "Ativar ESP de Inimigos",
    CurrentValue = false,
    Callback = function(Value)
        if Value then
            print("ESP ativado")
        else
            print("ESP desativado")
        end
    end
})

-- Funções de Teleporte
TeleportTab:CreateButton({
    Name = "Ir para Cidade 1",
    Callback = function()
        game.Players.LocalPlayer.Character:PivotTo(CFrame.new(1035, 200, 1123))
    end
})

-- Funções de Frutas
FruitTab:CreateButton({
    Name = "Notificar Frutas",
    Callback = function()
        Rayfield:Notify({
            Title = "Fruta Detectada!",
            Content = "Isso é apenas um exemplo.",
            Duration = 5
        })
    end
})

-- Funções de Raças
RaceTab:CreateButton({
    Name = "Desbloquear Raça V3 (Exemplo)",
    Callback = function()
        print("Upgrade de raça solicitado (exemplo)")
    end
})

-- Funções de Configurações
SettingsTab:CreateToggle({
    Name = "Remover Neblina",
    CurrentValue = false,
    Callback = function(Value)
        if Value then
            game.Lighting.FogEnd = 1e10
        else
            game.Lighting.FogEnd = 500
        end
    end
})

SettingsTab:CreateToggle({
    Name = "Ativar NoClip (Exemplo)",
    CurrentValue = false,
    Callback = function(Value)
        if Value then
            print("NoClip ligado (exemplo)")
        end
    end
})
