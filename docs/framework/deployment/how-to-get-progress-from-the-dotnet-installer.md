---
title: 'Gewusst wie: Abrufen des Status vom Installationsprogramm für .NET Framework 4.5'
ms.date: 03/30/2017
dev_langs:
- cpp
helpviewer_keywords:
- progress information, .NET Framework installer
- .NET Framework, installing
ms.assetid: 0a1a3ba3-7e46-4df2-afd3-f3a8237e1c4f
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 84bd96f27e8276546bef0dd9994163ccd843ac20
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/04/2018
---
# <a name="how-to-get-progress-from-the-net-framework-45-installer"></a>Gewusst wie: Abrufen des Status vom Installationsprogramm für .NET Framework 4.5
Bei [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] handelt es sich um eine verteilbare Laufzeit. Wenn Sie Apps für diese Version von .NET Framework entwickeln, können Sie das [!INCLUDE[net_v45](../../../includes/net-v45-md.md)]-Setup als Teil einer erforderlichen Komponente in das Setup Ihrer App einschließen (mit dem Setup verketten). Für ein angepasstes oder einheitliches Setup können Sie festlegen, dass das [!INCLUDE[net_v45](../../../includes/net-v45-md.md)]-Setup automatisch gestartet und sein Status nachverfolgt wird, während der Setupstatus Ihrer App angezeigt wird. Das [!INCLUDE[net_v45](../../../includes/net-v45-md.md)]-Setup (das beobachtet werden kann) definiert mithilfe eines MMIO (Memory-Mapped IO)-Segments ein Protokoll für die Kommunikation mit Ihrem Setup (dem Monitor oder Chainer), um die automatische Nachverfolgung zu aktivieren. Dieses Protokoll definiert ein Verfahren für einen Chainer zum Abrufen von Statusinformationen und ausführlichen Ergebnissen, zum Antworten auf Meldungen sowie zum Abrechen des [!INCLUDE[net_v45](../../../includes/net-v45-md.md)]-Setups.  
  
-   **Aufruf**  Um das [!INCLUDE[net_v45](../../../includes/net-v45-md.md)]-Setup aufzurufen und Statusinformationen aus dem MMIO-Abschnitt zu empfangen, muss das Setupprogramm folgende Aktionen ausführen:  
  
    1.  Aufruf des verteilbaren Programms für [!INCLUDE[net_v45](../../../includes/net-v45-md.md)]:  
  
        ```  
        dotNetFx45_Full_x86_x64.exe /q /norestart /pipe section-name  
        ```  
  
         Dabei ist *Abschnittname* ein beliebiger Name, mit dem Sie die App identifizieren. Das .NET Framework-Setup liest und schreibt asynchron aus dem/in den MMIO-Abschnitt. Daher ist es möglicherweise hilfreich, während dieser Zeit Ereignisse und Meldungen zu verwenden. Im Beispiel wird der .NET Framework-Setupvorgang von einem Konstruktor erstellt, der sowohl den MMIO-Abschnitt (`TheSectionName`) zuordnet als auch ein Ereignis (`TheEventName`) definiert.  
  
        ```  
        Server():ChainerSample::MmioChainer(L"TheSectionName", L"TheEventName")  
        ```  
  
         Ersetzen Sie diese Namen durch Namen, die für das Setupprogramm eindeutig sind.  
  
    2.  Lesen aus dem MMIO-Abschnitt. In [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] erfolgen Download und Installation gleichzeitig: Ein Teil von .NET Framework kann installiert werden, während ein anderer Teil heruntergeladen wird. Als Ergebnis wird der Status als zwei Zahlen (`m_downloadSoFar` und `m_installSoFar`), die von 0 bis 255 zunehmen, an den MMIO-Abschnitt zurückgesendet (das heißt, in den Abschnitt geschrieben). Wenn 255 geschrieben wurde und .NET Framework beendet wird, ist die Installation abgeschlossen.  
  
