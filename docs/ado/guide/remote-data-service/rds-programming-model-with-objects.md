---
title: Modelo de programación de RDS con objetos | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS programming model [ADO]
- RDS objects [ADO]
ms.assetid: 07ce0ef0-72f1-48f4-823d-1b65d28c0926
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7e499503541449d35cf17ded36c8a7e358518680
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47737236"
---
# <a name="rds-programming-model-with-objects"></a>Modelo de programación de RDS con objetos
El objetivo de RDS es obtener acceso y actualizar orígenes de datos a través de un intermediario, como IIS. El modelo de programación especifica la secuencia de actividades necesarias para lograr este objetivo. El modelo de objetos especifica los objetos cuyos métodos y propiedades afectan al modelo de programación.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo de Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Deben migrar las aplicaciones que usan RDS a [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
 RDS proporciona los medios para realizar la siguiente secuencia de acciones:  
  
-   Especifique el programa que se invocará en el servidor y obtenga una forma (proxy) para hacer referencia a él desde el cliente ([RDS. DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md)).  
  
-   Invocar el programa de servidor. Pasar parámetros al programa de servidor que identifica el origen de datos y el comando para emitir (proxy o [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)).  
  
-   El programa de servidor obtiene una [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto desde el origen de datos, normalmente mediante ADO. Opcionalmente, el **Recordset** objeto se procesa en el servidor ([RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)).  
  
-   El programa de servidor devuelve el estado final **Recordset** objeto a la aplicación de cliente (proxy).  
  
-   En el cliente, el **Recordset** objeto se coloca en un formulario que se puede usar fácilmente los controles visuales (control visual y **RDS. DataControl**).  
  
-   Cambia a la **Recordset** objeto se envían al servidor y se usa para actualizar el origen de datos (**RDS. DataControl** o **RDSServer.DataFactory**).  
  
## <a name="see-also"></a>Vea también  
 [Resumen del modelo de objetos de RDS](../../../ado/guide/remote-data-service/rds-object-model-summary.md)   
 [Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)   
 [Objeto DataFactory (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)   
 [Objeto DataSpace (RDS)](../../../ado/reference/rds-api/dataspace-object-rds.md)   
 [Escenario RDS](../../../ado/guide/remote-data-service/rds-scenario.md)   
 [Tutorial de RDS](../../../ado/guide/remote-data-service/rds-tutorial.md)   
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [Seguridad y uso de RDS](../../../ado/guide/remote-data-service/rds-usage-and-security.md)


