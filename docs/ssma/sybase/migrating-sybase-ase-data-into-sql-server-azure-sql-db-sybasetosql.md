---
title: 'Migrar datos de Sybase ASE en SQL Server: base de datos de SQL Azure | Documentos de Microsoft'
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Migrating data,Client Side Data Migration
- Migrating data,Server Side Data Migration
ms.assetid: 54a39f5e-9250-4387-a3ae-eae47c799811
caps.latest.revision: 15
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 2e30171c86c56f232d17ed159eb53d0eaddae79c
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="migrating-sybase-ase-data-into-sql-server---azure-sql-db--sybasetosql"></a>Migración de datos de Sybase ASE en SQL Server: base de datos de SQL Azure (SybaseToSQL)
Después de haber cargado correctamente los objetos de base de datos de Sybase Adaptive Server Enterprise (ASE) en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o base de datos de SQL Azure, puede migrar datos de ASE a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o base de datos de SQL Azure.  
  
> [!IMPORTANT]  
> Si el motor que se va a usar motor de migración de datos de lado de servidor, antes de migrar datos, debe instalar SSMA para Sybase ASE extensión Pack y los proveedores de Sybase ASE en el equipo que está ejecutando SSMA. También debe ejecutar el servicio Agente SQL Server. Para obtener más información acerca de cómo instalar el paquete de extensión, vea [instalar componentes de SSMA en SQL Server (SybaseToSQL)](http://msdn.microsoft.com/en-us/5ad9e12c-2cdb-4dd2-8703-05a23242d19d)  
  
## <a name="setting-migration-options"></a>Establecer las opciones de migración  
Antes de migrar datos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o base de datos de SQL Azure, revise las opciones de migración de proyecto en el **configuración del proyecto** cuadro de diálogo.  
  
-   Mediante este cuadro de diálogo puede establecer opciones como el tamaño de lote de migración, bloqueo de tablas, comprobación de restricciones, tratamiento de los valores null y control de valor de identidad. Para obtener más información acerca de las opciones de migración de proyecto, vea [configuración del proyecto (migración) (Sybase)](http://msdn.microsoft.com/en-us/82f8857f-7ab1-4738-ab6e-b1e95ea94924).  
  
    Para obtener más información sobre **configuración de migración de datos extendida**, consulte [configuración de la migración de datos](http://msdn.microsoft.com/en-us/94d7a083-2dbc-4e3d-94dd-92b7ff9d0c2d)  
  
-   El **motor de migración de** en el **configuración del proyecto** cuadro de diálogo permite al usuario realizar el proceso de migración con dos tipos de motores de migración de datos, especialmente.:  
  
    1.  Motor de migración de datos de lado cliente  
  
    2.  Motor de migración de datos de lado de servidor  
  
**Migración de datos del lado cliente:**  
  
-   Para iniciar la migración de datos en el lado del cliente, seleccione la opción **motor de migración de datos de lado cliente** en el **configuración del proyecto** cuadro de diálogo.  
  
-   En **configuración del proyecto**, **motor de migración de datos de lado cliente** opción se establece de forma predeterminada.  
  
    > [!NOTE]  
    > El motor de migración de datos de cliente reside dentro de la aplicación de SSMA y, por lo tanto, no es dependiente de la disponibilidad del módulo de extensión.  
  
**Migración de datos del lado servidor:**  
  
-   Durante la migración de datos del lado servidor, el motor reside en la base de datos de destino. Se instala a través del módulo de extensión. Para obtener más información sobre cómo instalar el módulo de extensión, vea [instalar componentes de SSMA en SQL Server (SybaseToSQL)](http://msdn.microsoft.com/en-us/5ad9e12c-2cdb-4dd2-8703-05a23242d19d)  
  
-   Para iniciar la migración en el servidor, seleccione la **motor de migración de datos de lado servidor** opción en el **configuración del proyecto** cuadro de diálogo.  
  
> [!NOTE]  
> Cuando se usa la base de datos de SQL Azure como la base de datos de destino, solo **migración de datos del lado cliente** está permitido y no se admite la migración de datos del lado servidor.  
  
## <a name="migrating-data-to-sql-server-or-azure-sql-db"></a>Migrar datos a SQL Server o base de datos de SQL Azure  
Migración de datos están una operación de carga masiva que mueve filas de datos de las tablas de ASE en tablas de SQL Server en las transacciones. El número de filas que se cargan en SQL Server o base de datos de SQL Azure en cada transacción se configura en la configuración del proyecto.  
  
Para ver los mensajes de la migración, asegúrese de que esté visible el panel de resultados. En caso contrario, seleccione **salida** desde el **vista** menú.  
  
**Para migrar datos**  
  
1.  Compruebe lo siguiente:  
  
    -   Los proveedores de ASE se instalan en el equipo que está ejecutando SSMA.  
  
    -   Los objetos convertidos se han sincronizado con la base de datos de destino (SQL Server o base de datos de SQL Azure).  
  
2.  En el Explorador de metadatos de Sybase, seleccione los objetos que contienen los datos que se van a migrar:  
  
    -   Para migrar datos de todos los esquemas, active la casilla situada junto a **esquemas**.  
  
    -   Para migrar datos o se omite las tablas individuales, expanda el esquema, expanda **tablas**y, a continuación, active o desactive la casilla situada junto a la tabla.  
  
3.  Para migrar datos, surgen dos casos:  
  
    **Migración de datos del lado cliente:**  
  
    Para llevar a cabo **migración de datos del lado cliente**, seleccione la **motor de migración de datos de lado cliente** opción en el **configuración del proyecto** cuadro de diálogo.  
  
    **Migración de datos del lado servidor:**  
  
    -   Antes de realizar la migración de datos del lado servidor, asegúrese de:  
  
        1.  SSMA para Sybase: paquete de extensión se instala en la instancia de SQL Server.  
  
        2.  El servicio Agente SQL Server se ejecuta en la instancia de SQL Server  
  
    -   Para llevar a cabo **migración de datos del lado servidor**, seleccione la **motor de migración de datos de lado servidor** opción en el **configuración del proyecto** cuadro de diálogo.  
  
4.  Haga clic en **esquemas** en el Explorador de metadatos de Sybase y, a continuación, haga clic en **migrar datos**. También puede migrar datos de objetos individuales o las categorías de objetos: haga clic en el objeto o su carpeta principal y seleccione el **migrar datos** opción.  
  
    > [!NOTE]  
    > Si no está instalado el SSMA para Sybase: paquete de extensión en la instancia de SQL Server y **motor de migración de datos de lado de servidor** está seleccionada, a continuación, al migrar los datos a la base de datos de destino, se produjo el siguiente error: ' componentes de migración de datos de SSMA no se encontraron en SQL Server, migración de datos en el servidor no podrá realizarse. Compruebe si el módulo de extensión está instalado correctamente ". Haga clic en **cancelar** para terminar la migración de datos.  
  
5.  En el **conectar para Sybase ASE** cuadro de diálogo, escriba las credenciales de conexión y, a continuación, haga clic en **conectar**. Para obtener más información sobre cómo conectarse a Sybase ASE, consulte [conectar para Sybase &#40; SybaseToSQL &#41;](../../ssma/sybase/connect-to-sybase-sybasetosql.md)  
  
    Si la base de datos de destino es SQL Server, a continuación, escriba las credenciales de conexión en el **conectar con SQL Server** cuadro de diálogo y haga clic en **conectar**. Para obtener más información sobre cómo conectarse a SQL Server, vea [conectarse a SQL Server(SybaseToSQL)](http://msdn.microsoft.com/en-us/dd368a1a-45b0-40e9-b4d3-5cdb48c26606)  
  
    Si la base de datos de destino es la base de datos de SQL Azure, a continuación, escriba las credenciales de conexión en el **conectar con base de datos de SQL Azure** cuadro de diálogo y haga clic en **conectar**. Para obtener más información sobre cómo conectarse a la base de datos de SQL Azure, consulte [conectarse a base de datos de SQL de Azure &#40; SybaseToSQL &#41;](../../ssma/sybase/connecting-to-azure-sql-db-sybasetosql.md)  
  
    Mensajes aparecerán en la **salida** panel. Una vez completada, la migración del **informe de migración de datos** aparece. Si no se ha migrado los datos, haga clic en la fila que contiene los errores y, a continuación, haga clic en **detalles**. Cuando haya terminado con el informe, haga clic en **cerrar**. Para obtener más información sobre informes de migración de datos, vea [informe de migración de datos (SSMA común)](http://msdn.microsoft.com/en-us/bbfb9d88-5a98-4980-8d19-c5d78bd0d241)  
  
> [!NOTE]  
> Cuando se utiliza SQL Express edition como la base de datos de destino, se permite la migración de datos de lado a solo cliente y no se admite la migración de datos del lado servidor.  
  
## <a name="see-also"></a>Vea también  
[Migrar bases de datos de ASE de Sybase a SQL Server: base de datos de SQL Azure &#40; SybaseToSQL &#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  

