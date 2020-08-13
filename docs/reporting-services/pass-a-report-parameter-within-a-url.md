---
title: Pasar un parámetro de informe en una dirección URL | Microsoft Docs
description: Obtenga información sobre cómo pasar parámetros de informe directamente al motor de procesamiento de informes si los incluye en una dirección URL de informe.
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
helpviewer_keywords:
- URL access [Reporting Services], passing parameters
- passing parameters [Reporting Services]
ms.assetid: f93a94cc-27b5-435a-aa85-69e6ec6459ad
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 2eca700dbe01abdb94ff2b60763db840fc4f3d53
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/28/2020
ms.locfileid: "87242935"
---
# <a name="pass-a-report-parameter-within-a-url"></a>Pasar un parámetro de informe en una dirección URL
  Puede pasar parámetros de informe a un informe incluyéndolos en un informe URL. Estos parámetros de dirección URL no tienen prefijo porque se pasan directamente al motor de procesamiento de informes.  

> [!NOTE]
> La integración de Reporting Services con SharePoint ya no está disponible a partir de SQL Server 2016.
  
> [!IMPORTANT]  
>  Es importante que la dirección URL incluya la sintaxis de proxy de `_vti_bin` para enrutar la solicitud a través de SharePoint y el proxy HTTP de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] . El proxy agrega algún contexto a la solicitud HTTP, contexto que es necesario para garantizar la correcta ejecución del informe para los servidores de informes de modo de SharePoint.  
>   
>  Si no incluye la sintaxis de proxy, tendrá que agregar *rp:* como prefijo del parámetro.  
  
 Todos los parámetros de consulta pueden tener parámetros de informe correspondientes. Para pasar un parámetro de consulta a un informe, pase el parámetro de informe correspondiente. Para más información, vea [Crear una consulta en el Diseñador de consultas relacionales &#40;Generador de informes y SSRS&#41;](../reporting-services/report-data/build-a-query-in-the-relational-query-designer-report-builder-and-ssrs.md).  
  
> [!IMPORTANT]
>  Los parámetros de informe distinguen entre mayúsculas y minúsculas.  
> 
> [!NOTE]
>  Los parámetros de informe distinguen mayúsculas de minúsculas y usan los caracteres especiales siguientes:  
> 
>  -   Cualquier carácter de espacio en blanco en la cadena de dirección URL se reemplaza con los caracteres "% 20", según los estándares de codificación de direcciones URL.  
> -   Un carácter de espacio en la parte del parámetro de la dirección URL se reemplaza con un carácter más (+).  
> -   Un punto y coma en cualquier parte de la cadena se reemplaza con los caracteres “%3A”.  
> -   Los exploradores deberían realizar de forma automática la codificación de dirección URL apropiada. No tiene que codificar ninguno de los caracteres manualmente.  
  
 Para establecer un parámetro de informe dentro de una dirección URL, use la siguiente sintaxis:  
  
```  
  
parameter=value  
```  
  
 Por ejemplo, para especificar dos parámetros, "ReportMonth" y "ReportYear", definidos en un informe, use las direcciones URL siguientes para un servidor de informes en modo nativo:  
  
```  
https://myrshost/ReportServer?/AdventureWorks 2008R2/Employee_Sales_Summary_2008R2&ReportMonth=3&ReportYear=2008  
```  
  
 Por ejemplo, para especificar los mismos parámetros definidos en un informe, use las direcciones URL siguientes para un servidor de informes en modo integrado de SharePoint: Anote `/_vti_bin`:  
  
```  
https://myspsite/subsite/_vti_bin/reportserver?https://myspsite/subsite/AdventureWorks 2008R2/Employee_Sales_Summary_2008R2.rdl&ReportMonth=3&ReportYear=2008  
```  
  
 Para pasar un valor NULL para un parámetro, use la siguiente sintaxis:  
  
```  
  
parameter  
:isnull=true  
  
```  
  
 Por ejemplo,  
  
```  
SalesOrderNumber:isnull=true  
```  
  
 Para pasar un valor **Boolean** , use 0 para FALSE o 1 para TRUE. Para pasar un valor **Float** , incluya el separador decimal correspondiente a la configuración regional del servidor.  
  
> [!NOTE]  
>  Si un informe contiene un parámetro de informe con un valor predeterminado y el valor de la propiedad **Prompt** es **false** (es decir, la propiedad Preguntar al usuario no está seleccionada en el Administrador de informes), no puede pasar un valor dentro de una dirección URL para ese parámetro de informe. Esto proporciona a los administradores una opción para evitar que los usuarios finales agreguen o modifiquen los valores de ciertos parámetros de informe.  
  
##  <a name="additional-examples"></a><a name="bkmk_examples"></a> Otros ejemplos  
 En el ejemplo siguiente de dirección URL se incluyen espacios en blanco y varios parámetros  
  
-   El nombre de carpeta de "Equipo de educación de usuarios de SQL Server" incluye espacios en blanco y, por tanto, el signo "+" reemplaza cada espacio.  
  
-   El nombre de informe "informe de proyecto de equipo" incluye espacios en blanco y, por tanto, el signo "+" reemplaza cada espacio.  
  
-   Pasa dos parámetros de "teamgrouping2" con un valor de "xgroup" y "teamgrouping1" con un valor de "ygroup".  
  
```  
https://myserver/Reportserver?/SQL+Server+User+Education+Team/_ContentTeams/folder123/team+project+report&teamgrouping2=xgroup&teamgrouping1=ygroup  
```  
  
 En el ejemplo siguiente de dirección URL se incluye un parámetro "OrderID" con varios valores. El formato de un parámetro multivalor es repetir el nombre del parámetro para cada valor.  
  
```  
https://myserver/Reportserver?/SQL+Server+User+Education+Team/_ContentTeams/folder123/team+project+report&teamgrouping2=xgroup&teamgrouping1=ygroup&OrderID=747&OrderID=787&OrderID=12  
```  
  
 En el siguiente ejemplo de dirección URL se pasa un único parámetro de *SellStartDate* con el valor "7/1/2005" para un servidor de informes en modo nativo.  
  
```  
https://myserver/ReportServer/Pages/ReportViewer.aspx?%2fProduct_and_Sales_Report_AdventureWorks&SellStartDate=7/1/2005  
```  
  
## <a name="see-also"></a>Consulte también  
 [Acceso URL &#40;SSRS&#41;](../reporting-services/url-access-ssrs.md)   
 [Referencia de parámetros de acceso URL](../reporting-services/url-access-parameter-reference.md)  
  
  
