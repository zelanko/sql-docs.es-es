---
title: 'Migrar datos de MySQL a SQL Server: base de datos de SQL Azure (MySQLToSQL) | Documentos de Microsoft'
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssma-mysql
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Data Migration, server side data migration
- Data Migration,client side data migration
ms.assetid: a6a7f4d6-68aa-4a38-93bf-53eba0d7dc82
caps.latest.revision: "24"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0887825cf16986b78cad5d1889a04d73dacf222a
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="migrating-mysql-data-into-sql-server---azure-sql-db-mysqltosql"></a>Migrar datos de MySQL a SQL Server: base de datos de SQL Azure (MySQLToSQL)
Después de haber sincronizado correctamente los objetos convertidos con [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure, puede migrar datos de MySQL a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure.  
  
> [!IMPORTANT]  
> Si el motor que se va a usar motor de migración de datos del lado servidor, a continuación, antes de migrar datos, debe instalar SSMA para paquete de extensión de MySQL y los proveedores de MySQL en el equipo que está ejecutando SSMA. El [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] también debe ejecutarse el servicio de agente. Para obtener más información acerca de cómo instalar el paquete de extensión, vea [instalar componentes de SSMA en SQL Server (MySQL a SQL)](http://msdn.microsoft.com/en-us/6772d0c5-258f-4d7b-afb0-b5f810e71af1)  
  
## <a name="setting-migration-options"></a>Establecer las opciones de migración  
Antes de migrar datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure, revise las opciones de migración de proyecto en el **configuración del proyecto** cuadro de diálogo.  
  
-   Mediante este cuadro de diálogo puede establecer opciones como el tamaño de lote de migración, bloqueo de tablas, comprobación de restricciones, tratamiento de los valores null y control de valor de identidad. Para obtener más información acerca de las opciones de migración de proyecto, vea [configuración del proyecto (migración)](http://msdn.microsoft.com/en-us/2a3cba9e-cd54-4a8b-b858-8fc4cf2580d9).  
  
    Para obtener más información sobre **configuración de migración de datos extendida**, consulte [configuración de la migración de datos](http://msdn.microsoft.com/en-us/9c396df4-5676-4f32-9c57-70d4f15f9b7a)  
  
-   El **motor de migración de** en el **configuración del proyecto** permite al usuario realizar el proceso de migración con dos tipos de motores de migración de datos de cuadro de diálogo:  
  
    1.  Motor de migración de datos de lado cliente  
  
    2.  Motor de migración de datos de lado de servidor  
  
**Migración de datos del lado cliente:**  
  
-   Para iniciar la migración de datos en el lado del cliente, seleccione la **motor de migración de datos de lado cliente** opción en el **configuración del proyecto** cuadro de diálogo.  
  
-   En **configuración del proyecto**, **motor de migración de datos de lado cliente** opción está establecida.  
  
    > [!NOTE]  
    > El **motor de migración de datos de cliente** reside dentro de la aplicación de SSMA y es, por lo tanto, no depende de la disponibilidad del módulo de extensión.  
  
**Migración de datos del lado servidor:**  
  
-   Durante la migración de datos del lado servidor, el motor reside en la base de datos de destino. Se instala a través del módulo de extensión. Para obtener más información sobre cómo instalar el módulo de extensión, vea [instalar componentes de SSMA en SQL Server (MySQL a SQL)](http://msdn.microsoft.com/en-us/6772d0c5-258f-4d7b-afb0-b5f810e71af1)  
  
-   Para iniciar la migración en el servidor, seleccione la **motor de migración de datos de lado servidor** opción en el **configuración del proyecto** cuadro de diálogo.  
  
> [!IMPORTANT]  
> **Migración de datos del lado cliente** opción sólo está disponible para SQL Azure.  
  
## <a name="migrating-data-to-sql-server-or-sql-azure"></a>Migrar datos a SQL Server o SQL Azure  
Migración de datos están una operación de carga masiva que mueve filas de datos de tablas de MySQL en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o tablas de SQL Azure en las transacciones. El número de filas que se carga en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] en cada transacción se configura en la configuración del proyecto.  
  
Para ver mensajes de migración, asegúrese de que esté visible el panel de resultados. En caso contrario, desde el **vista** menú, seleccione **salida**.  
  
**Para migrar datos**  
  
1.  Compruebe lo siguiente:  
  
    -   Los proveedores de MySQL se instalan en el equipo que está ejecutando SSMA.  
  
    -   Los objetos convertidos se han sincronizado con la base de datos de destino (SQL Server o SQL Azure).  
  
2.  En el Explorador de metadatos de MySQL, seleccione los objetos que contienen los datos que se van a migrar:  
  
    -   Para migrar datos de todos los esquemas, active la casilla situada junto a **esquemas**.  
  
    -   Para migrar datos o se omite las tablas individuales, expanda el esquema, expanda **tablas**y, a continuación, active o desactive la casilla situada junto a la tabla.  
  
3.  Para migrar datos, surgen dos casos:  
  
    **Migración de datos del lado cliente:**  
  
    -   Para llevar a cabo **migración de datos del lado cliente**, seleccione la **motor de migración de datos de lado cliente** opción en el **configuración del proyecto** cuadro de diálogo.  
  
    **Migración de datos del lado servidor:**  
  
    -   Antes de realizar la migración de datos en el servidor, asegúrese de:  
  
        1.  SSMA para MySQL: paquete de extensión se instala en la instancia de SQL Server.  
  
        2.  El [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] servicio del agente se ejecuta en la instancia de SQL Server  
  
    -   Para llevar a cabo **migración de datos del lado servidor**, seleccione la **motor de migración de datos de lado servidor** opción en el **configuración del proyecto** cuadro de diálogo.  
  
4.  Haga clic en **esquemas** en el Explorador de metadatos de MySQL y, a continuación, haga clic en **migrar datos**. También puede migrar datos de objetos individuales o las categorías de objetos: haga clic en el objeto o su carpeta principal; Seleccione el **migrar datos** opción.  
  
    > [!NOTE]  
    > Si el SSMA para paquete de extensión de MySQL no está instalado en la instancia de SQL Server y **motor de migración de datos de lado servidor** está seleccionada, a continuación, al migrar los datos a la base de datos de destino, se produjo el siguiente error: ' componentes de migración de datos de SSMA no se encontraron en SQL Server, migración de datos en el servidor no podrá realizarse. Compruebe si el módulo de extensión está instalado correctamente ". Haga clic en **cancelar** para terminar la migración de datos.  
  
5.  En el **conectar con MySQL** cuadro de diálogo, escriba las credenciales de conexión y, a continuación, haga clic en **conectar**. Para obtener más información sobre cómo conectarse a MySQL, vea [conectar con MySQL &#40; MySQLToSQL &#41;](../../ssma/mysql/connect-to-mysql-mysqltosql.md)  
  
    Si la base de datos de destino es SQL Server, a continuación, escriba las credenciales de conexión en el **conectar con SQL Server** cuadro de diálogo y haga clic en **conectar**. Para obtener más información sobre cómo conectarse a SQL Server, vea [conectar con SQL Server](http://msdn.microsoft.com/en-us/bb8c4bde-cfc2-4636-92ae-5dd24abe9536)  
  
    Si la base de datos de destino es SQL Azure, a continuación, escriba las credenciales de conexión en el **conectarse a SQL Azure** cuadro de diálogo y haga clic en **conectar**. Para obtener más información sobre cómo conectarse a SQL Azure, consulte [conectarse a la base de datos de SQL de Azure &#40; MySQLToSQL &#41;](../../ssma/mysql/connect-to-azure-sql-db-mysqltosql.md)  
  
    Mensajes aparecerán en la **salida** panel. Una vez completada, la migración del **informe de migración de datos** aparece. Si no se ha migrado los datos, haga clic en la fila que contiene los errores y, a continuación, haga clic en **detalles**. Cuando haya terminado con el informe, haga clic en **cerrar**. Para obtener más información sobre informes de migración de datos, vea [informe de migración de datos (SSMA común)](http://msdn.microsoft.com/en-us/bbfb9d88-5a98-4980-8d19-c5d78bd0d241)  
  
> [!NOTE]  
> Cuando se utiliza SQL Express edition como la base de datos de destino, se permite la migración de datos de lado a solo cliente y no se admite la migración de datos del lado servidor.  
  
## <a name="see-also"></a>Vea también  
[Migrar bases de datos de MySQL a SQL Server: base de datos de SQL Azure &#40; MySQLToSql &#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
