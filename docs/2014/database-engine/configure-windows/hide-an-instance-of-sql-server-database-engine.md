---
title: Ocultar una instancia del Motor de base de datos de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 08/19/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- Database Engine [SQL Server], hiding instances
- hiding instances of Database Engine
ms.assetid: 392de21a-57fa-4a69-8237-ced8ca86ed1d
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 631d55e1f8921601f25f2b2d8a14f00d11bd0947
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62782010"
---
# <a name="hide-an-instance-of-sql-server-database-engine"></a>Ocultar una instancia del motor de base de datos de SQL Server
  En este tema se describe cómo ocultar una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)] en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] utilizando el Administrador de configuración de SQL Server. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utiliza el servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser para enumerar las instancias del [!INCLUDE[ssDE](../../includes/ssde-md.md)] instaladas en el equipo. De esta manera, las aplicaciones cliente pueden buscar un servidor y los clientes pueden distinguir las distintas instancias del [!INCLUDE[ssDE](../../includes/ssde-md.md)] que están instaladas en el mismo equipo. Puede usar el procedimiento siguiente para evitar que el servicio SQL Server Browser exponga una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)] a los equipos cliente que intenten buscarla mediante el botón **Examinar** .  
  
##  <a name="SSMSProcedure"></a> Usar el Administrador de configuración de SQL Server  
  
#### <a name="to-hide-an-instance-of-the-sql-server-database-engine"></a>Para ocultar una instancia del motor de base de datos de SQL Server  
  
1.  En **Administrador de configuración de SQL Server**, expanda **Configuración de red de SQL Server**, haga clic con el botón derecho en **Protocolos de** *\<instancia de servidor>* y seleccione **Propiedades**.  
  
2.  En la pestaña **Marcas** , en el cuadro **HideInstance** , seleccione **Sí**y, a continuación, haga clic en **Aceptar** para cerrar el cuadro de diálogo. El cambio se aplica de forma inmediata para las conexiones nuevas.  
  
## <a name="remarks"></a>Comentarios  
 Si oculta una instancia con nombre, deberá proporcionar el número de puerto en la cadena de conexión para conectarse a la instancia oculta, aunque se esté ejecutando el servicio de explorador. Se recomienda utilizar un puerto estático en lugar de un puerto dinámico para la instancia con nombre oculta.  
  Para obtener más información, vea [Configurar un servidor para que escuche en un puerto TCP específico &#40;Administrador de configuración de SQL Server&#41;](configure-a-server-to-listen-on-a-specific-tcp-port.md).  
  
### <a name="clustering"></a>Agrupación en clústeres  
 Si oculta una instancia con nombre en clúster, es posible que el servicio de clúster no pueda conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esto provocará el error de la comprobación **IsAlive** de la instancia en clúster y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se desconectará. Se recomienda crear un alias en todos los nodos de la instancia en clúster para reflejar el puerto estático que configuró para la instancia.  
 Para obtener más información, vea [Crear o eliminar un alias de servidor para que lo utilice un cliente &#40;Administrador de configuración de SQL Server&#41;](create-or-delete-a-server-alias-for-use-by-a-client.md).  
  
 Si oculta una instancia con nombre agrupada, es posible que el servicio de clúster no pueda conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] si la clave del Registro **LastConnect** (**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SNI11.0\LastConnect**) tiene un puerto distinto del puerto en el que escucha [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Si el servicio de clúster no puede establecer la conexión con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], podría aparecer un error similar al siguiente:  
**Identificador del evento: 1001: nombre del evento: interbloqueo de recurso de clústeres de conmutación por error.**  
  
## <a name="see-also"></a>Vea también  
 [Configuración de red del servidor](server-network-configuration.md)   
 [Descripción de las conexiones de cliente del servidor virtual de SQL](https://support.microsoft.com/kb/273673)   
 [Cómo asignar un puerto estático a una instancia con nombre de SQL Server y evitar un problema común](https://blogs.msdn.com/b/arvindsh/archive/2012/09/08/how-to-assign-a-static-port-to-a-sql-server-named-instance-and-avoid-a-common-pitfall.aspx)  
  
  