-   **Exitcodes** Mit den folgenden Exitcodes im Befehl zum Aufrufen des verteilbaren Programms für [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] wird angegeben, ob das Setup erfolgreich war oder mit einem Fehler beendet wurde:  
  
    -   0 - erfolgreich abgeschlossenes Setup.  
  
    -   3010 – Setup wurde erfolgreich abgeschlossen. Das System muss neu gestartet werden.  
  
    -   1602 – Setup wurde abgebrochen.  
  
    -   Alle anderen Codes - in Setup sind Fehler aufgetreten; Details dazu finden Sie in den unter "%temp%" erstellten Protokolldateien.  
  
-   **Abbrechen des Setups** Sie können Setup jederzeit abbrechen, indem Sie mit der `Abort`-Methode das `m_downloadAbort`-Flag und das `m_ installAbort`-Flag im MMIO-Abschnitt festlegen.  
  
## <a name="chainer-sample"></a>Chainer-Beispiel  
 Im Chainer-Beispiel wird das [!INCLUDE[net_v45](../../../includes/net-v45-md.md)]-Setup automatisch gestartet und nachverfolgt, während der Status angezeigt wird. Dieses Beispiel ähnelt dem Chainer-Beispiel für .NET Framework 4. Jedoch werden außerdem Systemneustarts vermieden, indem das Meldungsfeld zum Schließen von .NET Framework 4-Apps verarbeitet wird. Weitere Informationen zu diesem Meldungsfeld finden Sie unter [Reducing System Restarts During .NET Framework 4.5 Installations (Reduzieren von Systemneustarts bei .NET Framework 4.5-Installationen)](../../../docs/framework/deployment/reducing-system-restarts.md). Sie können dieses Beispiel mit dem .NET Framework 4-Installationsprogramm verwenden. In diesem Szenario wird die Meldung einfach nicht gesendet.  
  
