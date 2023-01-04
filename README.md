# ServifyThis

Windows machines run services in the background, letting admins manage them via the Services Control panel (services.msc) or the sc command. Penetration testers sometimes want to create a Windows service that will allow them to gain and maintain remote access of a Windows machine, possibly a persistent listener offering up shell access on a given port. Unfortunately, while the Windows sc command can be used to run any .exe as a service, Windows waits 30 seconds for the given program to throw a given API call to indicate that the service has started successfully. If Windows doesn't hear back from the service, it kills the program, thinking that the service failed to start. Thus, with sc, you can make your service, but you'll only get 30 seconds of access.
Previously, various commercial and shareware programs were available that would wrap provided executables inside of code that makes the appropriate calls so that Windows would let the executable run as a service and avoid the 30-second kill rule. But, such programs were only available for a fee... until now.

InGuardians' ServifyThis program takes any Windows executable and converts it into a form suitable for use as a Windows service.

###**ServifyThis Usage Instructions:**

ServifyThis will take any Win32 executable (either command-line or GUI) and wrap it into a new executable/service/installer program that will:

1) Dump the "servified" executable on the target machine at a user-specified location and with a user-specified name.

2) Create, dump, and install a Win32 service executable that will automatically run the "servified" executable both immediately upon installation and whenever Windows boots. This service can be set to automatically respawn the "servified" executable if it exits. The name and location of the service executable, its file path, and the service name (shown in the Service control panel) are all user-specified. Optionally, the GUI of the "servified" executable can be displayed... although I don't know why you might want to...

3) The installation package self-deletes when its payload has been delivered.

4) Running the service executable with a "-u" (uninstall) option, will cause it to stop the service, stop the executable, remove the "servified" executable and finally, self-delete, leaving nothing behind on the previously exploited machine.

The parameters entered into the GUI of ServifyThis should be self-explanatory.
