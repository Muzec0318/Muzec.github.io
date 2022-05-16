---
layout: default
title : muzec - Cysec CTF 2022 Qualifier Writeup
---

A little words to keep us going XD

```
Do you have what it takes to beat the REST and be the BEST? 
```

![image](https://user-images.githubusercontent.com/69868171/168483729-be459be2-8f3b-412d-b456-c4b84ca27937.png)


Now that is a fun CTF challanges without wasting to much of a time so let jump in already to the fun part solving challanges we are starting with `WEB` category first.


### Easy WEB -- 500 Point

![image](https://user-images.githubusercontent.com/69868171/168483904-32c29500-545a-4fac-9ece-6fed5d57b799.png)

Now that we have the target URL let hit it.

![image](https://user-images.githubusercontent.com/69868171/168483982-3d755b2e-ea01-4e55-9207-9a268d250fa5.png)

Now that is a plain website quickly checking `robots.txt` and we have nothing we just got the same homepage back to us why not check the `source` for hint or way to move forrward.

![image](https://user-images.githubusercontent.com/69868171/168484087-36daee98-c896-439e-90b6-63dccf6da32c.png)

Now that is interesting we can see the `Add user` with a comment but the most intersting one that caught my eyes was `/api?id=source` we all love `API` XD so let check it out.

![image](https://user-images.githubusercontent.com/69868171/168484200-ef6ea876-9632-408b-9ef9-5aee1fc2c435.png)

That is a step forward let see what we have in the source code we just downloaded i will be using my terminal.

![image](https://user-images.githubusercontent.com/69868171/168484462-1d1205b2-0c07-4f14-917d-d19ad054d65e.png)

Let just get the flag already using `Curl` .

```
┌──(muzec㉿Muzec-Security)-[~/Desktop/CTFPlayground/CysecCTF]
└─$ curl -X GET https://cysec-easy-web.herokuapp.com/api --data "id=gimme-flag"
{"message":"CYSEC{eazy_peasy_l3m0n_squeezy}"}                                                                                                                                                                       
```

Flag:- `CYSEC{eazy_peasy_l3m0n_squeezy}`


### Breadcrumbs -- 1000 Point

![image](https://user-images.githubusercontent.com/69868171/168488158-762d8851-de3c-4860-8f0e-185ecb63c3cb.png)


A fun one seems like we are stealing a cookie lol let hit the webpage to see what we have.

![image](https://user-images.githubusercontent.com/69868171/168488229-069ca61b-aa6a-4694-a3d4-67262edf764b.png)

Seems we have a `login` page and `register` page and we have no valid credentials and it was stated already no `brute forcing` why not get our self a register account yes bro i mean let register XD.


![image](https://user-images.githubusercontent.com/69868171/168488482-988d0427-f4e4-4af1-8439-78940a1afd4c.png)

Now that we have an account let log in.

![image](https://user-images.githubusercontent.com/69868171/168488577-21995164-845f-466d-857a-f178d7296dd2.png)

In a dashboard hehehehehe don't be happy yet it just the normal account i created and seems we have some interesting pages to explore.

![image](https://user-images.githubusercontent.com/69868171/168488658-1b491275-0d52-46ff-9bd7-9acf64deb268.png)

The support page seems cool maybe XSS i just don't know yet but let try using `ngrok` to see if we can get a hit back to the listener i set up.

![image](https://user-images.githubusercontent.com/69868171/168488823-152d709b-6900-4fdd-96c6-b7de8d591a0c.png)

Now back to fill the support page.

![image](https://user-images.githubusercontent.com/69868171/168488853-bbd768c8-3f21-4d0e-9ea9-799a082d7a5f.png)

Let hit the `Submit` and wait for a hit back and boom i got a hit back but no cookie.

![image](https://user-images.githubusercontent.com/69868171/168489715-931b650f-b618-409a-9368-1647103cbddb.png)

Now that is strange right let try using `ngrok` web interface which we can always access on `http://localhost:4040` if you have ngrok running to inspect traffic.

![image](https://user-images.githubusercontent.com/69868171/168489791-64b688bf-4a8f-44f9-b6a9-a70a970e6614.png)

Waiting for some min and boom we got the cookie now let go claim or flag.

```
cnVkZWZpc2g6REM4VG1zd1FldG5kZTlSUTZuNjdOS1hGdHg3VUFyTVFOelJ6SnA2ejQ0Z0NGcGpnNVVlRlJBNUN1Q2JWNnRHSHNKdlRk
```

![image](https://user-images.githubusercontent.com/69868171/168489913-b621971d-2f34-443d-8a63-ae89984a7279.png)

Now we have our flag but am still curious to know what was encoded in the cookie.

![image](https://user-images.githubusercontent.com/69868171/168490005-0979e50e-232f-48f0-b70e-4dc007b38094.png)

Ahhhh you can't guess that right.

A quick one seems `nc` can also get us the cookie.

![image](https://user-images.githubusercontent.com/69868171/168553908-425539b2-47bb-472d-84a4-73232d76acc1.png)


Flag:- `CYSEC{itz__easssssszzzzzzy0876#}`


### The Examiner -- 1000 Point


![image](https://user-images.githubusercontent.com/69868171/168490455-f24da123-28db-4a43-99cc-42f4de8dd473.png)

Seems `The Examiner` web challange is hosted on THM platform let connect to our VPN to access it.

![image](https://user-images.githubusercontent.com/69868171/168491492-eaee8563-2395-4bf9-9860-52e8e5ffa7c8.png)

Deploying and we got our IP not going to waste to much time on using `nmap` to scan for full ports and we got one only which is port `5000` .

![image](https://user-images.githubusercontent.com/69868171/168491572-edf997cb-ea4d-4956-a482-574672a03bad.png)

Boom and we landed on a port scanner page let see what we have on the source code.

![image](https://user-images.githubusercontent.com/69868171/168491612-6873aadc-d9f1-46c5-bd26-d053788cd0fe.png)

Now that is the interesting part of the form let try intercepting our request using burp to undertand it more on how it works.

![image](https://user-images.githubusercontent.com/69868171/168491843-bf503b1e-4c7f-408b-8880-30fb7c0e5cd3.png)

Intercepted and send to repeater now let play with it.

![image](https://user-images.githubusercontent.com/69868171/168491868-c22963e4-26ff-4048-a24d-35882e66a408.png)

But i got `Invalid IP format detected.` i have no reason i keep swaping IP and Port but the same error now seems we already have the source code and our craft code i decided to change the `Content-Type` to `application/json` back in crafting our command.

![image](https://user-images.githubusercontent.com/69868171/168492285-c95c426a-b974-424a-a70d-49c85870342d.png)

Boom and we got it time to get a reverse shell back to our terminal.

![image](https://user-images.githubusercontent.com/69868171/168492426-37003502-e6d6-48a1-9228-1b4ac9ac1132.png)

Listener ready.

![image](https://user-images.githubusercontent.com/69868171/168492455-702f1566-b39c-45c8-ab32-a4f681b4036c.png)

One liner reverse shell payload to execute ready also let hit and we should have a reverse shell back to our terminal.

![image](https://user-images.githubusercontent.com/69868171/168492491-1ad3aa83-942b-4ce6-a957-52fa82d00dea.png)

Now spawning a full TTY shell to make our shell more stable and strong.

![image](https://user-images.githubusercontent.com/69868171/168492716-11fb1990-0955-4082-8c08-4ccf9b88f596.png)

Now it ready time for more enumeration.

![image](https://user-images.githubusercontent.com/69868171/168492807-0f7c6734-e5ad-48da-9227-035f30af8305.png)

User `Rudefish` can run `sudo` let hit gtfobins.

![image](https://user-images.githubusercontent.com/69868171/168492845-8f8b3ee0-be26-48ef-a038-2bb173cf4863.png)

Running that and we are root time to hunt for the flag.

![image](https://user-images.githubusercontent.com/69868171/168493029-344353e6-0561-4c10-907a-5525186f7a5c.png)

Getting into root directory seems we have no flag in it but seems we have the `.bash_history` which store the history of a user command let see what we have in it.

![image](https://user-images.githubusercontent.com/69868171/168493412-77eb7932-93d0-4e17-9c44-417d4c090f3e.png)


![image](https://user-images.githubusercontent.com/69868171/168493375-20b2b21e-62cc-4e40-b6e6-c3a35eca056c.png)

We can see the flag being remove in the `.bash_history` i try using the `find` command to see if the flag is hidden elsewhere but no luck so let check what port is running locally.

![image](https://user-images.githubusercontent.com/69868171/168494114-3c9ac44f-c003-457c-8df7-6ce6a42079a6.png)

Seems we have `SSH` port on which is cool seems we re root we can easily change any user password and have access to it also we can easily change to any  user without a password which can be done with `su sshuser` .

![image](https://user-images.githubusercontent.com/69868171/168494385-ffc351e8-614c-4e21-b40d-46e1d63ba69a.png)

Now we can easily generate a SSH private key for the user `sshuser` so we can easily access SSH with it.

![image](https://user-images.githubusercontent.com/69868171/168494991-38a0d2ec-87b2-42c0-800e-90328cb987b5.png)

```
ssh-keygen -t rsa
```

We have our private key and also added the `authorized_keys` now let try to access SSH.

![image](https://user-images.githubusercontent.com/69868171/168495070-f26c5fb1-e4c7-4fa1-8b94-2d9b2dfb1cf9.png)

Boom we have the flag and we are done.

Flag:- `CYSEC{y0u_scaNNed_ME!}`


### Doctor Strange -- 2000 Point

![image](https://user-images.githubusercontent.com/69868171/168495231-33e8db95-0563-44e8-95cb-d2e21505254b.png)

Man am tired jumping back in.

![image](https://user-images.githubusercontent.com/69868171/168495808-39aef10a-1e87-431c-a449-2814b8b3612d.png)

We have nothing on the source let check for `robots.txt` .

![image](https://user-images.githubusercontent.com/69868171/168495866-45be0e1a-0955-481b-95a4-99c336c8b675.png)

Ahhhh we have something on the `robots.txt` let check `inpect.js` .

![image](https://user-images.githubusercontent.com/69868171/168495999-3dbcb33a-6247-4f3c-9ee2-1fabd842fd9c.png)

```
const { exec } = require('child_process');

var setData = {
    isMalicious: true
};

const run = {
    runCommand: (req, res) => {
        if (!req.body.inspect) {
            return res.status(400).send("Bad request");
        } else {
            try {
                const data = JSON.parse(req.body.inspect);
                if (data.cmdToRun) {
                    const constructUserData = merge(setData, data);
                    if (setData.isMalicious === false) {
                        exec(`ping ${data.cmdToRun}`, (error, stdout, stderr) => {
                            if(error) {
                                return res.status(500).send(error.message)
                            } else if(stderr) {
                                return res.status(500).send(stderr.message);
                            } else {
                                return res.status(200).json(stdout)
                            }
                        });
                    } else {
                        exec(`ping 127.0.0.1`, (error, stdout, stderr) => {
                            if(error) {
                                return res.status(500).send(error.message)
                            } else if(stderr) {
                                return res.status(500).send(stderr.message);
                            } else {
                                return res.status(200).json({message: "Malicious code detected. This is all you get, you hacker", result: stdout})
                            }
                        });
                    }
                } else {
                    return res.status(400).send("What would you like to inspect today?");
                }
            } catch (e) {
                return res.status(400).send(e.message);
            }
        }
    }
};

module.exports = run;

const merge = (target, source) => {
    for(var attr in source) {
        if (typeof(target[attr]) === "object" && typeof(source[attr]) === "object") {
            merge(target[attr], source[attr]);
        } else {
            target[attr] = source[attr];
        }
    }
    return target;
};
```

Now that seems more like a javascript prototype pollution it kind of interesting seems we have to pollute `setData` object at the top here (line 3) to set it to `false` and `POST` request with the payload we got.

```
{"proto": {"isMalicious": false}, "cmdToRun":"<command_injection_payload>">}
```

Payload ready but seems we are missing the right endpoint let hit dirs brute forcing.

![image](https://user-images.githubusercontent.com/69868171/168496646-b81d40a5-6950-45e1-8dcc-a6baebc383ce.png)

We found a login page but no creds to access it trying some default and sql injection payloads got no luck let check the source page.

![image](https://user-images.githubusercontent.com/69868171/168496707-f67e60c1-ac7c-4d37-b3ce-18e0cb739071.png)

Now that is a progress we know it send a `POST` request to `/api/v1/login` anytime we try to login seems like more `API` let try brute forcing the endpoint to avoid missing important part that can help us solve it.

Fire up burp suite and intercept the request changing the rquest method to `POST` since the `API` request on `POST` method now that is funny WTF am typing self XD send to `intruder` .

![image](https://user-images.githubusercontent.com/69868171/168563238-3c3c32dc-6d16-4f5b-acff-2530838f76e7.png)

Now to payloads to select the wordlist seems `medium.txt` would work fine i guess.

![image](https://user-images.githubusercontent.com/69868171/168563618-503413a8-491c-4681-98bc-2c2e6e27bfe5.png)

Now hit on start attack we should get lot of `404 not found` error but from my observation the valid dirs have `400 bad request` .

![image](https://user-images.githubusercontent.com/69868171/168564456-b8e4e01f-99ca-4d87-90b3-d39470fee25a.png)

![image](https://user-images.githubusercontent.com/69868171/168565126-66c0c1ce-0d84-444f-a285-23a79d325b83.png)

Now that is some useful endpoint let see if i can register an account. Luckily yes i was able to register an account but it was useless unable to get access to the login page with it some back to the `inspect.js` it should be possible we have `inspect` endpoint let confirm it.

![image](https://user-images.githubusercontent.com/69868171/168567341-c8b6ceb4-0be9-48b5-ad76-56f8d1afdd16.png)

Back to burp suite with the endpoint and our sweet payload we created.

```
{"proto": {"isMalicious": false}, "cmdToRun":"<command_injection_payload>"}
```

![image](https://user-images.githubusercontent.com/69868171/168569291-59f8464a-a2ca-4584-9c0d-2f7c61460669.png)

```
{"proto": {"isMalicious": false}, "cmdToRun":"127.0.0.1;id"}
```

Boom we have command injection.

![image](https://user-images.githubusercontent.com/69868171/168569568-d3277215-93fa-44ac-b9fd-b1bca11921b4.png)

We can also using curl.

![image](https://user-images.githubusercontent.com/69868171/168569678-9bd553d9-e0d1-4bf5-bfe6-5639b0eef4a1.png)

Now let get our flag.

![image](https://user-images.githubusercontent.com/69868171/168569918-4ce9fb12-a1e4-48c7-9f9a-d9fe76bc6fad.png)

Done and dusted fun right.

Flag:- `CYSEC{l3t_the_!njection5_r41n.}`