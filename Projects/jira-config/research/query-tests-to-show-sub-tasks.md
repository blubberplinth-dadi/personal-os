# JQL þar sem ég var að reyna að fá Sub-tösk inn á borðið þó þau séu ekki í status sem fylgir einum af dálkunum á Þróunarborði. Vildi sjá spjaldið undir sögunni en sama hvað ég (og Claude) reyni þá tekst það ekki

## Bót, ekki Epics, Sögur/Böggar í eftirtöldum stöðum EÐA Sub-task (óháð stöðu). Sýnir subtask í Search for Issues í Jira en ekki þegar notað er sem Board filter
project = Insurances 
AND Teymi = "Bót"
AND issuetype != Epic 
AND ((issuetype IN (Story, Bug) and status IN ("Next In", "In Progress", "In code review", "In internal QA", "Waiting for shipping", "Done")) OR issuetype = Sub-task ) 
ORDER BY Rank

## Þessi sub-filter hefði svo átt að sjá til þess að Subtöskin kæmu ekki sem spjöld við hlið Story/Bug
(fixVersion in unreleasedVersions() OR fixVersion is EMPTY) AND issuetype != Sub-task 

