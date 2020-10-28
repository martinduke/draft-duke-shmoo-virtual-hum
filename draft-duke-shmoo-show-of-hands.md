---
title: "Specification for a show of hands tool"
abbrev: "Show Of Hands"
docname: draft-duke-shmoo-show-of-hands-00
date: {DATE}
category: info
ipr: trust200902
area: General

stand_alone: yes
pi: [toc, sortrefs, symrefs, docmapping]

author:
  ins: M. Duke
  name: Martin Duke
  org: F5 Networks, Inc
  email: martin.h.duke@gmail.com

informative:

  DRAFT_VIRTUAL_HUM:
    title: "Specification for a virtual humming tool"
    target: https://datatracker.ietf.org/doc/draft-duke-shmoo-virtual-hum/
    date: 2020

  SURVEY_108:
    title: "IETF 108 Survey"
    target: https://www.ietf.org/media/documents/IETF_108_Meeting_Survey.pdf
    date: 2020

--- abstract

This is the specification for an experimental show of hands tool for the Meetecho system to be used in online meetings to help chairs quickly poll the meeting. This tool is different from the previous experimental virtual hum tool as it addresses a different use case with different functionality.  Following mixed feedback in the IETF 108 post-meeting survey, the experimental virtual hum tool has been withdrawn from the Meetecho client for IETF 109.

--- middle

# Introduction

This is the specification for an experimental show of hands tool for the Meetecho system to be used in online meetings to help chairs quickly poll the meeting. This tool is different from the previous experimental virtual hum tool {{DRAFT_VIRTUAL_HUM}} as it addresses a different use case with different functionality.  Following mixed feedback in the IETF 108 post-meeting survey {{SURVEY_108}}, the experimental virtual hum tool has been withdrawn from the Meetecho client for IETF 109.

# Definition and usage of "show of hands"

In the context of this document, a "show of hands" is a simple, fast and anonymous mechanism for asking a yes/no question of a large group of people, with the common understanding that this mechanism is not a means for calling consensus and therefore only minimal formality of process is required.

# Tool specification

This specification is intended to be feature complete, which means that what should be implemented is only what is explicitly stated here and nothing else.

## General

* There is only one type of show of hands
* Only one show of hands can be open at any one time in a session.
* The Secretariat are excluded from the show of hands and are not able to participate and do not feature in the calculations:

## Opening and closing show of hands

* A session chair can open a show of hands.
* A session chair can assign a title to a show of hands to be made visible to session participants.
* A session chair can open a show of hands at any time during a session, except when a show of hands is already open.
* A session chair can open multiple shows of hands per session.
* A show of hands is closed when the session chair closes it.

## Taking part in a show of hands

* While a show of hands is open an indicator needs to be shown to all participants that includes the title, if assigned, and either the options below or a link that goes directly to them.
* When a show of hands is open each participant in the session may take part through the following mechanism: 
Each participant is presented with the following options from which they can select one.  None of the options is selected as a default.
"Raise hand"
"Do not raise hand"
No confirmation action is required.
A participant can change their chosen option at any time while the show of hands is open.
* When a participant selects any option then they are considered to have participated in the show of hands. 
* If a participant joins the session during the show of hands then they can take part.
* If a participant leaves the session during the show of hands and they are considered to have participated then their show of hands is still used for data calculation.

## Calculating and displaying the result

* In real time during a show of hands the following data is calculated:
The total number of participants who selected the "Raise hand" option.
The total number of participants who selected the "Do not raise hand" option
The total number of participants who have not selected either option.
* All totals are displayed to all participants in real time.
* When the show of hands is closed the totals are left displayed along with the relevant title.
* When a new show of hands is opened the totals from the previous show of hands are still shown, along with their assigned titles, in an ordered list.

## Implementation notes

* The way in which the options are presented and selected and the way in which the totals are presented are left to the implementer. However, the text for each option should appear as above.


# Alternative approaches

The following alternative approaches were considered.

## Multiple options

Consideration was given to allowing more options (e.g., thumbs up, neutral, and thumbs down) and to allowing the chair to specify the list of options to be used in a show of hands.  These alternatives may increase the use cases of the tool but also may increase its complexity.  At this stage these alternatives have not been included, nor have they been ruled out.

# Security Considerations

Meetecho participation is restricted to people who have datatracker accounts, providing some assurance of identity. Potential attacks against this tool will either subvert Meetecho admission control, or involve multiple datatracker registrations (and Meetecho logins) to amplify the voice of a single individual.

The integrity of this tool is dependent on the integrity of the registration and fee waiver processes. In particular, they must weed out duplicate registrations, bots, and so on.

# IANA Considerations

This document has no IANA actions.


--- back

# Acknowledgements

Alissa Cooper, Jay Daley, Colin Perkins, and Alvaro Retana made significant contributions to this document. There were also numerous informal conversations at IETF 108 that influenced it.

