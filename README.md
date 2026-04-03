-- สคริปวิ่งเร็วสำหรับ Delta Executor
-- วางแล้วกด Execute ได้เลย

local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humanoid = character:WaitForChild("Humanoid")

-- ตั้งค่าความเร็ว (ปรับได้ตามชอบ)
local speedValue = 100  -- ปรับเลขตรงนี้ เช่น 200, 300, 500 ยิ่งสูงยิ่งเร็ว

-- ฟังก์ชันอัพเดทความเร็ว
local function updateSpeed()
    if humanoid then
        humanoid.WalkSpeed = speedValue
    end
end

-- เรียกใช้ทันที
updateSpeed()

-- ถ้าตัวละครรีสปอว์นใหม่ จะอัพเดทความเร็วให้อัตโนมัติ
player.CharacterAdded:Connect(function(newChar)
    character = newChar
    humanoid = newChar:WaitForChild("Humanoid")
    updateSpeed()
end)

-- ทำให้เร็วแบบต่อเนื่อง (กันบางเกมรีเซ็ตความเร็ว)
game:GetService("RunService").Heartbeat:Connect(function()
    if humanoid and humanoid.WalkSpeed \~= speedValue then
        humanoid.WalkSpeed = speedValue
    end
end)

print("✅ สคริปวิ่งเร็วเปิดใช้งานแล้ว! ความเร็ว = " .. speedValue)
