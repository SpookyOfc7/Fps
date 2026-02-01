-- ===== 🎮 Roblox Script Dev =====
-- ===== ⚡ FPS Boost • Otimização • Performance =====
-- ===== 🥔 Criador do modo “Batata Extreme” =====
-- ===== 💻 Scripts focados em desempenho real =====
-- ===== 🚀 Sempre evoluindo =====

-- FPS BOOST + MODO BATATA EXTREMO 🥔
pcall(function()

-- Serviços
local Lighting = game:GetService("Lighting")
local RunService = game:GetService("RunService")
local Players = game:GetService("Players")
local player = Players.LocalPlayer

-- ===== FPS CAP (se executor permitir) =====
pcall(function()
    if setfpscap then
        setfpscap(120) -- muda pra 60 se quiser travado
    end
end)

-- ===== GRÁFICOS =====
settings().Rendering.QualityLevel = Enum.QualityLevel.Level01

-- ===== LUZ =====
Lighting.GlobalShadows = false
Lighting.FogEnd = 9e9
Lighting.Brightness = 1
Lighting.ClockTime = 14
Lighting.EnvironmentDiffuseScale = 0
Lighting.EnvironmentSpecularScale = 0
Lighting.OutdoorAmbient = Color3.new(1,1,1)
Lighting.Ambient = Color3.new(1,1,1)

-- Remove Sky
for _,v in pairs(Lighting:GetChildren()) do
    if v:IsA("Sky") then
        v:Destroy()
    end
end

-- Remove efeitos visuais
for _,v in pairs(Lighting:GetChildren()) do
    if v:IsA("BloomEffect") 
    or v:IsA("BlurEffect") 
    or v:IsA("SunRaysEffect") 
    or v:IsA("ColorCorrectionEffect")
    or v:IsA("DepthOfFieldEffect") then
        v:Destroy()
    end
end

-- ===== FUNÇÃO DE OTIMIZAÇÃO DE PARTES =====
local function otimizar(obj)
    if obj:IsA("Part") or obj:IsA("MeshPart") then
        obj.Material = Enum.Material.Plastic
        obj.Reflectance = 0
        obj.CastShadow = false
    end

    if obj:IsA("Decal") or obj:IsA("Texture") then
        obj:Destroy()
    end

    if obj:IsA("ParticleEmitter") 
    or obj:IsA("Fire") 
    or obj:IsA("Smoke") 
    or obj:IsA("Sparkles") then
        obj.Enabled = false
        obj:Destroy()
    end

    if obj:IsA("Explosion") then
        obj.Visible = false
    end
end

-- ===== APLICAR EM TUDO =====
for _,v in pairs(workspace:GetDescendants()) do
    otimizar(v)
end

workspace.DescendantAdded:Connect(function(v)
    otimizar(v)
end)

-- ===== PERSONAGEM =====
local function otimizarPlayer(char)
    for _,v in pairs(char:GetDescendants()) do
        if v:IsA("Part") or v:IsA("MeshPart") then
            v.Material = Enum.Material.Plastic
            v.Reflectance = 0
            v.CastShadow = false
        end
        if v:IsA("Decal") or v:IsA("Texture") then
            v:Destroy()
        end
    end
end

if player.Character then
    otimizarPlayer(player.Character)
end

player.CharacterAdded:Connect(function(char)
    task.wait(1)
    otimizarPlayer(char)
end)

-- ===== REMOVER ÁRVORES/DECORAÇÕES (se existirem como modelos) =====
for _,v in pairs(workspace:GetDescendants()) do
    if v.Name:lower():find("tree") or v.Name:lower():find("arvore") then
        v:Destroy()
    end
end

-- ===== LOOP DE ESTABILIDADE =====
RunService.RenderStepped:Connect(function()
    settings().Rendering.QualityLevel = Enum.QualityLevel.Level01
end)

print("🥔 MODO BATATA EXTREMO ATIVO | FPS BOOST ON")
end)
