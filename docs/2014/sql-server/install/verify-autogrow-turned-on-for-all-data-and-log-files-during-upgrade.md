---
title: Comprobar que el crecimiento automático está activado para todos los archivos de datos y de registro durante el proceso de actualización | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- log files [SQL Server], size
- data files [SQL Server], size
- tempdb [SQL Server], size
- autogrow [SQL Server]
ms.assetid: a5860904-e2be-4224-8a51-df18a10d3fb9
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 8ca12075598bce210a905cbdfba89f2d879cf09b
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85065192"
---
# <a name="verify-autogrow-is-turned-on-for-all-data-and-log-files-during-the-upgrade-process"></a>Comprobar que autogrow está activo para todos los datos y archivos de registro durante el proceso de actualización
  El Asesor de actualizaciones detectó archivos de datos o de registro no configurados para crecimiento automático. Las características nuevas y mejoradas requieren espacio en disco adicional para las bases de datos de usuario y la base de datos del sistema **tempdb** . Para asegurarse de que los recursos pueden dar cabida a los aumentos de tamaño durante la actualización y las operaciones de producción posteriores, se recomienda configurar el crecimiento automático para todos los archivos de registro y datos de usuario, así como los archivos de registro y de datos de **tempdb** antes de actualizar.  
  
 Después de actualizar y probar las cargas de trabajo, puede ser conveniente desactivar el crecimiento automático o ajustar el incremento de FILEGROWTH en función de los archivos de datos de usuario y de registro. Se recomienda que el crecimiento automático permanezca activado para la base de datos del sistema **tempdb** . Para obtener más información, vea "Planear la capacidad para tempdb" en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Descripción  
 **Archivos de datos**  
  
 La tabla siguiente muestra una lista con los cambios realizados en las características de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que conllevan unos requisitos mayores en cuanto a espacio en disco para los archivos de datos definidos por el usuario.  
  
|Característica|Cambios realizados en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|-------------|-----------------------------------------------------|  
|Texto completo|La asignación del id. de documento (DOCID) se almacena en el archivo de datos en lugar de almacenarse en el catálogo de texto completo.|  
|Columnas `text`, `ntext` y `image`|Las columnas de objetos grandes (LOB) definidas como tipos de datos `text`, `ntext` o `image` necesitan un espacio en disco adicional de 40 bytes por columna. Este aumento de espacio único se produce durante la primera actualización de cada columna LOB.|  
|metadata|Los metadatos adicionales del sistema se crean y se mantienen en el grupo de archivos PRIMARY de cada una de las bases de datos de usuario para los objetos de base de datos y los permisos de usuario. Por ejemplo, en versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], los permisos asociados con el que los concede o con el beneficiario se almacenan en una fila única como mapa de bits. El mapa de bits se expande en varias filas.<br /><br /> Durante el proceso de actualización, debe haber suficiente espacio en disco para almacenar tanto los metadatos anteriores como los nuevos. Se eliminarán los metadatos anteriores después de que la actualización se haya completado.|  
  
 **Archivos de registro de transacciones**  
  
 La tabla siguiente muestra una lista con los cambios realizados en las características de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que conllevan unos requisitos mayores en cuanto a espacio en disco para los archivos de registro de transacciones definidos por el usuario.  
  
|Característica|Cambios realizados en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|-------------|-----------------------------------------------------|  
|Restauración y recuperación|Durante la fase de deshacer de una recuperación de errores, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite a los usuarios tener acceso a la base de datos. Esto es posible porque las transacciones que no estaban confirmadas cuando se produjo el error vuelven a adquirir los bloqueos que mantenían antes del error. Mientras se revierten estas transacciones, sus bloqueos las protegen de las interferencias de los usuarios. Esta información de bloqueo adicional debe conservarse en el registro de transacciones.|  
  
 **Datos y archivos de registro de tempdb**  
  
 En versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , la base de datos **tempdb** se utiliza para almacenar los objetos siguientes:  
  
-   Objetos temporales creados explícitamente, como tablas, procedimientos almacenados, variables de tabla o cursores.  
  
-   Tablas de trabajo internas creadas por [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
-   Resultados de ordenaciones temporales cuando se crean o se vuelven a generar índices, si se especifica SORT_IN_TEMPDB.  
  
 Los objetos adicionales también usan la base de datos **tempdb** . En la tabla siguiente se enumeran los cambios o las adiciones a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] las características que producen requisitos adicionales de espacio en disco para los archivos de datos y de registro de **tempdb** .  
  
