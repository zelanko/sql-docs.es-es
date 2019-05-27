---
title: Compatibilidad de FileTable con otras características de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FileTables [SQL Server], using with other features
ms.assetid: f12a17e4-bd3d-42b0-b253-efc36876db37
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: c8ea6a5fcfe99926c264fc2116a637f8d30c05df
ms.sourcegitcommit: 45a9d7ffc99502c73f08cb937cbe9e89d9412397
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/22/2019
ms.locfileid: "66010153"
---
# <a name="filetable-compatibility-with-other-sql-server-features"></a>Compatibilidad de FileTable con otras características de SQL Server
  Describe el funcionamiento de FileTables con otras características de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
##  <a name="alwayson"></a> Grupos de disponibilidad AlwaysOn y FileTables  
 Cuando la base de datos que contiene datos de FILESTREAM o FileTable pertenece a un grupo de disponibilidad AlwaysOn:  
  
-   [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]admite parcialmente la funcionalidad de FileTable. Después de una conmutación por error, es posible tener acceso a los datos de FileTable en la réplica principal, pero no en las réplicas secundarias legibles.  
  
    > [!NOTE]  
    >  Observe que, después de una conmutación por error, se admite toda la funcionalidad de FILESTREAM. Los datos de FILESTREAM son accesibles tanto en las réplicas secundarias legibles como en la nueva réplica principal.  
  
-   Las funciones FILESTREAM y FileTable aceptan o devuelven nombres de red virtual (VNN) en lugar de nombres de equipo. Para obtener más información sobre estas funciones, vea [Funciones FILESTREAM y FileTable &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/filestream-and-filetable-functions-transact-sql).  
  
-   Todo acceso a los datos de FILESTREAM o FileTable a través de las API del sistema de archivos debe utilizar VNN en lugar de nombres de equipo. Para obtener más información, vea [FILESTREAM y FileTable con grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/filestream-and-filetable-with-always-on-availability-groups-sql-server.md).  
  
##  <a name="OtherPartitioning"></a> Particiones y FileTables  
 FileTables no admite la creación de particiones. Con la compatibilidad con varios grupos de archivos FILESTREAM, los problemas de ampliación se pueden administrar sin tener que recurrir a la creación de particiones en la mayoría de los escenarios (a diferencia de FILESTREAM de SQL 2008).  
  
##  <a name="OtherRepl"></a> Replicación y FileTables  
 La replicación y las características relacionadas (incluidos la replicación transaccional, la replicación de mezcla, la captura de datos modificados y el seguimiento de cambios) no se admiten con FileTables.  
  
##  <a name="OtherIsolation"></a> Semántica de transacción y FileTables  
 **aplicaciones para Windows**  
 Las aplicaciones Windows no entienden las transacciones de base de datos; por lo tanto, las operaciones de escritura de Windows no proporcionan las propiedades ACID de una transacción de base de datos. Por consiguiente, las reversiones y la recuperación transaccionales no son posibles con operaciones de actualización de Windows.  
  
 **Aplicaciones de Transact-SQL**  
 Para las aplicaciones de TSQL que funcionen en la columna FILESTREAM (file_stream) de una FileTable, la semántica de aislamiento es la misma que con el tipo de datos FILESTREAM de una tabla de usuario normal.  
  
##  <a name="OtherQueryNot"></a> Notificaciones de consulta y FileTables  
 La consulta no puede contener ninguna referencia a la columna FILESTREAM de la FileTable en la cláusula WHERE ni en ninguna otra parte de la consulta.  
  
##  <a name="OtherSelectInto"></a> SELECT INTO y FileTables  
 Las instrucciones SELECT INTO de una FileTable no propagarán la semántica de la FileTable en la tabla de destino creada (al igual que las columnas FILESTREAM de una tabla regular). Todas las columnas de destino de la tabla se comportarán como columnas normales. No tendrán ninguna semántica de FileTable asociada a ellas.  
  
