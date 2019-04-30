---
title: Configuración de DataFactory para los modos seguros o sin restricciones | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- DataFactory configuration in RDS [ADO]
ms.assetid: 8ff24805-dc7a-42ae-b600-5bad0e3f51b8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 32b87f7ddcd871748adbba66eb0a64a10204f0c1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63214851"
---
# <a name="configuring-datafactory-for-safe-or-unrestricted-modes"></a>Configuración de DataFactory para los modos seguro o sin restricciones
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo de Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Deben migrar las aplicaciones que usan RDS a [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 De forma predeterminada, ADO se instala con un "safe" [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) configuración. Modo seguro para los componentes de servidor RDS significa que los siguientes son ciertas:  
  
1.  Controlador es necesario con RDSServer.DataFactory (Esto está asignada por un valor de clave del registro).  
  
2.  El controlador predeterminado, msdfmap.handler, está registrado, presente en la lista de controladores de safe y marcada como controlador predeterminado.  
  
3.  Archivo MSDFMAP.ini se instala en el directorio de Windows. Debe configurar este archivo según sus necesidades, antes de utilizar RDS en modo de tres niveles.  
  
 Opcionalmente, puede configurar sin restricciones **DataFactory** instalación. **DataFactory** se pueden usar directamente sin el controlador personalizado. Los usuarios todavía pueden usar un controlador personalizado mediante la modificación de las cadenas de conexión, pero no es necesario. Para obtener más información acerca de las implicaciones del uso de la **RDSServer.DataFactory** de objetos, consulte [proteger aplicaciones RDS](../../../ado/guide/remote-data-service/securing-rds-applications.md).  
  
 Se ha proporcionado el handsafe.reg del archivo de registro para configurar las entradas de registro del controlador para una configuración segura. Para ejecutar en modo seguro, ejecute handsafe.reg.  
  
 Después de ejecutar handsafe.reg, debe detener y reiniciar el servicio de publicación World Wide Web en el servidor Web escribiendo los siguientes comandos en una ventana del símbolo del sistema: "NET STOP W3SVC" y "NET iniciar W3SVC".  
  
## <a name="see-also"></a>Vea también  
 [Personalización de DataFactory](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [Aspectos básicos de RDS](../../../ado/guide/remote-data-service/rds-fundamentals.md)



