---
title: Configurar SQL Server para recibir copias de la tabla remota
description: Describe cómo configurar una instancia de SQL Server SMP externa para recibir copias de la tabla remota de almacenamiento de datos paralelos.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 3e5475e86582ede2e6fa7ca5a302bba7ee74faa3
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "74401327"
---
# <a name="configure-an-external-smp-sql-server-to-receive-remote-table-copies---parallel-data-warehouse"></a>Configuración de una SQL Server SMP externa para recibir copias de tablas remotas: almacenamiento de datos paralelos
Describe cómo configurar una instancia de SQL Server externa para recibir copias de la tabla remota de almacenamiento de datos paralelos.  

En este tema se describe uno de los pasos de configuración para configurar la copia de tabla remota. Para obtener una lista de todos los pasos de configuración, consulte [copia de tabla remota](remote-table-copy.md).  
  
## <a name="before-you-begin"></a>Antes de empezar  
Para poder configurar la SQL Server externa, debe:  
  
-   Tener un sistema Windows con SQL Server 2008 Enterprise Edition o una versión posterior lista para instalarse o ya estar instalado. El sistema de Windows ya debe estar configurado de acuerdo con las instrucciones de [configuración de un sistema externo de Windows para recibir copias de la tabla remota mediante InfiniBand](configure-an-external-windows-system-to-receive-remote-table-copies-using-infiniband.md).  
  
-   Una cuenta de administrador de Windows con la posibilidad de configurar la instancia de SQL Server y el sistema de Windows.  
  
-   Un SQL Server cuenta de inicio de sesión (si SQL Server ya está instalado) con la capacidad de crear inicios de sesión y conceder permisos en las bases de datos de destino.  
  
## <a name="configure-an-external-smp-sql-server-to-receive-remote-table-copies"></a><a name="HowToSQLServer"></a>Configurar un SQL Server SMP externo para recibir copias de la tabla remota  
La característica de copia de tabla remota copia las tablas del dispositivo PDW de SQL Server a una base de datos de SQL Server SMP externa que se ejecuta en un sistema Windows. Después de configurar el sistema externo de Windows para recibir copias de la tabla remota, el siguiente paso es instalar y configurar SQL Server en el sistema de Windows.  
  
Para configurar SQL Server, siga estos pasos:  
  
1.  Instale SQL Server 2008 Enterprise Edition o una versión posterior en el sistema de Windows. Esto se conoce como el SQL Server SMP.  
  
2.  Configure SQL Server para aceptar conexiones TCP/IP en un puerto TCP fijo. Esta configuración está deshabilitada de forma predeterminada y debe estar habilitada para permitir que PDW de SQL Server se conecte a la SQL Server SMP.  
  
3.  Deshabilite el Firewall de Windows o configure el puerto TCP SQL Server SMP para que funcione con el Firewall de Windows habilitado.  
  
4.  Configure SQL Server para permitir el modo de autenticación SQL Server. La exportación de datos en paralelo siempre usa cuentas SQL Server para la autenticación.  
  
5.  Determine una cuenta SQL Server en el SQL Server SMP que se utilizará para la autenticación. Conceda a esa cuenta el privilegio para crear, quitar e insertar datos en tablas en la base de datos de destino para la operación de exportación de datos en paralelo.  
  
## <a name="best-practices-for-smp-sql-server-configuration-for-remote-table-copy"></a><a name="BPSQLConfig"></a>Prácticas recomendadas para la configuración de SQL Server SMP para la copia de tabla remota  
Al configurar el SQL Server SMP para recibir copias de la tabla remota, utilice las siguientes prácticas recomendadas para mejorar el rendimiento.  
  
1.  Siga los procedimientos recomendados como se documenta en SQL Server documentación del producto. Por ejemplo, habilite el cifrado de datos. Para obtener más información acerca de la protección de SQL Server, consulte [protección de SQL Server](../relational-databases/security/securing-sql-server.md) en MSDN.  
  
2.  Use el modelo de recuperación optimizado para cargas masivas de registro o simple.  
  
    Durante las operaciones de exportación de datos paralelas, los datos se insertan de forma masiva en la tabla de destino recién creada. Para obtener el máximo rendimiento durante la inserción masiva, establezca la base de datos de destino para que use el modelo de recuperación optimizado para cargas masivas de registro o simple.  
  
3.  Use la opción batch_size para recuperar espacio de registro.  
  
    Aunque los modelos de recuperación optimizados para cargas masivas de registros o simples usan un registro mínimo para los datos insertados de forma masiva, se sigue produciendo algún registro. Para evitar que los archivos de registro crezcan demasiado, use la opción SQL Server batch_size para recuperar el espacio de registro periódicamente.  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
