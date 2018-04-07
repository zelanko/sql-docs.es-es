---
title: Migrar datos de DB2 en SQL Server (DB2ToSQL) | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-db2
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 86cbd39f-6dac-409a-9ce1-7dd54403f84b
caps.latest.revision: 5
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0714e217aff8f6aa728bbc401472b9b538add968
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/06/2018
---
# <a name="migrating-db2-data-into-sql-server-db2tosql"></a>Migrar datos de DB2 en SQL Server (DB2ToSQL)
Después de haber sincronizado correctamente los objetos convertidos con [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], puede migrar datos de DB2 a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
> [!IMPORTANT]  
> Si el motor que se va a usar motor de migración de datos de lado de servidor, a continuación, antes de poder migrar datos, debe instalar SSMA para paquete de extensión de DB2 y los proveedores de DB2 en el equipo que está ejecutando SSMA. También debe ejecutar el servicio Agente SQL Server. Para obtener más información acerca de cómo instalar el paquete de extensión, vea [instalar componentes de SSMA en SQL Server](http://msdn.microsoft.com/en-us/cf2b724b-4ca7-470a-8dd7-fa95b1e060a4)  
  
## <a name="setting-migration-options"></a>Establecer las opciones de migración  
Antes de migrar datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], revise las opciones de migración de proyecto en el **configuración del proyecto** cuadro de diálogo.  
  
-   Mediante este cuadro de diálogo puede establecer opciones como el tamaño de lote de migración, bloqueo de tablas, comprobación de restricciones, tratamiento de los valores null y control de valor de identidad. Para obtener más información acerca de las opciones de migración de proyecto, vea [configuración del proyecto (migración)](http://msdn.microsoft.com/en-us/48aaa8e6-a9cb-487d-9ba5-fc3f1c4786ae).  
  
-   El **motor de migración de** en el **configuración del proyecto** permite al usuario realizar el proceso de migración con dos tipos de motores de migración de datos de cuadro de diálogo:  
  
    1.  Motor de migración de datos de lado cliente  
  
    2.  Motor de migración de datos de lado de servidor  
  
**Migración de datos del lado cliente:**  
  
-   Para iniciar la migración de datos en el lado del cliente, seleccione la **motor de migración de datos de lado cliente** opción en el **configuración del proyecto** cuadro de diálogo.  
  
-   En **configuración del proyecto**, **motor de migración de datos de lado cliente** opción está establecida.  
  
    > [!NOTE]  
    > El **motor de migración de datos de cliente** reside dentro de la aplicación de SSMA y es, por lo tanto, no depende de la disponibilidad del módulo de extensión.  
  
**Migración de datos del lado servidor:**  
  
-   Durante la migración de datos del lado servidor, el motor reside en la base de datos de destino. Se instala a través del módulo de extensión. Para obtener más información sobre cómo instalar el módulo de extensión, vea [instalar componentes de SSMA en SQL Server](http://msdn.microsoft.com/en-us/cf2b724b-4ca7-470a-8dd7-fa95b1e060a4)  
  
-   Para iniciar la migración en el servidor, seleccione la **motor de migración de datos de lado servidor** opción en el **configuración del proyecto** cuadro de diálogo.  
  
## <a name="migrating-data-to-sql-server"></a>Migrar datos a SQL Server  
Migración de datos están una operación de carga masiva que mueve filas de datos de tablas de DB2 en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tablas en las transacciones. El número de filas que se carga en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] en cada transacción se configura en la configuración del proyecto.  
  
Para ver mensajes de migración, asegúrese de que esté visible el panel de resultados. En caso contrario, desde el **vista** menú, seleccione **salida**.  
  
**Para migrar datos**  
  
1.  Compruebe lo siguiente:  
  
    -   Los proveedores de DB2 se instalan en el equipo que está ejecutando SSMA.  
  
    -   Se han sincronizado los objetos convertidos con el [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] base de datos.  
  
2.  En el Explorador de metadatos de DB2, seleccione los objetos que contienen los datos que se van a migrar:  
  
    -   Para migrar datos de todos los esquemas, active la casilla situada junto a **esquemas**.  
  
    -   Para migrar datos o se omite las tablas individuales, expanda el esquema, expanda **tablas**y, a continuación, active o desactive la casilla situada junto a la tabla.  
  
3.  Para migrar datos, surgen dos casos:  
  
    **Migración de datos del lado cliente:**  
  
    -   Para llevar a cabo **migración de datos del lado cliente**, seleccione la **motor de migración de datos de lado cliente** opción en el **configuración del proyecto** cuadro de diálogo.  
  
    **Migración de datos del lado servidor:**  
  
    -   Antes de realizar la migración de datos en el servidor, asegúrese de:  
  
        1.  SSMA para DB2: paquete de extensión se instala en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
        2.  El servicio Agente SQL Server se está ejecutando en la instancia de SQL Server.  
  
    -   Para llevar a cabo **migración de datos del lado servidor**, seleccione la **motor de migración de datos de lado servidor** opción en el **configuración del proyecto** cuadro de diálogo.  
  
4.  Haga clic en **esquemas** en el Explorador de metadatos de DB2 y, a continuación, haga clic en **migrar datos**. También puede migrar datos de objetos individuales o las categorías de objetos: haga clic en el objeto o su carpeta principal; Seleccione el **migrar datos** opción.  
  
    > [!NOTE]  
    > Si no está instalado el SSMA para DB2: paquete de extensión en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]y si **motor de migración de datos de lado servidor** está seleccionada, a continuación, al migrar los datos a la base de datos de destino, se produjo el siguiente error: ' componentes de migración de datos de SSMA no se encontraron en SQL Server, migración de datos en el servidor no podrá realizarse. Compruebe si el módulo de extensión está instalado correctamente ". Haga clic en **cancelar** para terminar la migración de datos.  
  
5.  En el **conectar a DB2** cuadro de diálogo, escriba las credenciales de conexión y, a continuación, haga clic en **conectar**. Para obtener más información sobre cómo conectarse a DB2, vea [conectarse a la base de datos DB2 &#40;DB2ToSQL&#41;](../../ssma/db2/connecting-to-db2-database-db2tosql.md)  
  
    Para conectarse a la base de datos de destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], escriba las credenciales de conexión en el **conectar con SQL Server** cuadro de diálogo y haga clic en **conectar**. Para obtener más información sobre cómo conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], consulte [conectarse a SQL Server](http://msdn.microsoft.com/en-us/b59803cb-3cc6-41cc-8553-faf90851410e)  
  
    Mensajes aparecerán en la **salida** panel. Una vez completada, la migración del **informe de migración de datos** aparece. Si no se ha migrado los datos, haga clic en la fila que contiene los errores y, a continuación, haga clic en **detalles**. Cuando haya terminado con el informe, haga clic en **cerrar**. Para obtener más información sobre informes de migración de datos, vea [informe de migración de datos (SSMA común)](http://msdn.microsoft.com/en-us/bbfb9d88-5a98-4980-8d19-c5d78bd0d241)  
  
> [!NOTE]  
> Cuando se utiliza SQL Express edition como la base de datos de destino, se permite la migración de datos de lado a solo cliente y no se admite la migración de datos del lado servidor.  
  
## <a name="see-also"></a>Vea también  
[Migrar datos de DB2 en SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-data-into-sql-server-db2tosql.md)  
  
