---
title: Ejecutar un archivo de script de Reporting Services | Microsoft Docs
description: Vea ejemplos de cómo ejecutar un archivo de script de Reporting Services desde el símbolo del sistema mediante el entorno de script de Reporting Services (RS.exe).
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: tools
ms.topic: conceptual
helpviewer_keywords:
- scripts [Reporting Services], running
ms.assetid: 0de4995c-85ec-4d4c-aaef-fbd30edfb20f
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 79d96354c497977b780078ccbe94b25738b0f522
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/22/2020
ms.locfileid: "86914798"
---
# <a name="run-a-reporting-services-script-file"></a>Ejecutar un archivo de script de Reporting Services
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] los archivos de script se ejecutan desde el símbolo del sistema con el entorno de scripts de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] (RS.exe). RS.exe tiene muchos argumentos del símbolo del sistema disponibles para su uso. Para más información sobre las opciones del símbolo del sistema, vea [Utilidad RS.exe &#40;SSRS&#41;](../../reporting-services/tools/rs-exe-utility-ssrs.md). Para obtener mas muestras de script, vea [Muestras de productos de SQL Server Reporting Services](https://go.microsoft.com/fwlink/?LinkId=177889).  
  
## <a name="sample-command-lines"></a>Líneas de comandos de ejemplo  
  
-   Ejecute Script.rss en el entorno de script que designa el servidor de informes de destino. De forma predeterminada, se aplica la Autenticación de Windows:  
  
    ```  
    rs -i Script.rss -s https://servername/reportserver  
    ```  
  
-   Ejecute Script.rss en el entorno de script que especifica un nombre de usuario y contraseña para autenticar las llamadas del servicio web:  
  
    ```  
    rs -i Script.rss -s https://servername/reportserver -u myusername -p mypassword  
    ```  
  
-   Ejecute Script.rss en el entorno de script que especifica un tiempo de espera de servidor de 30 segundos:  
  
    ```  
    rs -i Script.rss -s https://servername/reportserver -l 30  
    ```  
  
-   Ejecute Script.rss en el entorno de script que especifica una variable de script global denominada *report*.  
  
    ```  
    rs -i Script.rss -s https://servername/reportserver -v report="Company Sales"  
    ```  
  
-   Ejecute Script.rss en el entorno de script que especifica que las operaciones del servicio web del archivo de script se ejecutan como lote.  
  
    ```  
    rs -i Script.rss -s https://servername/reportserver -b  
    ```  
  
## <a name="see-also"></a>Consulte también  
 [Referencia técnica &#40;SSRS&#41;](../../reporting-services/technical-reference-ssrs.md)  
  
  
