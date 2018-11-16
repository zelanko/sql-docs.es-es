---
title: Objeto DataFactory (RDSServer) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- DataFactory object [ADO]
ms.assetid: e75240c2-b749-471e-b6ea-98cae232efbe
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 189dc8604883d8d91a8bc223c54dd3cb5c14969e
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/13/2018
ms.locfileid: "51599826"
---
# <a name="datafactory-object-rdsserver"></a>Objeto DataFactory (RDSServer)
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo de Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Deben migrar las aplicaciones que usan RDS a [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Este objeto de negocios de servidor predeterminado implementa métodos que proporcionan acceso de lectura y escritura a orígenes de datos para las aplicaciones del lado cliente.  
  
 El **RDSServer.DataFactory** objeto está diseñado como un objeto de automatización del lado servidor que recibe las solicitudes de cliente. En una implementación de Internet, reside en un servidor Web y se crea una instancia por el componente ADISAPI. El **RDSServer.DataFactory** objeto proporciona lectura y orígenes de acceso de escritura a datos especificado, pero no contiene ninguna lógica de reglas de validación o business.  
  
 Si usa un método que está disponible tanto en el **RDSServer.DataFactory** y [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) objetos, el servicio de datos remoto usa el **RDS. DataControl** versión predeterminada. El valor predeterminado, se da por supuesto un escenario básico de programación, donde el **RDSServer.DataFactory** actúa como un objeto de negocios de servidor genérico.  
  
 Si desea que la aplicación Web para controlar el procesamiento del lado servidor específicos de la tarea, puede reemplazar el **RDSServer.DataFactory** con un objeto de negocios personalizada.  
  
 Puede crear objetos de negocios de servidor que llame a la **RDSServer.DataFactory** métodos, como [consulta](../../../ado/reference/rds-api/query-method-rds.md) y [CreateRecordset](../../../ado/reference/rds-api/createrecordset-method-rds.md). Esto resulta útil si desea agregar funcionalidad a los objetos de negocios, pero puede aprovechar tecnologías de servicio de datos remoto existentes.  
  
 El **DataFactory** objeto no es seguro para los scripts que se ejecutan en el lado del cliente.  
  
 El identificador de clase para el **RDSServer.DataFactory** objeto es D 0-9501-00AA00B911A5 9381D8F5-0288-11.  
  
 Esta sección contiene el siguiente tema.  
  
-   [Eventos, métodos y propiedades del objeto DataFactory (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vea también  
 [Objeto DataFactory, método de consulta y ejemplo del método CreateObject (VBScript)](../../../ado/reference/rds-api/datafactory-object-query-method-and-createobject-method-example-vbscript.md)


