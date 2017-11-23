---
title: "Instalar características de aprendizaje de máquina de SQL Server en una máquina virtual de Azure | Documentos de Microsoft"
ms.custom: 
ms.date: 10/31/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c3c223b8-75c4-412e-a319-d57ecf6533af
caps.latest.revision: "11"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 08c3434ec120003de6d62bc61da3637e9177bb88
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="installing-sql-server-machine-learning-features-on-an-azure-virtual-machine"></a>Instalación de características en una máquina virtual de Azure de aprendizaje de automático de SQL Server
 
Si implementa una máquina virtual de Azure que incluye [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], ahora puede seleccionar el aprendizaje automático como una característica que se agregará a la instancia cuando se crea la máquina virtual.

+ [Crear una nueva máquina virtual que incluye SQL Server 2016 y R Services](#new)
+ [Agregar características de aprendizaje de máquina a una máquina virtual existente con SQL Server 2016](#existing)

> [!NOTE]
> ¡Máquinas virtuales están ahora disponibles para SQL Server 2017! Vea [este anuncio](https://azure.microsoft.com/blog/announcing-new-azure-vm-images-sql-server-2017-on-linux-and-windows/) para obtener más información.
> 
> R también está disponible como una característica de vista previa de la base de datos de SQL Azure. Para obtener más información, consulte [usar R en la base de datos de SQL Azure](../r/using-r-in-azure-sql-database.md).

## <a name="create-a-new-sql-server-2017-virtual-machine"></a>Crear una nueva máquina virtual de SQL Server 2017

Para usar R o Python en SQL Server 2017, asegúrese de obtener una máquina virtual de Windows. [!INCLUDE[sscurrentlong-md](../../includes/sscurrentlong-md.md)]en Linux es compatible con fast [puntuación nativo](../sql-native-scoring.md) utilizando la función de PREDICCIÓN de T-SQL, pero otra características de aprendizaje automático no están disponibles todavía en esta edición.

Para obtener una lista de ofertas de VM de SQL Server, consulte este artículo: [información general de SQL Server en máquinas virtuales de Azure (Windows)](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview).

### <a name="new"></a>Crear una nueva VM de Enterprise de SQL Server con aprendizaje automático

1. En el portal de Azure, haga clic en máquinas virtuales y, a continuación, haga clic en nuevo.
2. Seleccione la edición Enterprise SQL Server de 2017.
3. Configure el nombre de servidor y los permisos de cuenta y seleccione un plan de precios.
4. En **configuración de SQL Server** (paso 4 del Asistente para instalación VM), busque **servicios de aprendizaje de máquina (Advanced Analytics)** y haga clic en **habilitar**.
5. Revise el resumen de validación y haga clic en **Aceptar**.
6. Cuando la máquina virtual esté lista, conéctese a ella y abra SQL Server Management Studio, que ya está preinstalado. Aprendizaje automático está listo para ejecutarse.
7. Para confirmarlo, puede abrir una nueva ventana de consulta y ejecutar una instrucción sencilla como la siguiente, en la que se usa R para generar una secuencia de números del 1 al 10.

    ```
    EXEC sp_execute_external_script
    @language = N'R'
    , @script = N' OutputDataSet <- as.data.frame(seq(1, 10, ));'
    , @input_data_1 = N'   ;'
    WITH RESULT SETS (([Sequence] int NOT NULL));
    ```

6. Si tiene previsto conectarse a la instancia desde un cliente de ciencia de datos remotos, completar [pasos adicionales](#additional-steps) según sea necesario.

### <a name="disable-machine-learning-features-on-a-sql-server-vm"></a>Deshabilitar las características de aprendizaje de máquina en una VM de SQL Server

También puede habilitar o deshabilitar la característica en una máquina virtual de SQL Server existente en cualquier momento.

1. Abra la hoja de la máquina virtual.
2. Haga clic en **Configuración** y seleccione **Configuración de SQL Server**.
3. Realizar cambios en las características y aplicar.

### <a name="existing"></a>Agregar R Services a una VM existente de SQL Server 2016 Enterprise

Si ha creado una máquina virtual de Azure que incluye SQL Server sin aprendizaje automático, puede agregar la característica siguiendo estos pasos:

1. Vuelva a ejecutar el programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y agregar la característica en la página del asistente **Configuración del servidor**.
2. Habilite la ejecución de scripts externos y reinicie la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener más información, consulte [configurar SQL Server R Services](../../advanced-analytics/r/set-up-sql-server-r-services-in-database.md).
3. (Opcional) Configure el acceso de base de datos para cuentas de trabajo de R en caso de que sea necesario para la ejecución remota de scripts.
   Para obtener más información, consulte [Configurar SQL Server R Services](../../advanced-analytics/r/set-up-sql-server-r-services-in-database.md).
3. (Opcional) Modifique una regla de firewall en la máquina virtual de Azure si tiene intención de permitir la ejecución de scripts de R desde clientes de ciencia de datos remotos. Para más información, vea [Desbloquear el firewall](#firewall).
4. Instale o habilite las bibliotecas de red necesarias. Para más información, vea [Agregar protocolos de red](#network).

## <a name="additional-steps"></a>Pasos adicionales

Si espera que los clientes remotos obtener acceso al servidor como un contexto de proceso de SQL Server remoto, son necesarios algunos pasos adicionales.

### <a name="firewall"></a>Desbloquear el firewall

De forma predeterminada, el firewall en la máquina virtual de Azure incluye una regla que bloquea el acceso a las cuentas de usuario local de red.

Debe deshabilitar esta regla para asegurarse de que puede tener acceso a la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instancia desde un cliente de ciencia de datos remotos.  En caso contrario, el código de aprendizaje de automático no se puede ejecutar en contextos de proceso que use el área de trabajo de la máquina virtual.

Para habilitar el acceso de los clientes de ciencia de datos remoto:

1. En la máquina virtual, abra Firewall de Windows con seguridad avanzada.
2. Seleccione **Reglas de salida**.
3. Deshabilite la siguiente regla:
  
     `Block network access for R local user accounts in SQL Server instance MSSQLSERVER`
  
### <a name="enable-odbc-callbacks-for-remote-clients"></a>Habilitar devoluciones de llamada ODBC para clientes remotos

Si espera que los clientes que llamen al servidor que necesitará emitir consultas de ODBC como parte de su soluciones de aprendizaje automático, debe asegurarse de que el Launchpad puede realizar llamadas ODBC en nombre del cliente remoto. Para ello, debe permitir que las cuentas de trabajo SQL que usan Launchpad puedan iniciar sesión en la instancia.
Para obtener más información, consulte [Configurar SQL Server R Services](../../advanced-analytics/r/set-up-sql-server-r-services-in-database.md).

### <a name="network"></a>Agregar protocolos de red

+ Habilitar las canalizaciones con nombre
  
  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] usa el protocolo Canalizaciones con nombre en las conexiones entre los equipos cliente y servidor, así como en algunas conexiones de naturaleza interna. Si Canalizaciones con nombre no está habilitado, debe instalarlo y habilitarlo tanto en la máquina virtual de Azure como en cualquier cliente de ciencia de datos que se conecte al servidor.
  
+ Habilitar TCP/IP

  TCP/IP es necesaria para las conexiones de bucle invertido. Si recibe el siguiente error, habilite TCP/IP en la máquina virtual que es compatible con la instancia:

  "DBNETLIB; SQL Server no existe o se denegó el acceso"

## <a name="related-resources"></a>Recursos relacionados

[Uso de R en la base de datos SQL Azure](../r/using-r-in-azure-sql-database.md)