|Característica|Cambios realizados en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|-------------|-----------------------------------------------------|  
|Versiones de fila|Las versiones de fila son un marco general de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se utiliza para lo siguiente:<br /><br /> Admitir desencadenadores: compilar las tablas insertadas y eliminadas en los desencadenadores. Se crean versiones de las filas modificadas por el desencadenador. Esto incluye las filas modificadas por la instrucción que activó el desencadenador, así como las modificaciones de datos realizadas por el desencadenador. Los desencadenadores AFTER utilizan el almacén de versiones de **tempdb** para almacenar las imágenes anteriores de las filas modificadas por el desencadenador. Al cargar datos de manera masiva con los desencadenadores habilitados, se agrega una copia de cada fila al almacén de versiones.<br /><br /> Compatibilidad con los conjuntos de resultados activos múltiples (MARS). Si una sesión MARS emite una instrucción de modificación de datos (como INSERT, UPDATE o DELETE) en un momento en el que hay un conjunto de resultados activos, se crean versiones de las filas afectadas por la instrucción de modificación.<br /><br /> Compatibilidad con las operaciones de índice que especifican la opción ONLINE. Las operaciones de índice en línea utilizan versiones de fila para aislar la operación de índice de los efectos de modificaciones efectuadas por otras transacciones. Así se evita la necesidad de solicitar que se compartan bloqueos en filas que se han leído. Además, las operaciones simultáneas de actualización y eliminación de usuarios durante las operaciones de índice en línea requieren espacio para registros de versión en **tempdb**.<br /><br /> Compatibilidad con los niveles de aislamiento de transacción basados en versiones de fila: una nueva implementación de nivel de aislamiento de lectura confirmada que utiliza las versiones de fila para proporcionar coherencia de lectura de nivel de instrucción. Nuevo nivel de aislamiento de instantánea que proporciona una coherencia de lectura en las transacciones.<br /><br /> <br /><br /> Las versiones de fila se mantienen en el almacén de versiones de **tempdb** el tiempo suficiente para satisfacer los requisitos de las transacciones que se ejecutan en los niveles de aislamiento basados en versiones de fila.<br /><br /> Para obtener más información sobre las versiones de fila y el almacén de versiones, vea la "Descripción de los niveles de aislamiento basados en versiones de fila" en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|Almacenar en memoria caché la tabla temp y los metadatos variables de temp|Para cada metadato de la tabla temporal y de la variable Temp almacenada en caché en la caché de metadatos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , se asignan dos páginas adicionales para **tempdb**.<br /><br /> Si un procedimiento almacenado o desencadenador crea una tabla temp o una variable temp, no se eliminará el objeto temporal cuando el procedimiento o el desencadenador finalicen su ejecución. En su lugar, el objeto temporal se trunca a una página y se reutiliza la próxima vez que se ejecute el procedimiento o el desencadenador.|  
|Índices en tablas con particiones|Cuando [!INCLUDE[ssDE](../../includes/ssde-md.md)] realiza la ordenación para generar índices con particiones, se necesita espacio suficiente para almacenar las ordenaciones intermedias de cada partición en **tempdb** si se especifica la opción de índice SORT_IN_TEMPDB.|  
|[!INCLUDE[ssSB](../../includes/sssb-md.md)]|[!INCLUDE[ssSB](../../includes/sssb-md.md)]utiliza explícitamente **tempdb** al conservar el contexto de diálogo existente que no puede permanecer en la memoria (aproximadamente 1 KB por cada cuadro de diálogo).<br /><br /> [!INCLUDE[ssSB](../../includes/sssb-md.md)]usa implícitamente **tempdb** mediante el almacenamiento en caché de objetos en el contexto de la ejecución de la consulta. Por ejemplo, las tablas de trabajo utilizadas para los eventos del temporizador y las conversaciones entregadas en segundo plano.<br /><br /> Las características DBMail, notificaciones de eventos y notificaciones de consultas utilizan implícitamente [!INCLUDE[ssSB](../../includes/sssb-md.md)].|  
|Tipos de datos de objetos grandes (LOB)<br /><br /> Variables y parámetros LOB|Los tipos de datos `varchar(max)` , `nvarchar(max)` , el **texto varbinary (Max)**, `ntext` `image,` y `xml` son tipos de objetos grandes.<br /><br /> Cuando se habilita un nivel de aislamiento de transacción basado en versiones de fila en la base de datos y se realizan modificaciones de objetos grandes, el fragmento cambiado del LOB se copia en el almacén de versiones de **tempdb**.<br /><br /> Los parámetros definidos como un tipo de datos de objetos grandes se almacenan en **tempdb**.|  
|Expresiones de tabla comunes (CTE)|Las tablas de trabajo temporales para las operaciones de cola se crean en **tempdb** cuando se ejecutan consultas de expresiones de tabla comunes.|  
  
## <a name="corrective-action"></a>Acción correctora  
 Para establecer un archivo de datos o de registro en autogrow, modifique las instrucciones siguientes para especificar los datos y el registro de la base de datos. Debería ajustar el incremento de FILEGROWTH a un valor que sea adecuado para la situación.  
  
```  
ALTER DATABASE tempdb  
MODIFY FILE  
    (NAME = tempdev,  
    FILEGROWTH = 20MB);  
GO  
ALTER DATABASE tempdb  
MODIFY FILE  
    (NAME = templog,  
    FILEGROWTH = 10MB);  
```  
  
 El incremento predeterminado para el crecimiento de los archivos de datos es de 1 MB. El valor predeterminado para el archivo de registro es 10%. Se recomienda seguir estas directrices generales a la hora de establecer el incremento de FILEGROWTH.  
  
|Tamaño de archivo|Incremento de FILEGROWTH|  
|---------------|--------------------------|  
|0:50 MB|10 MB|  
|100-200 MB|20 MB|  
|500 MB o más|10 %|  
  
## <a name="see-also"></a>Consulte también  
 [Problemas de actualización Motor de base de datos](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server el asesor de actualizaciones de 2014 &#91;nuevo&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
