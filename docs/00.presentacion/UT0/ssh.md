**Unitat0-SSH![](Aspose.Words.a8580f72-fe80-44ac-8828-ca93dcca86d7.001.png)**

MaiteMartí

![](Aspose.Words.a8580f72-fe80-44ac-8828-ca93dcca86d7.002.png)Unitat0-SSH Curso2021-2022![](Aspose.Words.a8580f72-fe80-44ac-8828-ca93dcca86d7.003.png)

**1.Introduccion**

OpenSSHisafreelyavailableversionoftheSecureShell(SSH)protocolfamilyoftoolsforremotely controlling,ortransferringfilesbetween,computers.OpenSSHprovidesaserverdaemonandclient toolstofacilitatesecure,encryptedremotecontrolandfiletransferoperations.

The OpenSSH server component, sshd, listens continuously for client connections from any of the clienttools.

Whenaconnectionrequestoccurs,sshdsetsupthecorrectconnectiondependingonthetypeofclient toolconnecting.

Forexample,iftheremotecomputerisconnectingwiththesshclientapplication,theOpenSSH ![](Aspose.Words.a8580f72-fe80-44ac-8828-ca93dcca86d7.004.png)server sets up a remote control session after authentication. If a remote user connects to an OpenSSHserverwithscp,theOpenSSHserverdaemoninitiatesasecurecopyoffilesbetweenthe serverandclientafterauthentication.OpenSSHcanusemanyauthenticationmethods,including plainpassword,publickey,andKerberostickets.

SSHcommandhas3differentparts:

1 ssh {user}@{host}![](Aspose.Words.a8580f72-fe80-44ac-8828-ca93dcca86d7.005.png)

Openasecurecipherconnection.{user}representsthesytemaccount.{host}referstothehostyou want to connectto. This couldbe an IP address (for instance, 244.235.23.19) or a domain name (for example,www.xyzdomain.com).

**2.Installation**

Installation of the OpenSSH client and server applications is simple. To install the OpenSSH client applicationsonyourUbuntusystem,usethiscommandataterminalprompt(usuallyclientisinstalled bydefault):sudoaptinstallopenssh-client

ToinstalltheOpenSSHserverapplication,andrelatedsupportfiles,usethiscommandataterminal prompt:

1 sudo apt install openssh-server![](Aspose.Words.a8580f72-fe80-44ac-8828-ca93dcca86d7.006.png)

**Tasks**

![](Aspose.Words.a8580f72-fe80-44ac-8828-ca93dcca86d7.007.png) OpenyourUbuntuServer.![](Aspose.Words.a8580f72-fe80-44ac-8828-ca93dcca86d7.008.png)

