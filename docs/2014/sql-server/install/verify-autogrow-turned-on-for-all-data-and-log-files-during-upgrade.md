---
title: Compruebe el crecimiento automático está activado para todos los archivos de registro y datos durante el proceso de actualización | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- log files [SQL Server], size
- data files [SQL Server], size
- tempdb [SQL Server], size
- autogrow [SQL Server]
ms.assetid: a5860904-e2be-4224-8a51-df18a10d3fb9
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ab29cc94071b95f6ff8cffb95902851d1796ed80
ms.sourcegitcommit: 46a2c0ffd0a6d996a3afd19a58d2a8f4b55f93de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/15/2019
ms.locfileid: "59583278"
---
# <a name="verify-autogrow-is-turned-on-for-all-data-and-log-files-during-the-upgrade-process"></a>Comprobar que autogrow está activo para todos los datos y archivos de registro durante el proceso de actualización
  El Asesor de actualizaciones detectó archivos de datos o de registro no configurados para crecimiento automático. Características nuevas y mejoradas requieren espacio en disco adicional para bases de datos de usuario y la **tempdb** base de datos del sistema. Para asegurarse de que los recursos pueden aceptar los aumentos de tamaño durante la actualización y las operaciones de producción posteriores, se recomienda habilitar el crecimiento automático en ON para todos los archivos de registro y datos de usuario y la **tempdb** antes de actualizar los archivos de datos y de registro.  
  
 Después de actualizar y probar las cargas de trabajo, puede ser conveniente desactivar el crecimiento automático o ajustar el incremento de FILEGROWTH en función de los archivos de datos de usuario y de registro. Es recomendable que autogrow permanezca activado para la **tempdb** base de datos del sistema. Para obtener más información, vea "Planear la capacidad para tempdb" en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Descripción  
 **Archivos de datos**  
  
 La tabla siguiente muestra una lista con los cambios realizados en las características de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que conllevan unos requisitos mayores en cuanto a espacio en disco para los archivos de datos definidos por el usuario.  
  
|Característica|Cambios realizados en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|-------------|-----------------------------------------------------|  
|Texto completo|La asignación del id. de documento (DOCID) se almacena en el archivo de datos en lugar de almacenarse en el catálogo de texto completo.|  
|Columnas `text`, `ntext` y `image`|Las columnas de objetos grandes (LOB) definidas como tipos de datos `text`, `ntext` o `image` necesitan un espacio en disco adicional de 40 bytes por columna. Este aumento de espacio único se produce durante la primera actualización de cada columna LOB.|  
|metadatos|Los metadatos adicionales del sistema se crean y se mantienen en el grupo de archivos PRIMARY de cada una de las bases de datos de usuario para los objetos de base de datos y los permisos de usuario. Por ejemplo, en versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], los permisos asociados con el que los concede o con el beneficiario se almacenan en una fila única como mapa de bits. El mapa de bits se expande en varias filas.<br /><br /> Durante el proceso de actualización, debe haber suficiente espacio en disco para almacenar tanto los metadatos anteriores como los nuevos. Se eliminarán los metadatos anteriores después de que la actualización se haya completado.|  
  
 **Archivos de registro de transacciones**  
  
 La tabla siguiente muestra una lista con los cambios realizados en las características de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que conllevan unos requisitos mayores en cuanto a espacio en disco para los archivos de registro de transacciones definidos por el usuario.  
  
|Característica|Cambios realizados en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|-------------|-----------------------------------------------------|  
|Restauración y recuperación|Durante la fase de deshacer de una recuperación de errores, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite a los usuarios tener acceso a la base de datos. Esto es posible porque las transacciones que no estaban confirmadas cuando se produjo el error vuelven a adquirir los bloqueos que mantenían antes del error. Mientras se revierten estas transacciones, sus bloqueos las protegen de las interferencias de los usuarios. Esta información de bloqueo adicional debe conservarse en el registro de transacciones.|  
  
 **archivos de registro y datos de tempdb**  
  
 En versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], **tempdb** base de datos se usa para almacenar los objetos siguientes:  
  
-   Objetos temporales creados explícitamente, como tablas, procedimientos almacenados, variables de tabla o cursores.  
  
-   Tablas de trabajo internas creadas por [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
-   Resultados de ordenaciones temporales cuando se crean o se vuelven a generar índices, si se especifica SORT_IN_TEMPDB.  
  
 Objetos adicionales también usan el **tempdb** base de datos. En la tabla siguiente se enumera los cambios o adiciones en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] disco de las características que conllevan unos requisitos de espacio para **tempdb** archivos de registro y datos.  
  
