---
title: Objeto DataFactory (RDSServer) | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
helpviewer_keywords: DataFactory object [ADO]
ms.assetid: e75240c2-b749-471e-b6ea-98cae232efbe
caps.latest.revision: "15"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3df928f2c2ac6735bc1654b1f9eacb02cb202b42
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="datafactory-object-rdsserver"></a>Objeto DataFactory (RDSServer)
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar a [servicio de datos de WCF](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Este objeto de negocio de servidor predeterminado implementa métodos que proporcionan acceso a datos de lectura/escritura a los orígenes de datos especificados para las aplicaciones de cliente.  
  
 El **RDSServer.DataFactory** objeto está diseñado como un objeto de automatización de servidor que recibe solicitudes de cliente. En una implementación de Internet, reside en un servidor Web y se crea una instancia por el componente ADISAPI. El **RDSServer.DataFactory** objeto proporciona lectura y acceso de escritura a los datos especificados orígenes, pero no contiene ninguna lógica de reglas de validación o business.  
  
 Si usa un método que está disponible tanto en el **RDSServer.DataFactory** y [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) objetos, el servicio de datos remotos utiliza el **RDS. DataControl** versión de forma predeterminada. El valor predeterminado, se da por supuesto un escenario de programación básico, donde el **RDSServer.DataFactory** actúa como un objeto de negocio de servidor genérico.  
  
 Si desea que la aplicación Web para controlar el procesamiento de servidor específico de la tarea, puede reemplazar el **RDSServer.DataFactory** con un objeto comercial personalizado.  
  
 Puede crear objetos de negocio de servidor que llame a la **RDSServer.DataFactory** métodos, como [consulta](../../../ado/reference/rds-api/query-method-rds.md) y [CreateRecordset](../../../ado/reference/rds-api/createrecordset-method-rds.md). Esto resulta útil si desea agregar funcionalidad a los objetos comerciales, pero aprovechar las ventajas de las tecnologías de servicio de datos remotos existentes.  
  
 El **DataFactory** objeto no es seguro para las secuencias de comandos que se ejecutan en el lado del cliente.  
  
 El identificador de clase para la **RDSServer.DataFactory** objeto es 9381D8F5-0288-11 D 0-9501-00AA00B911A5.  
  
 Esta sección contiene el siguiente tema.  
  
-   [Eventos, métodos y propiedades del objeto DataFactory (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vea también  
 [Objeto DataFactory, método de consulta y ejemplo del método CreateObject (VBScript)](../../../ado/reference/rds-api/datafactory-object-query-method-and-createobject-method-example-vbscript.md)


