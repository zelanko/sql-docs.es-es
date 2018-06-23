---
title: Ejecutar un archivo de script de Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- scripts [Reporting Services], running
ms.assetid: 0de4995c-85ec-4d4c-aaef-fbd30edfb20f
caps.latest.revision: 35
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: 06a2631c737654ad1fc0041f5a919a57db4acc43
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36203340"
---
# <a name="run-a-reporting-services-script-file"></a>Ejecutar un archivo de script de Reporting Services
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] los archivos de script se ejecutan desde el símbolo del sistema con el entorno de scripts de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] (RS.exe). RS.exe tiene muchos argumentos del símbolo del sistema disponibles para su uso. Para más información sobre las opciones del símbolo del sistema, vea [Utilidad RS.exe &#40;SSRS&#41;](rs-exe-utility-ssrs.md). Para obtener mas muestras de script, vea [Muestras de productos de SQL Server Reporting Services](http://go.microsoft.com/fwlink/?LinkId=177889).  
  
## <a name="sample-command-lines"></a>Líneas de comandos de ejemplo  
  
-   Ejecute Script.rss en el entorno de script que designa el servidor de informes de destino. De forma predeterminada, se aplica la Autenticación de Windows:  
  
    ```  
    rs –i Script.rss -s http://servername/reportserver  
    ```  
  
-   Ejecute Script.rss en el entorno de script que especifica un nombre de usuario y contraseña para autenticar las llamadas del servicio web:  
  
    ```  
    rs –i Script.rss -s http://servername/reportserver -u myusername -p mypassword  
    ```  
  
-   Ejecute Script.rss en el entorno de script que especifica un tiempo de espera de servidor de 30 segundos:  
  
    ```  
    rs –i Script.rss -s http://servername/reportserver -l 30  
    ```  
  
-   Ejecute Script.rss en el entorno de script que especifica una variable de script global denominada *report*.  
  
    ```  
    rs –i Script.rss -s http://servername/reportserver -v report="Company Sales"  
    ```  
  
-   Ejecute Script.rss en el entorno de script que especifica que las operaciones del servicio web del archivo de script se ejecutan como lote.  
  
    ```  
    rs –i Script.rss -s http://servername/reportserver -b  
    ```  
  
## <a name="see-also"></a>Vea también  
 [Referencia técnica &#40;SSRS&#41;](../technical-reference-ssrs.md)  
  
  