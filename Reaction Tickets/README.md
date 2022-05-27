# Reaction Tickets
This is just a super simple "click the reaction to open a ticket" custom command for YAGPDB. Its designed to give you different ticket "types" (differentiated by the ticket channel's title), and generally just make life a little bit easier.

This CC will automatically reset the reaction counter to 1 so members don't know how many tickets have been created, or by who.

## Instructions
1) Make sure you have YAGPDB's ticket system enabled and configured to your liking. This CC works in tandem with it.
2) Create your message where people will click on the reaction, and add the reactions (this CC will not add the initial reactions for you).
3) Set up your CC. The trigger type should be "Reactions" and the trigger should be "added reactions only".
4) Edit things accordingly.
5) Save, and you're done!

I'd also considering replacing the default new ticket message in YAGPDB's ticket system with `{{/* */}}` (a blank comment), as this also includes a custom message field for each ticket type. Or just leave the basic instructions on how to add people and close the ticket. Up to you.

## Adding More Ticket Types
This CC can be expanded right up until you hit YAGPDB's character limit for custom commands, meaning you can have a number of different ticket types. In order to do so, you simply need to duplicate the codes below, and change the A in all instances of **embedA**, **emojiA**, and **titleA** to C, D, E, etc.
```{{ $embedA := cembed "title" "EMBED TITLE" "description" "EMBED DESCRIPTION" }}
{{ $emojiA := " " }}
{{ $titleA := " " }}```
and 
```{{if and (eq .Message.ID $msgID) (eq .Reaction.Emoji.Name $emojiA)}}
    {{$stfu := createTicket .User.ID $titleA}}
    {{sleep 1}}
    {{sendMessage $stfu.ChannelID $embedA}}
    {{addMessageReactions nil .Reaction.MessageID $emojiA}}
    {{deleteMessageReaction nil .Reaction.MessageID .Reaction.UserID .Reaction.Emoji.Name}}
{{end}}```
