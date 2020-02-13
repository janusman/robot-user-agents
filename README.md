# robot-user-agents

An opinionated list of strings that match HTTP User Agents whose traffic is usually/mostly not human-initiated.

* all-list.txt
  * Strings that identify User Agents that are *commonly* robots (and not human visitors). 
  * This list may mark some legitimate User Agents as robots. Example `OPPO A33` User Agents do not advertise as robots but have plainly exhibited robot behavior.
  * This list includes some `Microsoft *` User Agents whose requests may still originate from human interaction (say, like opening up an e-mail in Microsoft Outlook), but are still included here since many requests could be related to non-human interaction.
* bad-list.txt
  * A subset of the `all-list.txt` file which flags those User Agents which have been observed to do "Bad things"
  * The "Bad things" include: disregard for `robots.txt` directives, very aggressive crawling rates.
  * Some User Agents here do not advertise as robots, but plainly exhibit robot behavior.

Example usages:

* Convert list into a regular expression:

```
$ paste -d'|' -s all-list.txt 
```
