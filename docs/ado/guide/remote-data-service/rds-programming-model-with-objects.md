---
title: Modelo de programación de RDS con objetos | Documentos de Microsoft
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS programming model [ADO]
- RDS objects [ADO]
ms.assetid: 07ce0ef0-72f1-48f4-823d-1b65d28c0926
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3a7e49e00e63ceb330f0da1779ad810516d6a78b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="rds-programming-model-with-objects"></a>Modelo de programación de RDS con objetos
El objetivo de RDS es obtener acceso y actualizar orígenes de datos a través de un intermediario como IIS. El modelo de programación especifica la secuencia de actividades necesarias para lograr este objetivo. El modelo de objetos especifica los objetos cuyos métodos y propiedades afectan al modelo de programación.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar a [servicio de datos de WCF](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
 RDS proporciona los medios para realizar la siguiente secuencia de acciones:  
  
-   Especifique el programa que se invocará en el servidor y obtenga una forma (proxy) para hacer referencia a él desde el cliente ([RDS. DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md)).  
  
-   Invocar el programa de servidor. Pasar parámetros al programa de servidor que identifica el origen de datos y el comando para emitir (proxy o [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)).  
  
-   El programa de servidor obtiene un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto desde el origen de datos, normalmente mediante ADO. Si lo desea, el **Recordset** objeto se procesa en el servidor ([RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)).  
  
-   El programa de servidor devuelve el estado final **Recordset** objeto a la aplicación de cliente (proxy).  
  
-   En el cliente, el **Recordset** objeto se coloca en un formulario que se puede utilizar fácilmente mediante controles visuales (control visual y **RDS. DataControl**).  
  
-   Cambia a la **Recordset** objeto se envían al servidor y se utiliza para actualizar el origen de datos (**RDS. DataControl** o **RDSServer.DataFactory**).  
  
## <a name="see-also"></a>Vea también  
 [Resumen del modelo de objetos de RDS](../../../ado/guide/remote-data-service/rds-object-model-summary.md)   
 [Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)   
 [Objeto DataFactory (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)   
 [Objeto DataSpace (RDS)](../../../ado/reference/rds-api/dataspace-object-rds.md)   
 [Escenario RDS](../../../ado/guide/remote-data-service/rds-scenario.md)   
 [Tutorial RDS](../../../ado/guide/remote-data-service/rds-tutorial.md)   
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [Seguridad y uso de RDS](../../../ado/guide/remote-data-service/rds-usage-and-security.md)


