---
title: Configurar DataFactory para los modos seguros o no restringidos | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: DataFactory configuration in RDS [ADO]
ms.assetid: 8ff24805-dc7a-42ae-b600-5bad0e3f51b8
caps.latest.revision: "15"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0e2fa2afbd767d30f2b85514524acbb438adfe06
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="configuring-datafactory-for-safe-or-unrestricted-modes"></a>Configurar DataFactory para los modos seguros o sin restricciones
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar a [servicio de datos de WCF](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
 De forma predeterminada, ADO se instala con un "safe" [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) configuración. Modo seguro para los componentes de servidor RDS significa que las siguientes afirmaciones son ciertas:  
  
1.  Controlador es necesario con el objeto RDSServer.DataFactory (Esto está asignada por un valor de una clave del registro).  
  
2.  El controlador predeterminado, msdfmap.handler, registrado, presente en la lista de controladores de seguridad, y está marcada como controlador predeterminado.  
  
3.  Archivo MSDFMAP.ini se instala en el directorio de Windows. Debe configurar este archivo según sus necesidades, antes de utilizar RDS en modo de tres niveles.  
  
 Si lo desea, puede configurar una sin restricciones **DataFactory** instalación. **DataFactory** se puede usar directamente sin el controlador personalizado. Los usuarios pueden usar un controlador personalizado mediante la modificación de las cadenas de conexión, pero no es necesario. Para obtener más información acerca de las implicaciones del uso de la **RDSServer.DataFactory** de objetos, consulte [proteger aplicaciones RDS](../../../ado/guide/remote-data-service/securing-rds-applications.md).  
  
 Se ha proporcionado el handsafe.reg del archivo de registro para configurar las entradas del registro de controlador para una configuración segura. Para ejecutar en modo seguro, ejecute handsafe.reg.  
  
 Después de ejecutar handsafe.reg, debe detener y reiniciar el servicio de publicación World Wide Web en el servidor Web escribiendo los siguientes comandos en una ventana del símbolo del sistema: "NET STOP W3SVC" y "NET iniciar W3SVC".  
  
## <a name="see-also"></a>Vea también  
 [Personalización de DataFactory](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [Aspectos básicos de RDS](../../../ado/guide/remote-data-service/rds-fundamentals.md)