##  <a name="OtherTriggers"></a> Desencadenadores y FileTables  
 **Desencadenadores DDL (lenguaje de definición de datos)**  
 No existen consideraciones especiales para los desencadenadores DDL con las FileTables. Los desencadenadores DDL normales desencadenarán operaciones CREAT o ALTER DATABASE, así como operaciones CREATE o ALTER TABLE para FileTables. Los desencadenadores pueden recuperar los datos de eventos reales que incluyan el texto de comandos DDL e información adicional, llamando a la función EVENTDATA(). No existen eventos nuevos ni cambios en el esquema Eventdata existente.  
  
 **Desencadenadores DML (lenguaje de manipulación de datos)**  
 Estas restricciones se aplicarán durante la operación DDL para crear desencadenadores.  
  
-   Las FileTables NO admitirán desencadenadores INSTEAD OF para operaciones DML. Se trata de una restricción existente en todas las tablas que contengan columnas FILESTREAM.  
  
-   Las FileTables sí admitirán desencadenadores AFTER para operaciones DML.  
  
-   Los desencadenadores definidos en una FileTable no pueden actualizar ninguna FileTable, incluida la FileTable primaria. Esta restricción existe principalmente para impedir que un desencadenador entre en conflictos de bloqueo con los bloqueos mantenidos por el acceso al sistema de archivos de la misma transacción.  
  
 **Acceso no transaccional y sus efectos en los desencadenadores**  
 -   Cuando se permite el acceso de actualización no transaccional en una base de datos, se puede realizar una actualización en contexto de los datos de FILESTREAM en cualquier tabla, incluida la tabla FileTable de esa base de datos. Debido a esta posibilidad, puede que la imagen anterior del contenido de FILESTREAM no esté disponible para que la use el desencadenador.  
  
-   En operaciones de actualización no transaccional a través del sistema de archivos, SQL Server creará una transacción interna para capturar la operación CloseHandle y se pueden activar los desencadenadores DML definidos como parte de esa transacción. No se evitará una reversión en una transacción dentro del cuerpo del desencadenador, pero no se revierten los cambios realizados en la FILESTREAM.  Este intento de reversión también puede impedir que se activen los desencadenadores UPDATE, aunque el contenido de FILESTREAM pueda haber cambiado.  
  
-   Además de estos impactos, los desencadenadores de las FileTables deben ocuparse de un par de comportamientos adicionales  
  
    -   En el caso de operaciones de actualización no transaccional de una FileTable a través del sistema de archivos, es posible que el contenido de FILESTREAM esté bloqueado exclusivamente por otras operaciones de Win32 y quizá no se pueda acceder a él para operaciones de lectura y escritura a través del cuerpo del desencadenador. En casos como este, cualquier intento de acceso al contenido de FILESTREAM dentro del cuerpo del desencadenador puede provocar un error de "Infracción de uso compartido". Los desencadenadores se deben diseñar para controlar ese tipo de errores apropiadamente.  
  
    -   La imagen AFTER de FILESTREAM quizá no sea estable porque, en algunos casos, otras actualizaciones no transaccionales pueden escribir activamente en ella al mismo tiempo, debido a los modos de uso compartido permitidos en el acceso al sistema de archivos.  
  
-   La terminación anómala de los identificadores Win32, como eliminar explícitamente los identificadores Win32 por parte de un administrador O un bloqueo de la base de datos, no ejecutará desencadenadores de usuario durante las operaciones de recuperación, aunque quizá la terminación anómala de la aplicación pueda haber cambiado el contenido de FILESTREAM.  
  
##  <a name="OtherViews"></a> Vistas y FileTables  
 **Vistas**  
 Una vista se puede crear en una FileTable como en cualquier otra tabla. Sin embargo, las siguientes consideraciones se aplican a una vista creada en una FileTable:  
  