> [!WARNING]
>  Sie müssen das Beispiel als Administrator ausführen.  
  
 Sie können die vollständige Visual Studio-Projektmappe für das [Chainer-Beispiel für .NET Framework 4.5](http://go.microsoft.com/fwlink/?LinkId=231345) von der MSDN Samples Gallery herunterladen.  
  
 In den folgenden Abschnitten werden die wichtigsten Dateien in diesem Beispiel beschrieben: MMIOChainer.h, ChainingdotNet4.cpp und IProgressObserver.h.  
  
#### <a name="mmiochainerh"></a>MMIOChainer.h  
  
-   Die Datei „MMIOChainer.h“ (siehe den [vollständigen Code](http://go.microsoft.com/fwlink/?LinkId=231369)) enthält die Datenstrukturdefinition und die Basisklasse, von der die chainer-Klasse abgeleitet werden sollte. [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] erweitert die MMIO-Datenstruktur, um Daten zu behandeln, die das [!INCLUDE[net_v45](../../../includes/net-v45-md.md)]-Installationsprogramm benötigt. Die Änderungen an der MMIO-Struktur sind abwärtskompatibel. Deshalb kann ein .NET Framework 4-Chainer mit dem .NET Framework 4.5-Setup verwendet werden, ohne dass eine Neukompilierung erforderlich ist. In diesem Szenario wird jedoch nicht die Funktion zur Reduzierung von Systemneustarts unterstützt.  
  
     Ein Versionsfeld ermöglicht das Erkennen von Änderungen an der Struktur und dem Meldungsformat.  Das .NET Framework-Setup bestimmt die Version der Chainer-Schnittstelle, indem die `VirtualQuery`-Funktion aufgerufen wird, um die Größe der Dateizuordnung zu ermitteln.  Wenn die Größe für das Versionsfeld ausreicht, verwendet das .NET Framework-Setup den angegebenen Wert. Wenn die Dateizuordnung zu klein ist, um ein Versionsfeld aufzunehmen, wie dies bei .NET Framework 4 der Fall ist, wird beim Setupvorgang Version 0 (4) angenommen. Wenn der Chainer die Version der Meldung, die vom .NET Framework-Setup gesendet werden soll, nicht unterstützt, geht das .NET Framework-Setup von der Antwort "Ignorieren" aus.  
  
     Die MMIO-Datenstruktur ist wie folgt definiert:  
  
    ```cpp  
    // MMIO data structure for interprocess communication  
        struct MmioDataStructure  
        {  
            bool m_downloadFinished;               // Is download complete?  
            bool m_installFinished;                // Is installation complete?  
            bool m_downloadAbort;                  // Set to cause downloader to abort.  
            bool m_installAbort;                   // Set to cause installer to abort.  
            HRESULT m_hrDownloadFinished;          // Resulting HRESULT for download.  
            HRESULT m_hrInstallFinished;           // Resulting HRESULT for installation.  
            HRESULT m_hrInternalError;  
            WCHAR m_szCurrentItemStep[MAX_PATH];  
            unsigned char m_downloadSoFar;         // Download progress 0-255 (0-100% done).   
            unsigned char m_installSoFar;          // Installation progress 0-255 (0-100% done).  
            WCHAR m_szEventName[MAX_PATH];         // Event that chainer creates and chainee opens to sync communications.  
  
            BYTE m_version;                        // Version of the data structure, set by chainer:  
                                                   // 0x0: .NET Framework 4   
                                                   // 0x1: .NET Framework 4.5  
  
            DWORD m_messageCode;                   // Current message sent by the chainee; 0 if no message is active.  
            DWORD m_messageResponse;               // Chainer's response to current message; 0 if not yet handled.  
            DWORD m_messageDataLength;             // Length of the m_messageData field, in bytes.  
            BYTE m_messageData[1];                 // Variable-length buffer; content depends on m_messageCode.  
        };  
    ```  
  
-   Die `MmioDataStructure`-Datenstruktur sollte nicht direkt verwendet werden. Verwenden Sie stattdessen die `MmioChainer`-Klasse zum Implementieren des Chainers. Leiten Sie die `MmioChainer`-Klasse ab, um das verteilbare [!INCLUDE[net_v45](../../../includes/net-v45-md.md)]-Paket zu verketten.  
  
#### <a name="iprogressobserverh"></a>IProgressObserver.h  
  
-   Die Datei „IProgressObserver.h“ implementiert einen Statusbeobachter (siehe den [vollständigen Code](http://go.microsoft.com/fwlink/?LinkId=231370)). Dieser Beobachter wird über den Download- und Installationsstatus (als `char` ohne Vorzeichen mit den Werten 0-255, gibt Abschluss von 1 %-100 % an) benachrichtigt. Der Beobachter wird außerdem benachrichtigt, wenn der Chainee eine Meldung sendet, und der Beobachter sollte eine Antwort senden.  
  
    ```cpp  
        class IProgressObserver  
        {  
        public:  
            virtual void OnProgress(unsigned char) = 0; // 0 - 255:  255 == 100%  
            virtual void Finished(HRESULT) = 0;         // Called when operation is complete    
            virtual DWORD Send(DWORD dwMessage, LPVOID pData, DWORD dwDataLength) = 0; // Called when a message is sent  
        };  
    ```  
  
#### <a name="chainingdotnet45cpp"></a>ChainingdotNet4.5.cpp  
  
-   Die Datei [chainingdotNet4.5.cpp](http://go.microsoft.com/fwlink/?LinkId=231368) implementiert die von der `MmioChainer`-Klasse abgeleitete `Server`-Klasse und setzt die entsprechenden Methoden außer Kraft, um Statusinformationen anzuzeigen. Der MmioChainer erstellt einen Abschnitt mit dem angegebenen Abschnittsnamen und initialisiert den Chainer mit dem angegebenen Ereignisnamen. Der Ereignisname wird in der zugeordneten Datenstruktur gespeichert. Sie sollten eindeutige Abschnitts- und Ereignisnamen angeben. Die `Server`-Klasse im folgenden Code startet das angegebene Setupprogramm, überwacht seinen Status und gibt einen Exitcode zurück.  
  
    ```cpp  
    class Server : public ChainerSample::MmioChainer, public ChainerSample::IProgressObserver  
    {  
    public:  
        …………….  
        Server():ChainerSample::MmioChainer(L"TheSectionName", L"TheEventName") //customize for your event names  
        {}  
    ```  
  
     Die Installation wird in der Main-Methode gestartet.  
  
    ```cpp  
    // Main entry point for program  
    int __cdecl main(int argc, _In_count_(argc) char **_argv)  
    {  
        int result = 0;  
        CString args;  
        if (argc > 1)  
        {  
            args = CString(_argv[1]);  
        }  
  
        if (IsNetFx4Present(NETFX45_RC_REVISION))  
        {  
            printf(".NET Framework 4.5 is already installed");  
        }  
        else  
        {  
            result = Server().Launch(args);  
        }  
  
        return result;  
    }  
    ```  
  
-   Vor dem Starten der Installation überprüft der Chainer durch Aufruf von [!INCLUDE[net_v45](../../../includes/net-v45-md.md)], ob `IsNetFx4Present` bereits installiert ist.  
  
    ```cpp  
    ///  Checks for presence of the .NET Framework 4.  
    ///    A value of 0 for dwMinimumRelease indicates a check for the .NET Framework 4 full  
    ///    Any other value indicates a check for a specific compatible release of the .NET Framework 4.  
    #define NETFX40_FULL_REVISION 0  
    // TODO: Replace with released revision number  
    #define NETFX45_RC_REVISION MAKELONG(50309, 5)   // .NET Framework 4.5   
    bool IsNetFx4Present(DWORD dwMinimumRelease)  
    {  
        DWORD dwError = ERROR_SUCCESS;  
        HKEY hKey = NULL;  
        DWORD dwData = 0;  
        DWORD dwType = 0;  
        DWORD dwSize = sizeof(dwData);  
  
        dwError = ::RegOpenKeyExW(HKEY_LOCAL_MACHINE, L"SOFTWARE\\Microsoft\\NET Framework Setup\\NDP\\v4\\Full", 0, KEY_READ, &hKey);  
        if (ERROR_SUCCESS == dwError)  
        {  
            dwError = ::RegQueryValueExW(hKey, L"Release", 0, &dwType, (LPBYTE)&dwData, &dwSize);  
  
            if ((ERROR_SUCCESS == dwError) && (REG_DWORD != dwType))  
            {  
                dwError = ERROR_INVALID_DATA;  
            }  
            else if (ERROR_FILE_NOT_FOUND == dwError)  
            {  
                // Release value was not found, let's check for 4.0.  
                dwError = ::RegQueryValueExW(hKey, L"Install", 0, &dwType, (LPBYTE)&dwData, &dwSize);  
  
                // Install = (REG_DWORD)1;  
                if ((ERROR_SUCCESS == dwError) && (REG_DWORD == dwType) && (dwData == 1))  
                {  
                    // treat 4.0 as Release = 0  
                    dwData = 0;  
                }  
                else  
                {  
                    dwError = ERROR_INVALID_DATA;  
                }  
            }  
        }  
  
        if (hKey != NULL)  
        {  
            ::RegCloseKey(hKey);  
        }  
  
        return ((ERROR_SUCCESS == dwError) && (dwData >= dwMinimumRelease));  
    }  
    ```  
  
-   Sie können den Pfad der ausführbaren Datei (im Beispiel setup.exe) in der `Launch`-Methode ändern, damit sie auf den richtigen Speicherort zeigt, oder den Code anpassen, um den Speicherort zu bestimmen. Die `MmioChainer`-Basisklasse stellt die `Run()`-Blockierungsmethode bereit, die von der abgeleiteten Klasse aufgerufen wird.  
  
    ```cpp  
    bool Launch(const CString& args)  
    {  
    CString cmdline = L"dotNetFx45_Full_x86_x64.exe -pipe TheSectionName " + args; // Customize with name and location of setup .exe that you want to run  
    STARTUPINFO si = {0};  
    si.cb = sizeof(si);  
    PROCESS_INFORMATION pi = {0};  
  
    // Launch the Setup.exe that installs the .NET Framework 4.5  
    BOOL bLaunchedSetup = ::CreateProcess(NULL,   
     cmdline.GetBuffer(),  
     NULL, NULL, FALSE, 0, NULL, NULL,   
     &si,  
     &pi);  
  
    // If successful   
    if (bLaunchedSetup != 0)  
    {  
    IProgressObserver& observer = dynamic_cast<IProgressObserver&>(*this);  
    Run(pi.hProcess, observer);  
  
    ……………………..   
    return (bLaunchedSetup != 0);  
    }  
    ```  
  
-   Die `Send`-Methode fängt die Meldungen ab und verarbeitet sie.  In dieser Version von Microsoft .NET Framework wird nur die Meldung zum Schließen der Anwendung unterstützt.  
  
    ```cpp  
            // SendMessage  
            //  
            // Send a message and wait for the response.  
            // dwMessage: Message to send  
            // pData: The buffer to copy the data to  
            // dwDataLength: Initially a pointer to the size of pBuffer.  Upon successful call, the number of bytes copied to pBuffer.  
            //--------------------------------------------------------------  
        virtual DWORD Send(DWORD dwMessage, LPVOID pData, DWORD dwDataLength)  
        {  
            DWORD dwResult = 0;  
            printf("recieved message: %d\n", dwMessage);  
            // Handle message  
            switch (dwMessage)  
            {  
            case MMIO_CLOSE_APPS:  
                {  
                    printf("    applications are holding files in use:\n");  
                    IronMan::MmioCloseApplications* applications = reinterpret_cast<IronMan::MmioCloseApplications*>(pData);  
                    for(DWORD i = 0; i < applications->m_dwApplicationsSize; i++)  
                    {  
                        printf("      %ls (%d)\n", applications->m_applications[i].m_szName, applications->m_applications[i].m_dwPid);  
                    }  
  
                    printf("    should appliations be closed? (Y)es, (N)o, (R)efresh : ");  
                    while (dwResult == 0)  
                    {  
                        switch (toupper(getwchar()))  
                        {  
                        case 'Y':  
                            dwResult = IDYES;  // Close apps  
                            break;  
                        case 'N':  
                            dwResult = IDNO;  
                            break;  
                        case 'R':  
                            dwResult = IDRETRY;  
                            break;  
                        }  
                    }  
                    printf("\n");  
                    break;  
                }  
            default:  
                break;  
            }  
            printf("  response: %d\n  ", dwResult);  
            return dwResult;  
        }  
    };  
    ```  
  
-   Statusdaten sind Werte vom Typ `char` ohne Vorzeichen zwischen 0 (0 %) und 255 (100 %).  
  
    ```cpp  
    private: // IProgressObserver  
        virtual void OnProgress(unsigned char ubProgressSoFar)  
        {…………  
       }  
    ```  
  
-   Das HRESULT wird an die `Finished`-Methode übergeben.  
  
    ```cpp  
    virtual void Finished(HRESULT hr)  
    {  
    // This HRESULT is communicated over MMIO and may be different than process  
    // Exit code of the Chainee Setup.exe itself  
    printf("\r\nFinished HRESULT: 0x%08X\r\n", hr);  
    }  
    ```  
  
    > [!IMPORTANT]
    >  Das verteilbare Programm von [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] schreibt in der Regel viele Statusmeldungen und eine einzelne Meldung, die den Abschluss angibt (auf Chainer-Seite). Es liest außerdem asynchron und sucht nach `Abort`-Datensätzen. Wenn es einen `Abort`-Datensatz empfängt, wird die Installation abgebrochen, und nach dem Abbruch der Installation und dem Rollback der Setupvorgänge wird ein abgeschlossener Datensatz geschrieben, der E_ABORT lautet.  
  
 Ein typischer Server erstellt einen zufälligen MMIO-Dateinamen, erstellt die Datei (wie im vorherigen Codebeispiel in `Server::CreateSection` gezeigt) und startet das verteilbare Programm mit der `CreateProcess`-Methode. Dabei wird der Pipename mit der Option `-pipe someFileSectionName` übergeben. Der Server sollte Methoden für `OnProgress`, `Send` und `Finished` mit spezifischem Code für die Benutzeroberfläche der Anwendung implementieren.  
  
## <a name="see-also"></a>Siehe auch  
 [Bereitstellungshandbuch für Entwickler](../../../docs/framework/deployment/deployment-guide-for-developers.md)  
 [Bereitstellung](../../../docs/framework/deployment/index.md)
