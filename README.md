# ZendeskMassPhotoUpdater
A python script that lets you mass update the profile pictures for zendesk agents who belong to a group. My company just went through a rebrand and we have multiple brands in the company that share one instance. All agents groups for a specific brand have the same photo so this let me quickly update them.

This should work on a Mac assuming you save the script and the image you want (80px by 80px) on your desktop

Throw in your zendesk brand name, email, and token that you generated in Zendesk Admin in lines 6,7, and 8. Find and replace all "unique_string" mentions in the code with the unique word you have in the Zendesk Agent Groups you want to update the photo for. Make sure to set the image path on line 14 to wherever you saved the new logo file on your mac.
