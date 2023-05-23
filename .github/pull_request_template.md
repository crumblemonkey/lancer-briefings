Are you adding a new pilot?
- In the public/pilot directory add a bio text file ([callsign].md) and image ([callsign].png)
- In the public/mechs directory add a mech image ([mechname].png)
- In the src directory update App.vue by coppying and pasting one of the list of pilots (starts line 117) and update the properties. **Callsign/frame must match the filename used for pilot/mech!**

Are you adding a new mission?
- Check exisiting public/mission and public/events files for structure (very simple)
- In public/missions add a new text file with the mission outline and goals ([mission number].md)
- In public/events create a (possibly empty) text file with any other relevant details ([mission number].md)
- In the src directory update App.vue by copying and pasting one of the mission and adding to the bottom of the list (starts line 95). **slug must match the mission number in the file name!** Status can be start, partial-success, success, or failure.
- To make the mission show loaded when the page is loaded set the mission_slug and current_md starting line 92

You may also want to update the header section starting line 167 to keep us up to date.

**If you've edited a file update the line numbers above in .github/pull_request_template.md**

**Delete all the above text before submitting!!**