IESJaumeIIelJust-NetworkServices 2/[5](#_page4_x69.87_y69.87)

![](Aspose.Words.a8580f72-fe80-44ac-8828-ca93dcca86d7.009.png) Checksshpacketopenssh-server.

1 $ dpkg -l openssh-server![](Aspose.Words.a8580f72-fe80-44ac-8828-ca93dcca86d7.010.png)

![](Aspose.Words.a8580f72-fe80-44ac-8828-ca93dcca86d7.011.png) Ifyoudon’thaveityoumustinstallthepackagebyexecutingthesecommands:

1  $ sudo apt-get update -y![](Aspose.Words.a8580f72-fe80-44ac-8828-ca93dcca86d7.012.png)
1  $ sudo apt-get upgrade -y
1  $ sudo apt-get install openssh-server -y

![](Aspose.Words.a8580f72-fe80-44ac-8828-ca93dcca86d7.013.png) Checkiftheserviceisrunning:

1 $ systemctl status sshd.service![](Aspose.Words.a8580f72-fe80-44ac-8828-ca93dcca86d7.014.png)

or

1 $ **ps** -ef | grep sshd![](Aspose.Words.a8580f72-fe80-44ac-8828-ca93dcca86d7.015.png)

- Checkiftheportisopened.Youcanuseanyofthesecommands:

1 $ sudo netstat -ltp | grep sshd![](Aspose.Words.a8580f72-fe80-44ac-8828-ca93dcca86d7.016.png)

or

1 $ sudo ss -ltp | grep sshd ![](Aspose.Words.a8580f72-fe80-44ac-8828-ca93dcca86d7.017.png)or

1 $ sudo nmap localhost![](Aspose.Words.a8580f72-fe80-44ac-8828-ca93dcca86d7.018.png)

![](Aspose.Words.a8580f72-fe80-44ac-8828-ca93dcca86d7.019.png) Enelcasodequenoseestéejecutandoelservidor,lánzaloconelsiguientecomandoyvuelvea

hacerlascomprobacionesanteriores.

1 $ sudo systemctl start sshd.service![](Aspose.Words.a8580f72-fe80-44ac-8828-ca93dcca86d7.020.png)

![](Aspose.Words.a8580f72-fe80-44ac-8828-ca93dcca86d7.021.png) Unavezinstalado,realizadistintaspruebasdeconexióndesdeuncliente.Recuerdaque,aunque

el cliente se ejecuta desde otra máquina, el usuario especificado en la conexión debe ser del servidor.

**3.Configuration**

YoumayconfigurethedefaultbehavioroftheOpenSSHserverapplication,sshd,byeditingthefile /etc/ssh/sshd\_config.![](Aspose.Words.a8580f72-fe80-44ac-8828-ca93dcca86d7.022.png)

For information about the configuration directives used in this file, you may view the appropriate manualpagewiththefollowingcommand,issuedataterminalprompt:

1 man sshd\_config![](Aspose.Words.a8580f72-fe80-44ac-8828-ca93dcca86d7.023.png)

TipPriortoeditingtheconfigurationfile,youshouldmakeacopyoftheoriginalfileandprotectit ![](Aspose.Words.a8580f72-fe80-44ac-8828-ca93dcca86d7.024.png)fromwritingsoyouwillhavetheoriginalsettingsasareferenceandtoreuseasnecessary.Copy the/etc/ssh/sshd\_configfileandprotectitfromwritingwiththefollowingcommands,issuedata terminalprompt:

sudo cp /etc/ssh/sshd\_config /etc/ssh/sshd\_config.original

sudo chmod a-w /etc/ssh/sshd\_config.original Furthermoresincelosingansshservermightmeanlosingyourwaytoreachaserver,checkthe![](Aspose.Words.a8580f72-fe80-44ac-8828-ca93dcca86d7.025.png)

configurationafterchangingitandbeforerestartingtheserver:

sudo sshd -t -f /etc/ssh/sshd\_config Thefollowingareexamplesofconfigurationdirectivesyoumaychange:

- TosetyourOpenSSHtolistenonTCPport2222insteadofthedefaultTCPport22,changethe Portdirectiveassuch: Port 2222
  - TomakeyourOpenSSHserverdisplaythecontentsofthe/etc/issue.netfileasapre-loginbanner, simplyaddormodifythislineinthe/etc/ssh/sshd\_configfile: Banner /etc/issue.net

Aftermakingchangestothe/etc/ssh/sshd\_configfile,savethefile,andrestartthesshdserverapplica- tiontoeffectthechangesusingthefollowingcommandataterminalprompt:

1 sudo systemctl restart sshd.service![](Aspose.Words.a8580f72-fe80-44ac-8828-ca93dcca86d7.026.png)

**4.HowtoConnectviaSSH**

Now that you have the OpenSSH client and server installed on every machine you need, you can establishasecureremoteconnectionwithyourservers.Todoso:

1. OpentheSSHterminalonyourmachineandrunthefollowingcommand: ssh your\_username@host\_ip\_address![](Aspose.Words.a8580f72-fe80-44ac-8828-ca93dcca86d7.022.png)

If the username on your local machine matches the one on the server you are trying to![](Aspose.Words.a8580f72-fe80-44ac-8828-ca93dcca86d7.027.png)

connectto,youcanjusttype:

1 'ssh host\_ip\_address`![](Aspose.Words.a8580f72-fe80-44ac-8828-ca93dcca86d7.028.png)

2. Type in your password and hit Enter. Note that you will not get any feedback on the screen whiletyping.Ifyouarepastingyourpassword,makesureitisstoredsafelyandnotinatextfile. Whenyouareconnectingtoaserverfortheveryfirsttime,itwillaskyouifyouwanttocontinue connecting.JusttypeyesandhitEnter.Thismessageappearsonlythistimesincetheremote serverisnotidentifiedonyourlocalmachine.AnECDSAkeyfingerprintisnowaddedandyou areconnectedtotheremoteserver.

If the computer you are trying to remotely connect to is on the same network, then it is best to use theprivateIPaddressinsteadofthepublicIPaddress.Otherwise,youwillhavetousethepublicIP addressonly.Additionally,makesurethatyouknowthecorrectTCPportOpenSSHislisteningtofor connectionrequestsandthattheportforwardingsettingsarecorrect.Thedefaultportis22ifnobody changedconfigurationinthesshd\_configfile.Youmayalsojustappendtheportnumberafterthehost IPaddress.

HereistheexampleofaconnectionrequestusingtheOpenSSHclient.Wewillspecifytheportnumber aswell:

1 username@machine:~$ ssh alumne@185.52.53.222 –p7654![](Aspose.Words.a8580f72-fe80-44ac-8828-ca93dcca86d7.029.png)![](Aspose.Words.a8580f72-fe80-44ac-8828-ca93dcca86d7.022.png)
IESJaumeIIelJust-NetworkServices 5/5
