---
title: "Instalación de SQL Server R Services en una máquina virtual de Azure | Microsoft Docs"
ms.custom: 
ms.date: 07/10/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c3c223b8-75c4-412e-a319-d57ecf6533af
caps.latest.revision: 11
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e673268b1f6b56890f22576d293135b2675ed4ab
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="installing-sql-server-r-services-on-an-azure-virtual-machine"></a>Instalación de SQL Server R Services en una máquina virtual de Azure
 
Si implementa una máquina virtual de Azure que incluye [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], ahora puede seleccionar el aprendizaje automático como una característica que se agregará a la instancia cuando se crea la máquina virtual.

+ [Crear una máquina virtual con SQL Server 2016 y R Services](#new)
+ [Agregar R Services a una máquina virtual existente con SQL Server 2016](#existing)

## <a name="new"></a>Crear una máquina virtual de SQL Server 2016 Enterprise con R Services habilitado

1. En el portal de Azure, haga clic en máquinas virtuales y, a continuación, haga clic en nuevo.
2. Seleccione SQL Server 2016 Enterprise Edition.
3. Configure el nombre de servidor y los permisos de cuenta y seleccione un plan de precios.
4. En el paso 4 del asistente para la configuración de máquinas virtuales, en **Configuración de SQL Server**, busque **R Services (análisis avanzado)** y haga clic en **Habilitar**.
5. Revise el resumen de validación y haga clic en **Aceptar**.
6. Cuando la máquina virtual esté lista, conéctese a ella y abra SQL Server Management Studio, que ya está preinstalado. R Services está listo para ejecutarse.
7. Para confirmarlo, puede abrir una nueva ventana de consulta y ejecutar una instrucción sencilla como la siguiente, en la que se usa R para generar una secuencia de números del 1 al 10.
   ```
    execute sp_execute_external_script
    @language = N'R'
    , @script = N' OutputDataSet <- as.data.frame(seq(1, 10, ));'
    , @input_data_1 = N'   ;'
    WITH RESULT SETS (([Sequence] int NOT NULL));
   ```
6. Si se va a conectar a la instancia desde un cliente de ciencia de datos remoto, lleve a cabo [otros pasos adicionales](#additional-steps) según sea necesario.


## <a name="additional-steps"></a>Pasos adicionales  

Si espera que los clientes remotos obtener acceso al servidor como un contexto de proceso de SQL Server remoto, son necesarios algunos pasos adicionales.

### <a name="firewall"></a>Desbloquear el firewall

El firewall de la máquina virtual de Azure incluye de forma predeterminada una regla que bloquea el acceso a la red de las cuentas de usuario locales de R.

Debe deshabilitar esta regla para asegurarse de que puede tener acceso a la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instancia desde un cliente de ciencia de datos remotos.  En caso contrario, no se puede ejecutar el código de R en contextos de proceso que use el área de trabajo de la máquina virtual, incluso si otro código de R utiliza el contexto de proceso de SQL Server sin problemas.

Para permitir el acceso a R Services desde clientes de ciencia de datos remotos:

1. En la máquina virtual, abra Firewall de Windows con seguridad avanzada.
2. Seleccione **Reglas de salida**.
3. Deshabilite la siguiente regla:
  
     `Block network access for R local user accounts in SQL Server instance MSSQLSERVER`
  
### <a name="enable-odbc-callbacks-for-remote-clients"></a>Habilitar devoluciones de llamada ODBC para clientes remotos

Si tiene previsto que los clientes de R que llamen al servidor deban generar consultas de ODBC como parte de sus soluciones de R, deberá asegurarse de que el Launchpad puede realizar llamadas a ODBC en nombre del cliente remoto. Para ello, debe permitir que las cuentas de trabajo SQL que usan Launchpad puedan iniciar sesión en la instancia.
Para obtener más información, consulte [Configurar SQL Server R Services](../../advanced-analytics/r/set-up-sql-server-r-services-in-database.md).

### <a name="network"></a>Agregar protocolos de red

+ Habilitar las canalizaciones con nombre
  
  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] usa el protocolo Canalizaciones con nombre en las conexiones entre los equipos cliente y servidor, así como en algunas conexiones de naturaleza interna. Si Canalizaciones con nombre no está habilitado, debe instalarlo y habilitarlo tanto en la máquina virtual de Azure como en cualquier cliente de ciencia de datos que se conecte al servidor.
  
+ Habilitar TCP/IP

  Se necesita TCP/IP en las conexiones de bucle invertido a SQL Server R Services. Si recibe el siguiente error, habilite TCP/IP en la máquina virtual que es compatible con la instancia:

  "DBNETLIB; SQL Server no existe o se denegó el acceso"

## <a name="how-to-disable-r-services-on-an-instance"></a>Cómo deshabilitar R Services en una instancia

Esta característica también se puede habilitar o deshabilitar en una máquina virtual existente en cualquier momento.

1. Abra la hoja de máquina virtual.
2. Haga clic en **Configuración** y seleccione **Configuración de SQL Server**.

## <a name="existing"></a>Agregar SQL Server R Services a una máquina virtual existente de SQL Server 2016 Enterprise

Si ha creado una máquina virtual de Azure que no incluía R Services, puede agregar la característica siguiendo estos pasos:

1. Vuelva a ejecutar el programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y agregar la característica en la página del asistente **Configuración del servidor**.
2. Habilite la ejecución de scripts externos y reinicie la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener más información, consulte [Configurar SQL Server R Services](../../advanced-analytics/r/set-up-sql-server-r-services-in-database.md).
3. (Opcional) Configure el acceso de base de datos para cuentas de trabajo de R en caso de que sea necesario para la ejecución remota de scripts.
   Para obtener más información, consulte [Configurar SQL Server R Services](../../advanced-analytics/r/set-up-sql-server-r-services-in-database.md).
3. (Opcional) Modifique una regla de firewall en la máquina virtual de Azure si tiene intención de permitir la ejecución de scripts de R desde clientes de ciencia de datos remotos. Para más información, vea [Desbloquear el firewall](#firewall).
4. Instale o habilite las bibliotecas de red necesarias. Para más información, vea [Agregar protocolos de red](#network).

## <a name="related-resources"></a>Recursos relacionados

[Configurar SQL Server R Services](../../advanced-analytics/r/set-up-sql-server-r-services-in-database.md)

