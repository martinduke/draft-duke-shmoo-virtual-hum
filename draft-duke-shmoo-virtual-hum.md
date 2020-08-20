---
title: "Specification for a virtual humming tool"
abbrev: VirtualHum
docname: draft-duke-shmoo-virtual-hum-00
date: {DATE}
category: info
ipr: trust200902
area: General
workgroup: SHMOO

stand_alone: yes
pi: [toc, sortrefs, symrefs, docmapping]


author:
  -
    ins: M. Duke
    name: Martin Duke
    org: F5 Networks, Inc
    email: martin.h.duke@gmail.com


informative:

  SURVEY:
    title: "IETF 107 Survey"
    target: https://www.ietf.org/media/documents/survey-planning-possible-online-meetings-responses.pdf
    date: 2020

  VIOLINS:
    title: "Acoustics FAQ"
    target: https://newt.phys.unsw.edu.au/jw/musFAQ.html#extraviolin
    date: 2015


--- abstract


This is the specification for a virtual humming tool to emulate as closely as possible the audible hums used in-person meetings to help judge consensus. This specification is based on feedback provided in the survey about virtual humming as well as lived experience with in-person hums.  


--- middle


# Introduction


This is the specification for a virtual humming tool to emulate as closely as possible the audible hums used in-person meetings to help judge consensus. This specification is based on feedback provided in the survey {{SURVEY}} about virtual humming, as well as lived experience with in-person hums.  This note does not consider whether a better mechanism can be developed for judging consensus in online meetings rather than replicating an in-person hum.


# Key attributes of in-person humming


This specification aims to preserve the following attributes of in-person humming:


1. Participants can hum at different intensities.
2. A hum is only ever about one view, such as “agree” or “disagree”, not both. There is no way of differentiating between people humming at the same time for different things.
3. Hums often come in sets of two, but not always.
4. Participants can hear the overall hum, but the identification of the hum of any individual is unintentional and not to be encouraged.
5. The chair will generally assess the overall hum relative to the number of people in the room.
6. While the intensity of the overall hum is theoretically on a continuous scale, in practice Chairs only recognise a limited number of intensities of overall hum.
7. The overall loudness of a hum is governed by the physics of sound, most closely mapped to that of simple musical instruments {{VIOLINS}}.
8. It gets increasingly difficult to differentiate between hums as the number of people humming increases, with a practical limit reached at some point.
9. The larger the number of participants in a session, the more likely it is that there will be some who do not understand the subject matter well enough to participate in a hum. 


# Tool specification


This specification is intended to be feature complete, which means that what should be implemented is only what is explicitly stated here and nothing else.


## General


* There is only one type of hum
* Only one hum can be open at any one time in a session.


## Opening and closing hums


* A session chair can open a hum.
* A session chair can open a hum at any time during a session, except when a hum is already open.
* A session chair can open multiple hums per session.
* A hum is automatically closed 20 seconds after it is open.


## Taking part in a hum


* When a hum is open, each participant in the session, except the chairs, may take part in the hum through the following mechanism: 
1. Each session participant is presented with the following options from which they can select.  No option is selected as a default.
      1. "Soft (single)"
      2. "Loud (double)"
2. Selection of an option requires a confirmation action and only takes effect when confirmed.
3. Once an option has been chosen and confirmed then it cannot be changed.
* When a participant selects and confirms any option, they are considered to have hummed. 
* If a participant joins the session during the hum then they can take part.
* If a participant leaves the session during the hum, they are considered to have hummed and their hum is still used for data calculation.
* A timer is shown during the hum to all participants and chairs.


## After the hum


* When a hum is closed a score ***s*** calculated as the sum of:
      1. 1 for each Soft hum
      2. 2 for each Loud hum
* A hum indicator is then displayed as follows depending on the value of ***s*** and the following buckets:
   1. ***s*** ≤ 2:                                        niente 
   2. ***s*** > 2 and ***s*** ≤ 10:                pianissimo
   3. ***s*** > 10 and ***s*** ≤ 26:        piano
   4. ***s*** > 26 and ***s*** ≤ 58:        forte
   5. ***s*** > 58:                                         fortissimo
* The hum indicator is displayed to all MeetEcho participants, not just the chairs.
* When a new hum is opened the indicator from the previous hum is blanked out, ready to be replaced with a new indicator when the hum closes.


## Explanatory notes


* The choice of buckets for ***s*** uses a simple formula where the size of the bucket doubles each time, which equates to exponential growth in the bucket size.  This is roughly equivalent to the logarithmic formulae in {{VIOLINS}} used to calculate the increase in loudness from one violin to two violins playing the same note.
* The names of the hum indicators are taken from loudness marks used in musical notation.


## Implementation notes


* Some participants will not be allowed to hum contractually, but this will not need to be enforced by the system.
* The way in which the options are presented and selected and the way in which the hum indicator is selected is left to the implementer. However, the text for each option should appear as above.
* The results display needs to show all the possible results (niente, pianissimo, piano, forte, fortissimo) in some form of ordered view with an indicator as to which end is the quietest and which the loudest, with the appropriate result highlighted.




# Alternative approaches


A number of alternative approaches were considered and rejected as set out below.


## Single level of hum


A single-level of hum was considered but rejected on the basis that it took the specification too close to voting and was not a match to an in-person hum.


## More levels of hum


More levels of hum were considered but rejected as it was felt that two levels was the best overall match to an in-person hum.


## No hum indicator


Consideration was given to separating the idea of choosing not to hum and not being informed enough to participate. When we ceased normalizing the result for the number of attendees, this became irrelevant.


## Simple result calculation


Consideration was given to using a simple formula to calculate the result, such as using the score not the result, and rejected as it was felt that a logarithmic formula was a closer match to an in-person hum.


## Bucket size closer to the formulae


Consideration was given to directly using the logarithmic formulae in {{VIOLINS}} used to calculate the increase in loudness from one violin to two violins playing the same note, which would have calculated an approximate decibel level for each hum.  Each hum indicator would then represent the same number of decibels, and so produce a similar effect to the chosen specification. This was rejected because it would either produce buckets that were too small and so the top bucket would be reached too quickly, or buckets that were too large giving the inverse problem.


## Grayscale


An essentially continuous color-based indicator used in place of buckets, would better match the continuous nature of sound and further divorce the output from the absolute numbers of people humming. However, this would produce higher-precision results than are possible with human ears in a room.


# Security Considerations


Meetecho participation is restricted to people who have datatracker accounts, providing some assurance of identity. Potential attacks against this tool will either subvert Meetecho admission control, or involve multiple datatracker registrations (and Meetecho logins) to amplify the voice of a single individual.


The integrity of this tool is dependent on the integrity of the registration and fee waiver processes. In particular, they must weed out duplicate registrations, bots, and so on.


# IANA Considerations


This document has no IANA actions.




--- back


# Acknowledgements


Alissa Cooper, Jay Daley, Roman Danyliw, Colin Perkins, Alvaro Retana, and Robert Wilton made significant contributions to this document. Benjamin Kaduk, Erik Kline, Warren Kumari, and Barry Leiba also provided helpful feedback.
