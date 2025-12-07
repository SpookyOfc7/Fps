-- FPS BOOST / REMOVE SHADOW / GRAPHICS LOW

local settings = settings
local lighting = game:GetService("Lighting")

-- Remover sombras
lighting.GlobalShadows = false
lighting.FogEnd = 100000
lighting.Brightness = 1

-- Apagar reflexos e efeitos desnecessários
for i,v in pairs(lighting:GetChildren()) do
    if v:IsA("BloomEffect") or v:IsA("BlurEffect") or v:IsA("ColorCorrectionEffect") 
    or v:IsA("SunRaysEffect") or v:IsA("DepthOfFieldEffect") then
        v.Enabled = false
    end
end

-- Texturas mais leves
for _, obj in pairs(workspace:GetDescendants()) do
    if obj:IsA("Part") or obj:IsA("UnionOperation") or obj:IsA("MeshPart") then
        obj.Material = Enum.Material.Plastic -- Gráfico "massinha"
        obj.Reflectance = 0
    end
end

-- Aumentar desempenho gráfico
settings().Rendering.QualityLevel = Enum.QualityLevel.Level01
settings().Rendering.MeshPartDetailLevel = Enum.MeshPartDetailLevel.Low

print("✔ Otimizado! FPS deve aumentar")
