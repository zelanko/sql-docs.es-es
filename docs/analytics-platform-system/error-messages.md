---
title: Mensajes de error (SQL Server PDW)
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: 
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/13/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e6223cba-2dec-4b8a-bc10-e2ef6a821fe0
caps.latest.revision: "9"
ms.openlocfilehash: c9c0ebf9b452fdf2ec54ae84bec34288e73e88aa
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="error-messages"></a>mensajes de error
Mensajes de error de SQL Server PDW notifican los errores y problemas detectados por los componentes de SQL Server PDW y también pueden incluir errores de SQL Server que apareció a través de SQL Server PDW. Estos mensajes de error utilizan una sintaxis coherente para presentar información. Descripción de esta sintaxis le permitirá identificar y corregir problemas en SQL Server PDW.  
  
## <a name="Basics"></a>Conceptos básicos del mensaje de error  
Mensajes de error que se devuelven siguen la misma sintaxis.  
  
`Error_Indicator [SQL_State_Code] [Driver_Details] [QueryID] Message_String`  
  
Estos son los valores posibles para cada campo:  
  
|Campo|Description|Ejemplo|  
|---------|---------------|-----------|  
|*Error_Indicator*|La palabra "ERROR" u otro texto que avisa al usuario un problema.|error|  
|*SQL_State_Code*|El código de estado SQL, según la especificación de ODBC. El controlador genera el código de estado SQL adecuado siempre que devuelve un mensaje a una aplicación. El texto "Microsoft" indica el origen del error.|42000|  
|*Driver_Details*|Detalles de dependiente del controlador, como el tipo de controlador que se utiliza.|Controlador de ODBC SQL Server 2008 R2 Parallel Data Warehouse|  
|*QueryID*|El identificador único para la consulta. Use este valor para buscar información adicional relacionada con el procesamiento de la consulta. Por ejemplo, los detalles de ejecución de consulta pueden encontrarse en la consola de administración con el identificador de la consulta. Para obtener más información, consulte [supervisar el dispositivo mediante la consola de administración](monitor-the-appliance-by-using-the-admin-console.md).<br /><br />Si un QueryID no es aplicable, el texto "Interno" se devuelve al usuario.|QID2377|  
|*Message_String*|Una descripción legible del error o problema. Cuando se devuelven los errores de SQL Server, éste es el texto de mensaje de SQL Server.|Asignación igual de solo puede aparecer en la lista set de una instrucción UPDATE.|  
  
Estos valores de ejemplo podrían ser presenta al usuario similar al siguiente:  
  
`ERROR [42000] [Microsoft][ODBC SQL Server 2008 R2 Parallel Data Warehouse driver][QID2380]Only equal assignment can appear in the set list of an UPDATE statement.`  
  
## <a name="see-also"></a>Vea también  
<!-- MISSING LINKS 
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
[Descripción de las alertas de la consola de administración](understanding-admin-console-alerts.md)  
  