|Característica|Cambios realizados en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|-------------|-----------------------------------------------------|  
|Versiones de fila|Las versiones de fila son un marco general de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se utiliza para lo siguiente:<br /><br /> Admite desencadenadores: Crear las tablas inserted y deleted en desencadenadores. Se crean versiones de las filas modificadas por el desencadenador. Esto incluye las filas modificadas por la instrucción que activó el desencadenador, así como las modificaciones de datos realizadas por el desencadenador. Desencadenadores AFTER utilizan el almacén de versiones de **tempdb** para almacenar las imágenes anteriores de las filas modificadas por el desencadenador. Al cargar datos de manera masiva con los desencadenadores habilitados, se agrega una copia de cada fila al almacén de versiones.<br /><br /> Compatibilidad con los conjuntos de resultados activos múltiples (MARS). Si una sesión MARS emite una instrucción de modificación de datos (como INSERT, UPDATE o DELETE) en un momento en el que hay un conjunto de resultados activos, se crean versiones de las filas afectadas por la instrucción de modificación.<br /><br /> Compatibilidad con las operaciones de índice que especifican la opción ONLINE. Las operaciones de índice en línea utilizan versiones de fila para aislar la operación de índice de los efectos de modificaciones efectuadas por otras transacciones. Así se evita la necesidad de solicitar que se compartan bloqueos en filas que se han leído. Además, usuario simultáneas actualizar y eliminar operaciones de índice en línea durante la operaciones requieren espacio para registros de versión en **tempdb**.<br /><br /> Compatibilidad con los niveles de aislamiento de transacción basados en versiones de fila: Nueva implementación del nivel de aislamiento de lectura confirmada que utiliza las versiones de fila para proporcionar una coherencia de lectura en las instrucciones. Nuevo nivel de aislamiento de instantánea que proporciona una coherencia de lectura en las transacciones.<br /><br /> <br /><br /> Las versiones de fila se conservan en el **tempdb** suficiente como para satisfacer los requisitos de las transacciones ejecutadas con niveles de aislamiento basados en versiones de fila de almacén de versiones.<br /><br /> Para obtener más información sobre las versiones de fila y el almacén de versiones, vea la "Descripción de los niveles de aislamiento basados en versiones de fila" en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|Almacenar en memoria caché la tabla temp y los metadatos variables de temp|Para todos los metadatos de la tabla temporal y variable temp almacenados en la caché de metadatos por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se asignan dos páginas adicionales para **tempdb**.<br /><br /> Si un procedimiento almacenado o desencadenador crea una tabla temp o una variable temp, no se eliminará el objeto temporal cuando el procedimiento o el desencadenador finalicen su ejecución. En su lugar, el objeto temporal se trunca a una página y se reutiliza la próxima vez que se ejecute el procedimiento o el desencadenador.|  
|Índices en tablas con particiones|Cuando el [!INCLUDE[ssDE](../../includes/ssde-md.md)] realiza una ordenación para generar los índices con particiones, espacio suficiente para albergar las ordenaciones intermedias de cada partición se requiere en **tempdb** si se especifica la opción de índice SORT_IN_TEMPDB.|  
|[!INCLUDE[ssSB](../../includes/sssb-md.md)]|[!INCLUDE[ssSB](../../includes/sssb-md.md)] usa explícitamente **tempdb** hora de conservar el contexto del diálogo existente que no puede retenerse en memoria (aproximadamente 1 KB por cuadro de diálogo).<br /><br /> [!INCLUDE[ssSB](../../includes/sssb-md.md)] usa implícitamente **tempdb** mediante el almacenamiento en caché de objetos en el contexto de ejecución de la consulta. Por ejemplo, las tablas de trabajo utilizadas para los eventos del temporizador y las conversaciones entregadas en segundo plano.<br /><br /> Las características DBMail, notificaciones de eventos y notificaciones de consultas utilizan implícitamente [!INCLUDE[ssSB](../../includes/sssb-md.md)].|  
|Tipos de datos de objetos grandes (LOB)<br /><br /> Variables y parámetros LOB|Los tipos de datos `varchar(max)`, `nvarchar(max)`, **texto varbinary (max)**, `ntext`, `image,` y `xml` son tipos de objetos grandes.<br /><br /> Cuando está habilitado un nivel de aislamiento de transacción basado en versiones de fila en la base de datos y se realizan modificaciones de objetos grandes, el fragmento cambiado del LOB se copia en el almacén de versiones en **tempdb**.<br /><br /> Los parámetros definidos como un tipo de datos de objetos grandes se almacenan en **tempdb**.|  
|Expresiones de tabla comunes (CTE)|Tablas de trabajo temporales para las operaciones de cola se crean en **tempdb** cuando se ejecutan consultas de expresiones de tabla comunes.|  
  
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
|0-50MB|10MB|  
|100-200 MB|20MB|  
|500 MB o más|10%|  
  
## <a name="see-also"></a>Vea también  
 [Problemas de actualización de motor de base de datos](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Asesor de actualizaciones de SQL Server 2014 &#91;nuevo&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
