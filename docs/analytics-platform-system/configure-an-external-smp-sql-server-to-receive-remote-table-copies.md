---
title: Configurar externo de SMP de SQL Server para recibir copias de la tabla remota (PDW)
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/13/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6bbd2ed6-064e-4b45-b67b-608dc0f2b2bc
caps.latest.revision: "13"
ms.openlocfilehash: 56ef4d9b75e8051a17c276556a321ed19ddcf2d8
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="configure-an-external-smp-sql-server-to-receive-remote-table-copies"></a>Configurar un servidor externo de SMP de SQL para reciben una copia de la tabla remota
Describe cómo configurar una instancia externa de SQL Server para recibir copias de la tabla remota de SQL Server PDW.  
  
En este tema se describe uno de los pasos de configuración para configurar la copia de la tabla remota. Para obtener una lista de todos los pasos de configuración, consulte [copia de tabla remota](remote-table-copy.md).  
  
## <a name="before-you-begin"></a>Antes de comenzar  
Antes de configurar el servidor SQL externo, debe:  
  
-   Tiene un sistema de Windows con SQL Server 2008 Enterprise Edition o una versión posterior lista para instalar o ya instalado. El sistema de Windows debe estar configurado en las instrucciones de [configurar un externo Windows System para recepción remota tabla copias utilizando InfiniBand](configure-an-external-windows-system-to-receive-remote-table-copies-using-infiniband.md).  
  
-   Una cuenta de administrador de Windows con la capacidad de configurar la instancia de SQL Server y el sistema de Windows.  
  
-   Una cuenta de inicio de sesión de SQL Server (si ya está instalado SQL Server) con la capacidad para crear inicios de sesión y conceder permisos en las bases de datos de destino.  
  
## <a name="HowToSQLServer"></a>Configurar un servidor externo de SMP de SQL para reciben una copia de la tabla remota  
La característica de copia de la tabla remota copia tablas desde el dispositivo PDW de SQL Server en una base de datos externo de SMP de SQL Server que se ejecuta en un sistema de Windows. Después de configurar el sistema de Windows externo para recibir copias de la tabla remota, el siguiente paso es instalar y configurar SQL Server en el sistema de Windows.  
  
Para configurar SQL Server, siga estos pasos:  
  
1.  Instalar SQL Server 2008 Enterprise Edition o una versión posterior en el sistema de Windows. Esto se conoce como SMP de SQL Server.  
  
2.  Configurar SQL Server para aceptar conexiones TCP/IP en un puerto TCP fijo. Esta configuración está deshabilitada de forma predeterminada y debe habilitarse para permitir que SQL Server PDW para conectarse al servidor de SQL SMP.  
  
3.  Deshabilite el firewall de Windows o configurar el puerto TCP de SMP SQL Server para que funcione con el firewall de Windows habilitado.  
  
4.  Configurar SQL Server para permitir el modo de autenticación de SQL Server. Los datos en paralelo siempre exportación usa cuentas de SQL Server para la autenticación.  
  
5.  Determinar una cuenta de SQL Server en el servidor de SQL de SMP que se usará para la autenticación. Conceda el privilegio para crear, quitar e insertar datos en tablas en la base de datos de destino para la operación de exportación de datos en paralelo de esa cuenta.  
  
## <a name="BPSQLConfig"></a>Prácticas recomendadas para la configuración del servidor SQL de SMP de copia de la tabla remota  
Al configurar el servidor de SQL de SMP para recibir copias de la tabla remota, utilice las siguientes prácticas recomendadas para mejorar el rendimiento.  
  
1.  Siga las recomendaciones que se documentan en la documentación del producto SQL Server. Por ejemplo, habilite el cifrado de datos. Para obtener más información acerca de cómo proteger SQL Server, vea [proteger SQL Server](../relational-databases/security/securing-sql-server.md) en MSDN.  
  
2.  Utilice el modelo de recuperación simple o masivo.  
  
    Durante los datos en paralelo las operaciones de exportación, los datos son masiva inserta en la tabla de destino recién creado. Para obtener un rendimiento máximo durante la inserción masiva, establezca la base de datos de destino para usar el registro masivo o el modelo de recuperación simple.  
  
3.  Utilice la opción batch_size para reclamar espacio del registro.  
  
    Aunque la recuperación de registro masivo o simple modela uso mínimo de registro para los datos de forma masiva inserta, todavía se produce algún registro. Para evitar que los archivos de registro crezca demasiado grande, utilice la opción de batch_size de SQL Server para recuperar periódicamente el espacio del registro.  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
