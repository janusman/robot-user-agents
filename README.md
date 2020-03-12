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

Example usages from the bash commandline:

* Fetch `bad-list.txt` and convert list into a regular expression:

```
$ curl -s https://raw.githubusercontent.com/janusman/robot-user-agents/master/bad-list.txt |paste -d'|' -s
```

* Live-tail an apache `access.log` file and highlight User Agents from the `bad-list.txt`:

```
$ regex=`curl -s https://raw.githubusercontent.com/janusman/robot-user-agents/master/bad-list.txt |paste -d'|' -s`; tail -f access.log |egrep --color "$regex|^"
```

* From the last 1000 lines of the access.log, count requests only from the User Agents from `all-list.txt`:

```
$ lines=1000; regex=`curl -s https://raw.githubusercontent.com/janusman/robot-user-agents/master/all-list.txt |paste -d'|' -s`; tail -${lines} access.log |egrep -o "$regex" |sort |uniq -c |sort -nr |head
    106 Siteimprove.com
     80 bingbot
     19 SemrushBot
      7 Ahrefs
      5 YandexBot
      5 Baiduspider
      2 trendictionbot
      1 DotBot
```
