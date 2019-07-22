---
title: Solución de problemas de un bloqueo con SQL Server Management Studio (SSMS)
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: dnethi
ms.technology: ssms
ms.topic: conceptual
ms.assetid: c28ffa44-7b8b-4efa-b755-c7a3b1c11ce4
author: markingmyname
ms.author: maghan
manager: jroth
ms.custom: ''
ms.date: 07/01/2019
ms.openlocfilehash: 41f140a00669e1b5809b83b369f86ba8b277a37e
ms.sourcegitcommit: aeb2273d779930e76b3e907ec03397eab0866494
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/10/2019
ms.locfileid: "67716773"
---
# <a name="get-diagnostic-data-after-a-sql-server-management-studio-ssms-crash"></a>Obtención de los datos de diagnóstico después de un bloqueo de SQL Server Management Studio (SSMS)

[!INCLUDE[Se aplica a](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)

## <a name="get-full-memory-dump-after-a-hang-or-crash"></a>Obtención del volcado de memoria completo después de un bloqueo

Obtenga un volcado de memoria completo de SQL Server Management Studio (SSMS) cuando se produce un bloqueo.

Para capturar información de diagnóstico para solucionar un bloqueo de SSMS, siga estos pasos.

1. Descargue [ProcDump](https://technet.microsoft.com/sysinternals/dd996900.aspx).

2. Descomprima la descarga en una carpeta.

3. Abra el símbolo del sistema y ejecute el siguiente comando.

    ```command prompt  <PathToProcDumpFolder>\procdump.exe -e -h -ma -w ssms.exe
    ```

    If it prompts you to accept a license agreement, select *Agree*.

4. Start SSMS, if it hasn't started already.

5. Reproduce the issue.

6. The text should appear in the cmd prompt about writing the dump file, wait for that to finish.

7. Create a new folder and copy the *.dmp file that is written out to that folder.

8. Copy the following files into the same folder.

    "C:\Windows\Microsoft.NET\Framework\v4.0.30319\mscordacwks.dll"
    "C:\Windows\Microsoft.NET\Framework\v4.0.30319\SOS.dll"
    "C:\Windows\Microsoft.NET\Framework\v4.0.30319\clr.dll"

9. Zip up the folder

## Get full memory dump for an OutOfMemoryException

Get a full memory dump of SSMS when it throws an OutOfMemoryException.

You can get a full memory dump with any managed exception.

To capture diagnostic information to troubleshoot an OutOfMemoryException from SSMS, follow the steps below.

1. Download [ProcDump](https://technet.microsoft.com/sysinternals/dd996900.aspx).

2. Unzip the download into a folder.

3. Open Command Prompt and run the following command.

    ```command prompt
    <PathToProcDumpFolder>\procdump.exe -e 1 -f System.OutOfMemoryException -ma -w ssms.exe
    ```

    Si se le solicita que acepte un contrato de licencia, seleccione *Acepto*.

4. Inicie SQL Server Management Studio si no se ha iniciado ya.

5. Reproduzca el problema.

6. El texto debe aparecer en la ventana de símbolo del sistema cmd para escribir el archivo de volcado de memoria; espere a que termine.

7. Cree una carpeta y copie el archivo *.dmp que se escribe en esa carpeta.

8. Copie los archivos siguientes en la misma carpeta.

    "C:\Windows\Microsoft.NET\Framework\v4.0.30319\mscordacwks.dll"  "C:\Windows\Microsoft.NET\Framework\v4.0.30319\SOS.dll"  "C:\Windows\Microsoft.NET\Framework\v4.0.30319\clr.dll"

9. Comprima la carpeta.