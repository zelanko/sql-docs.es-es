---
title: Migración de datos de DB2 en SQL Server (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 86cbd39f-6dac-409a-9ce1-7dd54403f84b
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 9cc7b3dd309dfac9e35021ca3234ca66483181e9
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "68074104"
---
# <a name="migrating-db2-data-into-sql-server-db2tosql"></a>Migración de datos de DB2 en SQL Server (DB2ToSQL)
Después de sincronizar correctamente los objetos convertidos con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], puede migrar los datos de DB2 a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
> Si el motor utilizado es el motor de migración de datos del lado servidor, antes de poder migrar los datos, debe instalar el paquete de extensión SSMA para DB2 y los proveedores de DB2 en el equipo que ejecuta SSMA. El servicio Agente SQL Server también debe estar en ejecución. Para obtener más información acerca de cómo instalar el paquete de extensión, consulte [instalación de componentes de SSMA en SQL Server](https://msdn.microsoft.com/cf2b724b-4ca7-470a-8dd7-fa95b1e060a4)  
  
## <a name="setting-migration-options"></a>Establecer opciones de migración  
Antes de migrar datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]a, revise las opciones de migración del proyecto en el cuadro de diálogo **configuración del proyecto** .  
  
-   Mediante este cuadro de diálogo puede establecer opciones como el tamaño del lote de migración, el bloqueo de tablas, la comprobación de restricciones, el control de valores NULL y el control de valores de identidad. Para obtener más información sobre la configuración de migración de proyectos, vea [configuración del proyecto (migración)](https://msdn.microsoft.com/48aaa8e6-a9cb-487d-9ba5-fc3f1c4786ae).  
  
-   El **motor de migración** en el cuadro de diálogo **configuración del proyecto** permite que el usuario realice el proceso de migración mediante dos tipos de motores de migración de datos:  
  
    1.  Motor de migración de datos del lado cliente  
  
    2.  Motor de migración de datos del lado servidor  
  
**Migración de datos del lado cliente:**  
  
-   Para iniciar la migración de datos en el lado cliente, seleccione la opción **motor de migración de datos del lado cliente** en el cuadro de diálogo **configuración del proyecto** .  
  
-   En **configuración del proyecto**, se establece la opción **motor de migración de datos del lado cliente** .  
  
    > [!NOTE]  
    > El **motor de migración de datos del lado cliente** reside dentro de la aplicación SSMA y, por lo tanto, no depende de la disponibilidad del paquete de extensión.  
  
**Migración de datos del lado servidor:**  
  
-   Durante la migración de datos del lado servidor, el motor reside en la base de datos de destino. Se instala a través del paquete de extensión. Para obtener más información sobre cómo instalar el paquete de extensión, consulte [instalación de componentes de SSMA en SQL Server](https://msdn.microsoft.com/cf2b724b-4ca7-470a-8dd7-fa95b1e060a4)  
  
-   Para iniciar la migración en el lado del servidor, seleccione la opción **motor de migración de datos del lado servidor** en el cuadro de diálogo **configuración del proyecto** .  
  
## <a name="migrating-data-to-sql-server"></a>Migrar datos a SQL Server  
La migración de datos es una operación de carga masiva que mueve filas de datos de tablas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DB2 a tablas de transacciones. El número de filas que se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cargan en cada transacción se configura en la configuración del proyecto.  
  
Para ver los mensajes de migración, asegúrese de que el panel de salida esté visible. En caso contrario, en el menú **Ver** , seleccione **salida**.  
  
**Para migrar datos**  
  
1.  Verifique lo siguiente:  
  
    -   Los proveedores de DB2 se instalan en el equipo que ejecuta SSMA.  
  
    -   Ha sincronizado los objetos convertidos con la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] base de datos.  
  
2.  En el explorador de metadatos DB2, seleccione los objetos que contienen los datos que desea migrar:  
  
    -   Para migrar datos de todos los esquemas, active la casilla situada junto a **esquemas**.  
  
    -   Para migrar datos u omitir tablas individuales, expanda primero el esquema, expanda **tablas**y, a continuación, Active o desactive la casilla situada junto a la tabla.  
  
3.  Para migrar datos, surgen dos casos:  
  
    **Migración de datos del lado cliente:**  
  
    -   Para realizar la **migración de datos del lado cliente**, seleccione la opción **motor de migración de datos del lado cliente** en el cuadro de diálogo **configuración del proyecto** .  
  
    **Migración de datos del lado servidor:**  
  
    -   Antes de realizar la migración de datos en el lado servidor, asegúrese de:  
  
        1.  El paquete de extensión SSMA para DB2 está instalado en la instancia [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]de.  
  
        2.  El servicio Agente SQL Server se está ejecutando en la instancia de SQL Server.  
  
    -   Para realizar la **migración de datos del lado servidor**, seleccione la opción **motor de migración de datos del lado servidor** en el cuadro de diálogo **configuración del proyecto** .  
  
4.  Haga clic con el botón secundario en **esquemas** en el explorador de metadatos DB2 y, a continuación, haga clic en **migrar datos**. También puede migrar datos para objetos individuales o categorías de objetos: haga clic con el botón secundario en el objeto o en su carpeta primaria; Seleccione la opción **migrar datos** .  
  
    > [!NOTE]  
    > Si el paquete de extensión SSMA para DB2 no está instalado en la instancia [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]de, y si el **motor de migración de datos del lado servidor** está seleccionado, al migrar los datos a la base de datos de destino, se produce el siguiente error: no se encontraron los componentes de migración de datos de SSMA en SQL Server, la migración de datos del servidor no será posible. Compruebe si el paquete de extensiones está instalado correctamente. Haga clic en **Cancelar** para finalizar la migración de datos.  
  
5.  En el cuadro de diálogo **conectar con DB2** , escriba las credenciales de conexión y, a continuación, haga clic en **conectar**. Para obtener más información sobre cómo conectarse a DB2, vea [conectarse a la base de datos db2 &#40;DB2ToSQL&#41;](../../ssma/db2/connecting-to-db2-database-db2tosql.md)  
  
    Para conectarse a la base de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]datos de destino, escriba las credenciales de conexión en el cuadro de diálogo **conectar con el SQL Server** y haga clic en **conectar**. Para obtener más información sobre cómo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]conectarse a, consulte [conexión a SQL Server](https://msdn.microsoft.com/b59803cb-3cc6-41cc-8553-faf90851410e)  
  
    Los mensajes aparecerán en el panel de **resultados** . Una vez completada la migración, aparece el **Informe de migración de datos** . Si no se migró ningún dato, haga clic en la fila que contiene los errores y, a continuación, haga clic en **detalles**. Cuando haya terminado con el informe, haga clic en **cerrar**. Para obtener más información sobre el informe de migración de datos, vea [Informe de migración de datos (SSMA Common)](https://msdn.microsoft.com/bbfb9d88-5a98-4980-8d19-c5d78bd0d241)  
  
> [!NOTE]  
> Cuando se utiliza SQL Express Edition como base de datos de destino, solo se permite la migración de datos del lado cliente y no se admite la migración de datos del lado servidor.  
  
## <a name="see-also"></a>Consulte también  
[Migración de datos de DB2 a SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-data-into-sql-server-db2tosql.md)  
  