-   La vista no tendrá semántica de FileTable. Es decir, las columnas de la vista (incluidas las columnas de atributos de archivo) se comportan como columnas de vistas normales sin ninguna semántica especial y lo mismo se aplica a las filas que representen archivos y directorios.  
  
-   La vista se puede actualizar en función de la semántica de "vista actualizable", pero las restricciones de la tabla subyacente pueden rechazar las actualizaciones como en la tabla.  
  
-   La ruta de acceso al archivo de un archivo se puede mostrar agregándola como columna explícita en la vista. Por ejemplo:  
  
     `CREATE VIEW MP3FILES AS SELECT column1, column2, ..., GetFileNamespacePath() AS PATH, column3,...  FROM Documents`  
  
 **Vistas indizadas**  
 Las vistas indizadas actualmente no pueden incluir columnas FILESTREAM ni columnas calculadas o columnas calculadas persistentes que dependan de las columnas FILESTREAM. Además, este comportamiento se mantiene sin cambios con las vistas definidas en la FileTable.  
  
##  <a name="OtherSnapshots"></a> Aislamiento de instantánea y FileTables  
 El aislamiento de instantánea de lectura confirmada (RCSI) y el aislamiento de instantánea (SI) confían en la posibilidad de disponer de una instantánea de los datos disponibles para los lectores aunque se produzcan operaciones de actualización en los datos. Sin embargo, las FileTables permiten el acceso de escritura no transaccional a los datos de secuencia de archivo. Como resultado, las siguientes restricciones se aplican al uso de estas características de base de datos que contenga FileTables:  
  
-   Una base de datos que contiene FileTables se puede modificar para habilitar RCSI/SI.  
  
-   Cuando el acceso no transaccional se establece en FULL para la base de datos, una transacción que se ejecuta en RCSI o SI se comporta de la siguiente forma:  
  
    -   Se producirá un error de lectura de [!INCLUDE[tsql](../../../includes/tsql-md.md)] en la columna file_stream deFileTable. INSERT y UPDATE se seguirán ejecutando correctamente en la columna, en tanto en cuanto no lean en la columna file_stream.  
  
    -   Si la instrucción [!INCLUDE[tsql](../../../includes/tsql-md.md)] especifica sugerencias de tabla READCOMMITTEDLOCK, las lecturas se realizarán correctamente y se aplicarán bloqueos a las filas, en vez de usar las versiones de fila.  
  
    -   Además, se producirá un error en las solicitudes de apertura de FileStream de Win32 con transacciones.  
  
    -   El acceso de Win32 de FileTable sin transacciones se ejecutará correctamente. No se verán afectadas las consultas internas realizadas por FileTable.  
  
    -   La indización de texto completo siempre se realizará correctamente, independientemente de cuáles sean las opciones de la base de datos (READ_COMMITTED_SNAPSHOT o ALLOW_SNAPSHOT_ISOLATION).  
  
##  <a name="readsec"></a> Bases de datos secundarias legibles  
 Las mismas consideraciones se aplican a las bases de datos secundarias legibles en cuanto a las instantáneas, como se describe en la sección anterior, [Aislamiento de instantánea y FileTables](#OtherSnapshots).  
  
##  <a name="CDB"></a> Bases de datos independientes y FileTables  
 La característica FILESTREAM de la función de FileTable depende requiere cierta configuración fuera de la base de datos. Por consiguiente, una base de datos que utiliza FILESTREAM o FileTable no es totalmente contenida.  
  
 Puede establecer la contención de la base de datos en PARTIAL si desea utilizar algunas características de bases de datos contenidas, como usuarios contenidos. Sin embargo, en este caso, debe tener en cuenta que algunas de las opciones de base de datos no están contenidas en la base de datos y no se mueven automáticamente cuando lo hace la base de datos.  
  
## <a name="see-also"></a>Vea también  
 [Administrar FileTables](manage-filetables.md)  
  
  
