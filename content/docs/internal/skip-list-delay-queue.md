+++
date = "2016-01-01T12:22:13+05:30"
draft = false
title = "Skip List based Delay Queue"

+++


[date:64bit:Int]

- Delay Queue will have a separate meta file.

- Delay Queue will be fragmented date wise

	````
		for ex:
			2016-10-25.Qname.dly
			2016-10-26.Qname.dly
	````

- There will be a Reader process that will pop elements from the Delay Queue

- If the last element is NULL and the Current date is greater than the one stored in the Metafile
	- Update the date in the Meta file, 
	- create the new date fragment if not exists, 
	- Move the Reader Process to the new fragment/file,
	- Delete the old fragment.

