---
title: 'Migrar datos de Sybase ASE a SQL Server: base de datos SQL de Azure | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Migrating data,Client Side Data Migration
- Migrating data,Server Side Data Migration
ms.assetid: 54a39f5e-9250-4387-a3ae-eae47c799811
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: faecf1d3a7ab820ef01a25ea67b2313ab03e056a
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/15/2018
ms.locfileid: "51657405"
---
# <a name="migrating-sybase-ase-data-into-sql-server---azure-sql-db--sybasetosql"></a>Migración de datos de Sybase ASE a SQL Server: Azure SQL DB (SybaseToSQL)
Después de haber cargado correctamente los objetos de base de datos de Sybase Adaptive Server Enterprise (ASE) en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Azure SQL DB, puede migrar datos desde el ASE para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Azure SQL DB.  
  
> [!IMPORTANT]  
> Si el motor que se va a usar motor de migración de datos de lado servidor, antes de migrar datos, debe instalar SSMA para Sybase ASE extensión Pack y los proveedores de Sybase ASE en el equipo que ejecuta SSMA. También debe ejecutar el servicio Agente SQL Server. Para obtener más información sobre cómo instalar el paquete de extensiones, consulte [instalación de componentes de SSMA en SQL Server (SybaseToSQL)](https://msdn.microsoft.com/5ad9e12c-2cdb-4dd2-8703-05a23242d19d)  
  
## <a name="setting-migration-options"></a>Establecer las opciones de migración  
Antes de migrar datos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Azure SQL DB, revise las opciones de migración de proyecto en el **configuración del proyecto** cuadro de diálogo.  
  
-   Mediante este cuadro de diálogo puede establecer opciones como el tamaño del lote de migración, bloqueo de tablas, comprobación de restricciones, tratamiento de los valores null y control de valor de identidad. Para obtener más información acerca de la configuración de proyecto de migración, consulte [configuración del proyecto (migración) (Sybase)](https://msdn.microsoft.com/82f8857f-7ab1-4738-ab6e-b1e95ea94924).  
  
    Para obtener más información sobre **configuración de migración de datos extendida**, consulte [configuración de migración de datos](data-migration-settings-sybasetosql.md)  
  
-   El **migración motor** en el **configuración del proyecto** cuadro de diálogo permite al usuario realizar el proceso de migración con dos tipos de motores de migración de datos, viz.:  
  
    1.  Motor de migración de datos de lado cliente  
  
    2.  Motor de migración de datos de lado servidor  
  
**Migración de datos del lado cliente:**  
  
-   Para iniciar la migración de datos en el lado cliente, seleccione la opción **motor de migración de datos de lado cliente** en el **configuración del proyecto** cuadro de diálogo.  
  
-   En **configuración del proyecto**, **motor de migración de datos de lado cliente** opción se establece de forma predeterminada.  
  
    > [!NOTE]  
    > El motor de migración de datos de cliente reside dentro de la aplicación de SSMA y, por lo tanto, no es dependiente de la disponibilidad del módulo de extensión.  
  
**Migración de datos del lado servidor:**  
  
-   Durante la migración de datos del lado servidor, el motor reside en la base de datos de destino. Se instala a través del módulo de extensión. Para obtener más información sobre cómo instalar el paquete de extensiones, consulte [instalación de componentes de SSMA en SQL Server (SybaseToSQL)](https://msdn.microsoft.com/5ad9e12c-2cdb-4dd2-8703-05a23242d19d)  
  
-   Para iniciar la migración en el servidor, seleccione el **motor de migración de datos de lado servidor** opción el **configuración del proyecto** cuadro de diálogo.  
  
> [!NOTE]  
> Cuando se usa la base de datos de SQL Azure como la base de datos de destino, solo **migración de datos del lado cliente** está permitido y no se admite la migración de datos del lado servidor.  
  
## <a name="migrating-data-to-sql-server-or-azure-sql-db"></a>Migrar datos a SQL Server o SQL Azure DB  
Migración de datos están una operación de carga masiva que mueve las filas de datos de las tablas de ASE en tablas de SQL Server en las transacciones. El número de filas que se cargan en SQL Server o Azure SQL DB en cada transacción se configura en la configuración del proyecto.  
  
Para ver los mensajes de la migración, asegúrese de que está visible el panel de salida. En caso contrario, seleccione **salida** desde el **vista** menú.  
  
**Para migrar datos**  
  
1.  Compruebe lo siguiente:  
  
    -   Los proveedores de ASE se instalan en el equipo que ejecuta SSMA.  
  
    -   Los objetos convertidos se han sincronizado con la base de datos de destino (SQL Server o Azure SQL DB).  
  
2.  En el Explorador de metadatos de Sybase, seleccione los objetos que contienen los datos que se van a migrar:  
  
    -   Para migrar datos de todos los esquemas, active la casilla situada junto a **esquemas**.  
  
    -   Para migrar datos u omitir las tablas individuales, expanda el esquema, expanda **tablas**y, a continuación, active o desactive la casilla de verificación junto a la tabla.  
  
3.  Para migrar datos, surgen dos casos:  
  
    **Migración de datos del lado cliente:**  
  
    Para llevar a cabo **migración de datos del lado cliente**, seleccione el **motor de migración de datos de lado cliente** opción el **configuración del proyecto** cuadro de diálogo.  
  
    **Migración de datos del lado servidor:**  
  
    -   Antes de realizar la migración de datos del lado servidor, asegúrese de:  
  
        1.  SSMA para Sybase: paquete de extensión se instala en la instancia de SQL Server.  
  
        2.  El servicio Agente SQL Server se ejecuta en la instancia de SQL Server  
  
    -   Para llevar a cabo **migración de datos del lado servidor**, seleccione el **motor de migración de datos de lado servidor** opción el **configuración del proyecto** cuadro de diálogo.  
  
4.  Haga clic en **esquemas** en el Explorador de metadatos de Sybase y, a continuación, haga clic en **migrar datos**. También puede migrar datos para objetos individuales o categorías de objetos: haga clic en el objeto o la carpeta principal y seleccione el **migrar datos** opción.  
  
    > [!NOTE]  
    > Si no está instalado SSMA para Sybase: paquete de extensión en la instancia de SQL Server y **motor de migración de datos de lado servidor** está seleccionada, al migrar los datos a la base de datos de destino, se encontró el siguiente error: ' SSMA No se encontraron componentes de migración de datos en SQL Server, no será posible la migración de datos del servidor. Compruebe si el paquete de extensión se instaló correctamente ". Haga clic en **cancelar** para finalizar la migración de datos.  
  
5.  En el **conectarse a Sybase ASE** cuadro de diálogo, escriba las credenciales de conexión y, a continuación, haga clic en **Connect**. Para obtener más información sobre cómo conectarse a Sybase ASE, consulte [conectarse a Sybase &#40;SybaseToSQL&#41;](../../ssma/sybase/connect-to-sybase-sybasetosql.md)  
  
    Si la base de datos de destino es SQL Server, a continuación, escriba las credenciales de conexión en el **conectar con SQL Server** cuadro de diálogo y haga clic en **Connect**. Para obtener más información sobre cómo conectarse a SQL Server, vea [conectarse a SQL Server(SybaseToSQL)](https://msdn.microsoft.com/dd368a1a-45b0-40e9-b4d3-5cdb48c26606)  
  
    Si la base de datos de destino es Azure SQL DB, a continuación, escriba las credenciales de conexión en el **Connect a Azure SQL DB** cuadro de diálogo y haga clic en **Connect**. Para obtener más información sobre cómo conectarse a Azure SQL DB, consulte [conexión a Azure SQL DB &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-azure-sql-db-sybasetosql.md)  
  
    Los mensajes aparecerán en la **salida** panel. Una vez completada la migración, el **informe de migración de datos** aparece. Si no se ha migrado los datos, haga clic en la fila que contiene los errores y, a continuación, haga clic en **detalles**. Cuando haya terminado con el informe, haga clic en **cerrar**. Para obtener más información sobre el informe de migración de datos, vea [informe de migración de datos (SSMA comunes)](https://msdn.microsoft.com/bbfb9d88-5a98-4980-8d19-c5d78bd0d241)  
  
> [!NOTE]  
> Cuando se utiliza SQL Express edition como la base de datos de destino, se permite la migración de datos de lado a solo cliente y no se admite la migración de datos del lado servidor.  
  
## <a name="see-also"></a>Vea también  
[Migrar bases de datos de Sybase ASE a SQL Server: base de datos SQL Azure &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
