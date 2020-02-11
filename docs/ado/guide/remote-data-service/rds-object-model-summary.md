---
title: Resumen del modelo de objetos RDS | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS objects [ADO], object model summary
- RDS object model [ADO]
ms.assetid: 909f9af7-31db-4eec-ad52-650ce74dac2f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6c455d816b3ba5a9606d09e3b05e54583e11ca41
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67922531"
---
# <a name="rds-object-model-summary"></a>Resumen del modelo de objetos de RDS
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, los componentes de servidor RDS ya no se incluyen en el sistema operativo Windows (consulte la guía de compatibilidad de Windows 8 y [Windows server 2012](https://www.microsoft.com/download/details.aspx?id=27416) para obtener más detalles). Los componentes de cliente RDS se quitarán en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar al [servicio de datos de WCF](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
|Object|Descripción|  
|------------|-----------------|  
|[ActiveX. DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md)|Este objeto contiene un método para obtener un proxy de servidor. El proxy puede ser el predeterminado o un programa de servidor personalizado (objeto comercial). El programa de servidor se puede invocar en Internet, en una intranet, en una red de área local o en una biblioteca de vínculos dinámicos local.<br /><br /> El objeto **DataSpace** es seguro para el scripting.|  
|[RDSServer. DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)|Este objeto representa el programa de servidor predeterminado. Ejecuta la recuperación de datos y el comportamiento de actualización de RDS predeterminados.<br /><br /> El objeto **DataFactory** no es seguro para el scripting.|  
|[ActiveX. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)|Este objeto puede invocar automáticamente a **RDS. Objetos DataSpace** y **RDSServer. DataFactory** .<br /><br /> Utilice este objeto para invocar la recuperación de datos predeterminada de RDS o el comportamiento de actualización.<br /><br /> Este objeto también proporciona los medios para que los controles visuales tengan acceso al objeto de **conjunto de registros** devuelto.<br /><br /> El objeto **DataControl** es seguro para el scripting.|  
  
## <a name="see-also"></a>Consulte también  
 [Aspectos básicos de RDS](../../../ado/guide/remote-data-service/rds-fundamentals.md)   
 [Escenario de RDS](../../../ado/guide/remote-data-service/rds-scenario.md)   
 [Tutorial de RDS](../../../ado/guide/remote-data-service/rds-tutorial.md)   
 [Seguridad y uso de RDS](../../../ado/guide/remote-data-service/rds-usage-and-security.md)


