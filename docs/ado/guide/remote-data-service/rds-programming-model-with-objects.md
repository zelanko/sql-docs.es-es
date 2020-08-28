---
description: Modelo de programación de RDS con objetos
title: Modelo de programación de RDS con objetos | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS programming model [ADO]
- RDS objects [ADO]
ms.assetid: 07ce0ef0-72f1-48f4-823d-1b65d28c0926
author: rothja
ms.author: jroth
ms.openlocfilehash: 2658b8b7591284f1624f3649e3980db6e2022726
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2020
ms.locfileid: "88977956"
---
# <a name="rds-programming-model-with-objects"></a>Modelo de programación de RDS con objetos
El objetivo de RDS es obtener acceso a los orígenes de datos y actualizarlos a través de un intermediario como IIS. El modelo de programación especifica la secuencia de actividades necesaria para lograr este objetivo. El modelo de objetos de especifica los objetos cuyos métodos y propiedades afectan al modelo de programación.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, los componentes de servidor RDS ya no se incluyen en el sistema operativo Windows (consulte la guía de compatibilidad de Windows 8 y [Windows server 2012](https://www.microsoft.com/download/details.aspx?id=27416) para obtener más detalles). Los componentes de cliente RDS se quitarán en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar al [servicio de datos de WCF](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 RDS proporciona los medios para realizar la siguiente secuencia de acciones:  
  
-   Especifique el programa que se va a invocar en el servidor y obtenga una forma (proxy) para hacer referencia a él desde el cliente ([RDS. DataSpace](../../reference/rds-api/dataspace-object-rds.md)).  
  
-   Invoque el programa de servidor. Pase los parámetros al programa de servidor que identifica el origen de datos y el comando que se va a emitir (proxy o [RDS. DataControl](../../reference/rds-api/datacontrol-object-rds.md)).  
  
-   El programa de servidor obtiene un objeto de [conjunto de registros](../../reference/ado-api/recordset-object-ado.md) del origen de datos, normalmente mediante ADO. Opcionalmente, el objeto de **conjunto de registros** se procesa en el servidor ([RDSServer. DataFactory](../../reference/rds-api/datafactory-object-rdsserver.md)).  
  
-   El programa de servidor devuelve el último objeto de **conjunto de registros** a la aplicación cliente (proxy).  
  
-   En el cliente, el objeto de **conjunto de registros** se coloca en un formulario que se puede usar fácilmente en los controles visuales (control visual y **RDS). DataControl**).  
  
-   Los cambios en el objeto de **conjunto de registros** se devuelven al servidor y se usan para actualizar el origen de datos (**RDS. DataControl** o **RDSServer. DataFactory**).  
  
## <a name="see-also"></a>Consulte también  
 [Resumen del modelo de objetos RDS](./rds-object-model-summary.md)   
 [Objeto DataControl (RDS)](../../reference/rds-api/datacontrol-object-rds.md)   
 [Objeto DataFactory (RDSServer)](../../reference/rds-api/datafactory-object-rdsserver.md)   
 [Objeto DataSpace (RDS)](../../reference/rds-api/dataspace-object-rds.md)   
 [Escenario de RDS](./rds-scenario.md)   
 [Tutorial de RDS](./rds-tutorial.md)   
 [Objeto de conjunto de registros (ADO)](../../reference/ado-api/recordset-object-ado.md)   
 [Seguridad y uso de RDS](./rds-usage-and-security.md)