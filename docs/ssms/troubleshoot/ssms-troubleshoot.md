---
title: Solución de problemas de bloqueo con SSMS
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: dnethi
ms.technology: ssms
ms.topic: conceptual
ms.assetid: c28ffa44-7b8b-4efa-b755-c7a3b1c11ce4
author: markingmyname
ms.author: maghan
ms.custom: seo-lt-2019
ms.date: 09/18/2019
ms.openlocfilehash: f994a44d6fe0f458ae8f8d8be0351421322e7967
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "75243882"
---
# <a name="get-diagnostic-data-after-a-sql-server-management-studio-ssms-crash"></a>Obtención de los datos de diagnóstico después de un bloqueo de SQL Server Management Studio (SSMS)

[!INCLUDE[Applies to](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

## <a name="get-full-memory-dump-after-a-hang-or-crash"></a>Obtención del volcado de memoria completo después de un bloqueo

Obtenga un volcado de memoria completo de SQL Server Management Studio (SSMS) cuando se produce un bloqueo.

Para capturar información de diagnóstico para solucionar un bloqueo de SSMS, siga estos pasos.

1. Descargue [ProcDump](https://technet.microsoft.com/sysinternals/dd996900.aspx).

2. Descomprima la descarga en una carpeta.

3. Abra el símbolo del sistema y ejecute el siguiente comando.

    ```console
    <PathToProcDumpFolder>\procdump.exe -e -h -ma -w ssms.exe
    ```

    Si se le solicita que acepte un contrato de licencia, seleccione *Acepto*.

4. Inicie SSMS, si todavía no se ha iniciado.

5. Reproduzca el problema.

6. El texto debe aparecer en la ventana de símbolo del sistema cmd para escribir el archivo de volcado de memoria; espere a que termine.

7. Cree una carpeta y copie el archivo *.dmp que se escribe en esa carpeta.

8. Copie los archivos siguientes en la misma carpeta.

    "C:\Windows\Microsoft.NET\Framework\v4.0.30319\mscordacwks.dll"  "C:\Windows\Microsoft.NET\Framework\v4.0.30319\SOS.dll"  "C:\Windows\Microsoft.NET\Framework\v4.0.30319\clr.dll"

9. Comprima la carpeta.

## <a name="get-full-memory-dump-for-an-outofmemoryexception"></a>Obtención de un volcado de memoria completo para una excepción OutOfMemoryException

Obtenga un volcado de memoria completo de SSMS cuando se inicia una excepción OutOfMemoryException.

Puede obtener un volcado de memoria completo con cualquier excepción administrada.

Para capturar información de diagnóstico para solucionar problemas de una excepción OutOfMemoryException desde SSMS, siga estos pasos.

1. Descargue [ProcDump](https://technet.microsoft.com/sysinternals/dd996900.aspx).

2. Descomprima la descarga en una carpeta.

3. Abra el símbolo del sistema y ejecute el siguiente comando:

    ```console
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
