# renameFLExMedia
Media sources recorded in TheCombine, FLEx itself and WeSay use GUIDs for filenames. This can be problematic when searching for media files in the file manager.
This set of scripts renames the files and the associated links in the fwdata file according to a user-specified convention.
The user can specify to use a custom field or a standard Fieldworks field (e.g. sensegloss) or combination thereof as the basis for renaming the sound file.

- getCurrentFilesNames.ps1 retrieves current filenames in the LinkedFiles directory (generates an xml file)
- checkUniqueFileNames.xsl first ensures that filenames are unique according to the selected field (or combination of fields) and that existing filesnames do not interfere. It also generates a report for any problematic soundfileNames that should be changed before running changeFileLinks.xsl
- changeFileNamesAndLinks.ps1 - runs the following
- - changeFileLinks.xsl changes fwdata to new filename links.
  - generateRenameList.xsl creates a tab-delimited file that includes two columns: originalFileName, targetFileName
  - the above tab-delimited file is used by powershell to change all the listed filenames.

Parameters: pFileNameField - the custom field or standard Fieldworks field (e.g. sensegloss) or combination thereof as the basis for renaming the sound file.

Current assumptions:
1. Can work with AudioWritingSystems on LexemeForm, CitationForm, and ExampleSentences. Currently ignores Pronunciation media files as these are done differently, not using GUIDs and do not support audiowriting systems (I think).
2. One soundfile per object per field.
