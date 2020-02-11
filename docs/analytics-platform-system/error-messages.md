---
title: Mensajes de error
description: Los mensajes de error de almacenamiento de datos paralelos (PDW) notifican los errores y problemas detectados por los componentes de PDW y también pueden incluir SQL Server errores que aparecen a través de PDW. Estos mensajes de error utilizan una sintaxis coherente para presentar información. Comprender esta sintaxis le permitirá identificar y corregir los problemas.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 2d89e80a89df53e85ef8d2bf53c369d9e4dc0d49
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "74401162"
---
# <a name="error-messages-in-parallel-data-warehouse"></a>Mensajes de error en almacenamiento de datos paralelos

Los mensajes de error de almacenamiento de datos paralelos (PDW) notifican los errores y problemas detectados por los componentes de PDW y también pueden incluir SQL Server errores que aparecen a través de PDW. Estos mensajes de error utilizan una sintaxis coherente para presentar información. Comprender esta sintaxis le permitirá identificar y corregir problemas en PDW de SQL Server.  
  
## <a name="Basics"></a>Aspectos básicos de los mensajes de error  
Los mensajes de error que se devuelven siguen la misma sintaxis.  
  
`Error_Indicator [SQL_State_Code] [Driver_Details] [QueryID] Message_String`  
  
Estos son los valores posibles para cada campo:  
  
|Campo|Descripción|Ejemplo|  
|---------|---------------|-----------|  
|*Error_Indicator*|La palabra "ERROR" u otro texto que alerta al usuario de un problema.|ERROR|  
|*SQL_State_Code*|Código de estado SQL, de acuerdo con la especificación ODBC. El controlador genera el código de estado SQL adecuado cada vez que devuelve un mensaje a una aplicación. El texto "Microsoft" indica el origen del error.|42000|  
|*Driver_Details*|Detalles dependientes del controlador, como el tipo de controlador utilizado.|Controlador de almacenamiento de datos paralelos ODBC SQL Server 2008 R2|  
|*QueryID*|Identificador único de la consulta. Utilice este valor para buscar información adicional relacionada con el procesamiento de la consulta. Por ejemplo, los detalles de ejecución de la consulta se pueden encontrar en la consola de administración con el ID. de consulta. Para obtener más información, consulte [supervisión del dispositivo mediante la consola de administración](monitor-the-appliance-by-using-the-admin-console.md).<br /><br />Si un QueryID no es aplicable, el texto "Internal" se devuelve al usuario.|QID2377|  
|*Message_String*|Una descripción inteligible del error o del problema. Al devolver SQL Server errores, es el texto del mensaje de SQL Server.|Solo la asignación igual puede aparecer en la lista de conjuntos de una instrucción UPDATE.|  
  
Estos valores de ejemplo se presentarían al usuario de la siguiente manera:  
  
`ERROR [42000] [Microsoft][ODBC SQL Server 2008 R2 Parallel Data Warehouse driver][QID2380]Only equal assignment can appear in the set list of an UPDATE statement.`  
  
## <a name="see-also"></a>Consulte también  
<!-- MISSING LINKS 
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
[Descripción de las alertas de la consola de administración](understanding-admin-console-alerts.md)  
  
