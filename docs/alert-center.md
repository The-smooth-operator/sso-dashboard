# Proposal for Alert Center

## Alert Center Purpose

The security alert center will provide sso-dashboard users security, information, and configuration alerts.
Based on alert severity alerts should be called out differently based on category.  Different types of alerts
will have different things the user can do with them.

### Alert Severity

- __Information__ : an informational alert regarding systems maintenance or other information pertaining to apps in the dashboard.

- __Warning__ : a warning regarding the state of the users account or configuration.  Example: ( Firefox is out of date, your password is older than (x) days)

- __High Security__ : a high security alert.  This is any event that would potentially create risk to Mozilla based on the state of the users
account.  Example: ( Your version of Firefox is no longer supported or vulnerable.  Your account has been part of a major data breach. )

- __High Security Alert__ ( from MozDef ):  MozDef the Mozilla defense platform tracks user account activity.  Alerts coming from MozDef tell
the user that something anomalous happened with their account.  These are the category of alert that would require a user to self identify
that the alert was a false positive or ask for help.  

### Alert Schema

As an enterprise infosec system I can send an alert for "All Users" or an individual and it should show in real time in the related user(s) dashboard.

```
alert:
  severity: information|warning|high|mozdef  # Required
  message: "Your just moved faster than superman." # Required
  additonal_info: "A large amount of information that may be about what has happened." # Optional Displays only in alert center.
  date: 07:07:07 6/26/17 GMT -8 # Optional
  additional_label: "More Info" # Text rendered on button next to alert ( Optional )
  additional_link: "https://wiki.example.com/geolocation/alert" # Optional
```

### Alert UI

Information and warning alerts can only be acknowledged or dismissed.  They may also have a "more_info" link that takes them away from the dashboard.  

__Informational alerts__
!['dashboard.png'](images/warning.png)

MozDef alerts should always be acknowledged as false positives or positives.  These are high severity use cases where infosec needs to be notified if the user needs help.  

> A user flagging an alert as a false positive should require them to 2FA again to prevent an attacker from stealing a session etc and clearing their own alerts.  

__MozDef Alerts__
!['dashboard.png'](images/mozdef.png)

### Alert Center

The alert center has all of the same information available as in the bar with additional information taken from the "additional info" about the alert.  Users can acknowledge / dismiss for all alerts not generated by MozDef and Confirm in the same way for MozDef alerts.  

## What about lot's of alerts?  

We probably also want to account for a user having a ton of alerts all at once.  Let's say that as a user I am part of a major data breach, my house gets robbed, and attackers are logging in with one of my 2FA device(s) and password all over the globe.  There should also be a high severity dialogue that says.

"You have 52 alerts waiting.  View notification center."  _or something like that_ 