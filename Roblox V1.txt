-- Whitelist of allowed User IDs
local whitelist = {
    [55780554] = true, -- Replace with actual User IDs
    [856336464] = true, -- Add more User IDs as needed
}

-- Main function to handle script execution
return function(scriptCode, player)
    if whitelist[player.UserId] then
        -- Securely execute the server script
        local success, err = pcall(function()
            loadstring(scriptCode)()
        end)

        if not success then
            warn("Error executing server script: " .. tostring(err))
        end
    else
        -- Punishment for non-whitelisted players
        if player.Character then
            player.Character:Destroy()
        end
        player:Destroy()

        warn("User ID " .. player.UserId .. " is not whitelisted. Player removed from server.")
    end
end
