---
title: Configurar SQL Server para recibir copias de la tabla remota - almacenamiento de datos paralelos | Microsoft Docs
description: Describe cómo configurar una instancia de SQL Server de SMP externa para recibir copias de la tabla remota de almacenamiento de datos paralelos.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: ae6799d468d57dec04046b443c613823c0a8cb8c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63224685"
---
# <a name="configure-an-external-smp-sql-server-to-receive-remote-table-copies---parallel-data-warehouse"></a>Configurar un servidor SQL de SMP externo para recibir copias de la tabla remota - almacenamiento de datos paralelos
Describe cómo configurar una instancia externa de SQL Server para recibir copias de la tabla remota de almacenamiento de datos paralelos.  

Este tema describe uno de los pasos de configuración para configurar la copia de la tabla remota. Para obtener una lista de todos los pasos de configuración, consulte [copia remota de la tabla](remote-table-copy.md).  
  
## <a name="before-you-begin"></a>Antes de empezar  
Antes de configurar el servidor SQL Server externo, debe:  
  
-   Tiene un sistema de Windows con SQL Server 2008 Enterprise Edition o una versión posterior lista para ser instalado o ya instalado. El sistema de Windows debe estar configurado según las instrucciones de [configurar un externo Windows del sistema para recibir remoto tabla copias utilizando InfiniBand](configure-an-external-windows-system-to-receive-remote-table-copies-using-infiniband.md).  
  
-   Una cuenta de administrador de Windows con la capacidad de configurar la instancia de SQL Server y el sistema de Windows.  
  
-   Una cuenta de inicio de sesión de SQL Server (si ya está instalado SQL Server) con la capacidad de crear los inicios de sesión y conceder permisos en las bases de datos de destino.  
  
## <a name="HowToSQLServer"></a>Configurar un servidor SQL de SMP externo para recibir copias de la tabla remota  
La característica de copia de la tabla remota copia tablas desde el dispositivo PDW de SQL Server en una base de datos de SQL Server de SMP externo que se ejecuta en un sistema de Windows. Después de configurar el sistema externo de Windows para recibir copias de la tabla remota, el siguiente paso es instalar y configurar SQL Server en el sistema de Windows.  
  
Para configurar SQL Server, siga estos pasos:  
  
1.  Instalar SQL Server 2008 Enterprise Edition o una versión posterior en el sistema de Windows. Esto se conoce como el servidor SQL Server de SMP.  
  
2.  Configurar SQL Server para aceptar conexiones TCP/IP en un puerto TCP fijo. Esta configuración está deshabilitada de forma predeterminada y debe habilitarse para permitir PDW de SQL Server para conectarse a SQL Server de SMP.  
  
3.  Deshabilite el firewall de Windows o configure el puerto TCP de SQL Server de SMP para que funcione con el firewall de Windows habilitado.  
  
4.  Configurar SQL Server para permitir el modo de autenticación de SQL Server. Los datos en paralelo exportarán siempre utiliza cuentas de SQL Server para la autenticación.  
  
5.  Determinar una cuenta de SQL Server en el servidor de SQL de SMP que se usará para la autenticación. Conceda el privilegio para crear, quitar e insertar datos en tablas en la base de datos de destino para la operación de exportación de datos paralelos de esa cuenta.  
  
## <a name="BPSQLConfig"></a>Procedimientos recomendados para la configuración del servidor SQL de SMP de copia de la tabla remota  
Al configurar SQL Server para recibir copias de la tabla remota SMP, use los siguientes procedimientos recomendados para mejorar el rendimiento.  
  
1.  Siga los procedimientos recomendados como se documenta en la documentación del producto SQL Server. Por ejemplo, habilitar el cifrado de datos. Para obtener más información acerca de cómo proteger SQL Server, vea [Securing SQL Server](../relational-databases/security/securing-sql-server.md) en MSDN.  
  
2.  Utilice el modelo de recuperación simple o masivo.  
  
    Durante los datos en paralelo las operaciones de exportación, están de datos masiva inserta en la tabla de destino recién creado. Para obtener un rendimiento máximo durante la inserción masiva, establezca la base de datos de destino para usar el registro masivo o el modelo de recuperación simple.  
  
3.  Utilice la opción batch_size para reclamar espacio del registro.  
  
    Aunque la recuperación simple o masivo modela uso mínimo de registro para los datos insertado de forma masiva, todavía se produce algún registro. Para evitar que los archivos de registro crezca demasiado grande, use la opción de SQL Server batch_size periódicamente reclamar espacio del registro.  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
