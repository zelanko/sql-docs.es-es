---
title: Mensajes de error - almacenamiento de datos paralelos | Microsoft Docs
description: Mensajes de error de almacenamiento de datos (PDW) paralelo notifican los errores y problemas detectados por los componentes PDW y también pueden incluir errores de SQL Server que se exponen a través de PDW. Estos mensajes de error utilizan una sintaxis coherente para presentar información. Descripción de esta sintaxis le permitirá identificar y corregir problemas.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 3ffc7a097845f4652f56d82c572ecfab868d33f1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63042601"
---
# <a name="error-messages-in-parallel-data-warehouse"></a>Mensajes de error en el almacenamiento de datos paralelos

Mensajes de error de almacenamiento de datos (PDW) paralelo notifican los errores y problemas detectados por los componentes PDW y también pueden incluir errores de SQL Server que se exponen a través de PDW. Estos mensajes de error utilizan una sintaxis coherente para presentar información. Descripción de esta sintaxis le permitirá identificar y corregir problemas en PDW de SQL Server.  
  
## <a name="Basics"></a>Conceptos básicos del mensaje de error  
Mensajes de error que se devuelven siguen la misma sintaxis.  
  
`Error_Indicator [SQL_State_Code] [Driver_Details] [QueryID] Message_String`  
  
Estos son los valores posibles para cada campo:  
  
|Campo|Descripción|Ejemplo|  
|---------|---------------|-----------|  
|*Error_Indicator*|La palabra "ERROR" o cualquier otro texto avisa al usuario a un problema.|error|  
|*SQL_State_Code*|El código de estado SQL, según la especificación de ODBC. El controlador genera el código de estado SQL apropiado siempre que devuelve un mensaje a una aplicación. El texto "Microsoft" indica el origen del error.|42000|  
|*Driver_Details*|Detalles de dependiente del controlador, como el tipo de controlador que se utiliza.|Controlador de ODBC SQL Server 2008 R2 Parallel Data Warehouse|  
|*QueryID*|El identificador único para la consulta. Use este valor para buscar información adicional relacionada con el procesamiento de la consulta. Por ejemplo, los detalles de ejecución de consulta pueden encontrarse en la consola de administración con el identificador de consulta. Para obtener más información, consulte [supervisar el dispositivo mediante la consola de administración](monitor-the-appliance-by-using-the-admin-console.md).<br /><br />Si un QueryID no es aplicable, el texto "Interno" se devuelve al usuario.|QID2377|  
|*Message_String*|Una descripción legible del error o problema. Cuando se devuelven errores de SQL Server, se trata el texto del mensaje de SQL Server.|Asignación igual solo puede aparecer en la lista establecida de una instrucción UPDATE.|  
  
Estos valores de ejemplo podrían ser presenta al usuario similar al siguiente:  
  
`ERROR [42000] [Microsoft][ODBC SQL Server 2008 R2 Parallel Data Warehouse driver][QID2380]Only equal assignment can appear in the set list of an UPDATE statement.`  
  
## <a name="see-also"></a>Vea también  
<!-- MISSING LINKS 
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
[Descripción de las alertas de la consola de administración](understanding-admin-console-alerts.md)  
  
