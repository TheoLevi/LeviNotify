# Preview :
![image](https://media.discordapp.net/attachments/738159425721991250/1053070080197537792/image.png?width=1202&height=676)

To display a notification you should call it like below:

Go to qb-core/client/functions.lua and find QBCore.Functions.Notify and replace that with this.

```Code 1
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
