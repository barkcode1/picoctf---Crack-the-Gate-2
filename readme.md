```
The login system has been upgraded with a basic rate-limiting mechanism that locks out repeated failed attempts from the same source. We’ve received a tip that the system might still trust user-controlled headers. Your objective is to bypass the rate-limiting restriction and log in using the known email address: ctf-player@picoctf.org and uncover the hidden secret.
The website is running here. Can you try to log in?.
Download the passwords list here.
```

Like the last problem, I quickly checked the source code. Expectedly however, I couldn't find anything of use.\
\
I turned my attention to the password list. It seemed I could just see which password worked.\
\
Going to burpsuite, I set up an intruder sniper attack to loop throughout all the passwords.\
As said by the description however, I was met with 429 errors, which represented a "too many requests" error.\
\
I first attempted to bypass this by changing my user-agent in the header in case it was tracking through there. Unfortunately, that didn't seem to work.\
\
My second idea was much better however, which was to change my ip address. Googling up the exact command gave me ```X-Forwarded-For```\
I made a second list of numbers so it would loop through different ip address in the intruder attack - specifically the pitchfork attack.\
\
After seeing every response give 200, I knew I had solved it. I looped through all the responses, with all most giving: ```"success":false```\
Luckily though, one response gave the flag: \
```"success":true,"email":"ctf-player@picoctf.org","firstName":"pico","lastName":"player","flag":"picoCTF{xff_byp4ss_brut3_ff36dbbc}"```


