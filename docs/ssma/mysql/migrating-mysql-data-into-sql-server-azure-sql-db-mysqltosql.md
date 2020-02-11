---
title: 'Migración de datos de MySQL en SQL Server: Azure SQL DB (MySQLToSQL) | Microsoft Docs'
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Data Migration, server side data migration
- Data Migration,client side data migration
ms.assetid: a6a7f4d6-68aa-4a38-93bf-53eba0d7dc82
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 83a4a2d1bea5074cc268590d4074bde631f28694
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67908830"
---
# <a name="migrating-mysql-data-into-sql-server---azure-sql-db-mysqltosql"></a>Migración de datos de MySQL en SQL Server: Azure SQL DB (MySQLToSQL)
Después de sincronizar correctamente los objetos convertidos con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure, puede migrar los datos de MySQL a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure.  
  
> [!IMPORTANT]  
> Si el motor utilizado es el motor de migración de datos del lado servidor, antes de migrar los datos, debe instalar el paquete de extensión SSMA para MySQL y los proveedores de MySQL en el equipo que ejecuta SSMA. El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] servicio del agente también debe estar en ejecución. Para obtener más información sobre cómo instalar el paquete de extensión, consulte [instalación de componentes de SSMA en SQL Server (MySQL to SQL)](https://msdn.microsoft.com/6772d0c5-258f-4d7b-afb0-b5f810e71af1) .  
  
## <a name="setting-migration-options"></a>Establecer opciones de migración  
Antes de migrar datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a o SQL Azure, revise las opciones de migración del proyecto en el cuadro de diálogo **configuración del proyecto** .  
  
-   Mediante este cuadro de diálogo puede establecer opciones como el tamaño del lote de migración, el bloqueo de tablas, la comprobación de restricciones, el control de valores NULL y el control de valores de identidad. Para obtener más información sobre la configuración de migración de proyectos, vea [configuración del proyecto (migración)](https://msdn.microsoft.com/2a3cba9e-cd54-4a8b-b858-8fc4cf2580d9).  
  
    Para obtener más información sobre la configuración de la **migración de datos extendida**, consulte Configuración de la [migración de datos](data-migration-settings-mysqltosql.md)  
  
-   El **motor de migración** en el cuadro de diálogo **configuración del proyecto** permite que el usuario realice el proceso de migración mediante dos tipos de motores de migración de datos:  
  
    1.  Motor de migración de datos del lado cliente  
  
    2.  Motor de migración de datos del lado servidor  
  
**Migración de datos del lado cliente:**  
  
-   Para iniciar la migración de datos en el lado cliente, seleccione la opción **motor de migración de datos del lado cliente** en el cuadro de diálogo **configuración del proyecto** .  
  
-   En **configuración del proyecto**, se establece la opción **motor de migración de datos del lado cliente** .  
  
    > [!NOTE]  
    > El **motor de migración de datos del lado cliente** reside dentro de la aplicación SSMA y, por lo tanto, no depende de la disponibilidad del paquete de extensión.  
  
**Migración de datos del lado servidor:**  
  
-   Durante la migración de datos del lado servidor, el motor reside en la base de datos de destino. Se instala a través del paquete de extensión. Para obtener más información sobre cómo instalar el paquete de extensión, consulte [instalación de componentes de SSMA en SQL Server (MySQL to SQL)](https://msdn.microsoft.com/6772d0c5-258f-4d7b-afb0-b5f810e71af1) .  
  
-   Para iniciar la migración en el lado del servidor, seleccione la opción **motor de migración de datos del lado servidor** en el cuadro de diálogo **configuración del proyecto** .  
  
> [!IMPORTANT]  
> La opción de **migración de datos del lado cliente** solo está disponible para SQL Azure.  
  
## <a name="migrating-data-to-sql-server-or-sql-azure"></a>Migrar datos a SQL Server o SQL Azure  
La migración de datos es una operación de carga masiva que mueve filas de datos de tablas MySQL [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a tablas o SQL Azure en las transacciones. El número de filas que se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cargan en cada transacción se configura en la configuración del proyecto.  
  
Para ver los mensajes de migración, asegúrese de que el panel de salida esté visible. En caso contrario, en el menú **Ver** , seleccione **salida**.  
  
**Para migrar datos**  
  
1.  Verifique lo siguiente:  
  
    -   Los proveedores de MySQL se instalan en el equipo que ejecuta SSMA.  
  
    -   Ha sincronizado los objetos convertidos con la base de datos de destino (SQL Server/SQL Azure).  
  
2.  En el explorador de metadatos de MySQL, seleccione los objetos que contienen los datos que desea migrar:  
  
    -   Para migrar datos de todos los esquemas, active la casilla situada junto a **esquemas**.  
  
    -   Para migrar datos u omitir tablas individuales, expanda primero el esquema, expanda **tablas**y, a continuación, Active o desactive la casilla situada junto a la tabla.  
  
3.  Para migrar datos, surgen dos casos:  
  
    **Migración de datos del lado cliente:**  
  
    -   Para realizar la **migración de datos del lado cliente**, seleccione la opción **motor de migración de datos del lado cliente** en el cuadro de diálogo **configuración del proyecto** .  
  
    **Migración de datos del lado servidor:**  
  
    -   Antes de realizar la migración de datos en el lado servidor, asegúrese de:  
  
        1.  El paquete de extensión SSMA para MySQL está instalado en la instancia de SQL Server.  
  
        2.  El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] servicio del agente se está ejecutando en la instancia de SQL Server  
  
    -   Para realizar la **migración de datos del lado servidor**, seleccione la opción **motor de migración de datos del lado servidor** en el cuadro de diálogo **configuración del proyecto** .  
  
4.  Haga clic con el botón derecho en **esquemas** en el explorador de metadatos de MySQL y luego haga clic en **migrar datos**. También puede migrar datos para objetos individuales o categorías de objetos: haga clic con el botón secundario en el objeto o en su carpeta primaria; Seleccione la opción **migrar datos** .  
  
    > [!NOTE]  
    > Si el paquete de extensión SSMA for MySQL no está instalado en la instancia de SQL Server, y si el **motor de migración de datos del lado servidor** está seleccionado, al migrar los datos a la base de datos de destino, se produce el siguiente error: "no se encontraron los componentes de migración de datos de ssma en SQL Server, la migración de datos del servidor no será posible. Compruebe si el paquete de extensiones está instalado correctamente. Haga clic en **Cancelar** para finalizar la migración de datos.  
  
5.  En el cuadro de diálogo **conectar con MySQL** , escriba las credenciales de conexión y, a continuación, haga clic en **conectar**. Para obtener más información sobre cómo conectarse a MySQL, consulte [conexión a mysql &#40;MySQLToSQL&#41;](../../ssma/mysql/connect-to-mysql-mysqltosql.md)  
  
    Si la base de datos de destino está SQL Server, escriba las credenciales de conexión en el cuadro de diálogo **conectar con SQL Server** y haga clic en **conectar**. Para obtener más información sobre cómo conectarse a SQL Server, consulte [conexión a SQL Server](https://msdn.microsoft.com/bb8c4bde-cfc2-4636-92ae-5dd24abe9536)  
  
    Si la base de datos de destino está SQL Azure, escriba las credenciales de conexión en el cuadro de diálogo **conectar con SQL Azure** y haga clic en **conectar**. Para más información sobre cómo conectarse a SQL Azure, consulte [conexión a Azure SQL DB &#40;MySQLToSQL&#41;](../../ssma/mysql/connect-to-azure-sql-db-mysqltosql.md)  
  
    Los mensajes aparecerán en el panel de **resultados** . Una vez completada la migración, aparece el **Informe de migración de datos** . Si no se migró ningún dato, haga clic en la fila que contiene los errores y, a continuación, haga clic en **detalles**. Cuando haya terminado con el informe, haga clic en **cerrar**. Para obtener más información sobre el informe de migración de datos, vea [Informe de migración de datos (SSMA Common)](https://msdn.microsoft.com/bbfb9d88-5a98-4980-8d19-c5d78bd0d241)  
  
> [!NOTE]  
> Cuando se utiliza SQL Express Edition como base de datos de destino, solo se permite la migración de datos del lado cliente y no se admite la migración de datos del lado servidor.  
  
## <a name="see-also"></a>Consulte también  
[Migración de bases de datos de MySQL a SQL Server: Azure SQL DB &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
