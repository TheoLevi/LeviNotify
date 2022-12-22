Hi, thank you for buying my script, I'm very grateful!

To display a notification you should call it like below:

<!-- Just Do This -->


<!-- Go to qb-core/client/functions.lua and find QBCore.Functions.Notify and replace that with code 1 -->

Code 1
if QBCore.Config.leviNotify == true then
    function QBCore.Functions.Notify(text, textype, length)
        if type(text) == "table" then
            local ttext = text.text or 'Placeholder'
            local caption = text.caption or 'Placeholder'
            local ttype = textype or 'info'
            local length = length or 8500
            exports['leviNotify']:Alert(ttext, caption, length, ttype)
        else
            local ttype = textype or 'info'
            local length = length or 8500
            exports['leviNotify']:Alert(text, "", length, ttype)
        end
    end 
else
    function QBCore.Functions.Notify(text, texttype, length)
        if type(text) == "table" then
            local ttext = text.text or 'Placeholder'
            local caption = text.caption or 'Placeholder'
            texttype = texttype or 'primary'
            length = length or 5000
            SendNUIMessage({
                action = 'notify',
                type = texttype,
                length = length,
                text = ttext,
                caption = caption
            })
        else
            texttype = texttype or 'primary'
            length = length or 5000
            SendNUIMessage({
                action = 'notify',
                type = texttype,
                length = length,
                text = text
            })
        end
    end
end



 <!-- Next go to your qb-core config and add this  -->

 
QBConfig.leviNotify = true



<!-- For Custom Notification -->


# Client side

exports['leviNotify']:Alert("Title", "Message", Time, 'type')

# Server side

TriggerClientEvent('leviNotify:Alert', source, "Title", "Message", Time, 'type')


[Time] - 1000 = 1 second | 5000 = 5 seconds

Types: 
	- success (green)
	- info (blue)
	- warning (yellow)
	- error (red)
	- phone (orange)
	- neutral (grey)