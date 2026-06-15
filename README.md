-- Script Local de Gigante (FE Visual)
-- Funciona alterando as propriedades de escala do Humanoid apenas para o seu cliente

local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer

-- Defina a escala do seu gigante aqui (1 é o normal, 5 é cinco vezes maior)
local MultiplicadorEscala = 5 

local function TornarGigante(character)
    local humanoid = character:WaitForChild("Humanoid")
    
    -- Espera os valores de escala padrão do Roblox carregarem
    local bodyHeight = humanoid:WaitForChild("BodyHeightScale", 3)
    local bodyWidth = humanoid:WaitForChild("BodyWidthScale", 3)
    local bodyDepth = humanoid:WaitForChild("BodyDepthScale", 3)
    local headScale = humanoid:WaitForChild("HeadScale", 3)
    
    -- Altera visualmente o tamanho do corpo
    if bodyHeight then bodyHeight.Value = MultiplicadorEscala end
    if bodyWidth then bodyWidth.Value = MultiplicadorEscala end
    if bodyDepth then bodyDepth.Value = MultiplicadorEscala end
    if headScale then headScale.Value = MultiplicadorEscala end
    
    -- Ajusta a velocidade e o pulo para combinarem com o tamanho (opcional)
    humanoid.WalkSpeed = 16 * (MultiplicadorEscala * 0.6)
    humanoid.JumpPower = 50 * (MultiplicadorEscala * 0.4)
    
    -- Ajusta a câmera para não ficar dentro do seu pé
    local camera = workspace.CurrentCamera
    camera.CameraSubject = humanoid
end

-- Executa se o personagem já existir
if LocalPlayer.Character then
    TornarGigante(LocalPlayer.Character)
end

-- Executa sempre que você renascer
LocalPlayer.CharacterAdded:Connect(TornarGigante)
