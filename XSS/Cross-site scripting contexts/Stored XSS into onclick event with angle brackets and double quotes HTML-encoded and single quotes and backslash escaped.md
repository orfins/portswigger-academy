I took the example code:

`&apos;-alert(document.domain)-&apos;`

and modified it to contain an acceptable website address, and made the call to `alert` empty:

`http://a.com&apos;-alert(document.domain)-&apos;`

Please note: the hyphens (`-`) are there as string operators. `+` would do the job as well. 