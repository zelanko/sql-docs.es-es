---
title: Requisitos para usar las tablas con optimización para memoria | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 47d9a7e8-c597-4b95-a58a-dcf66df8e572
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 314f90a482091823efae4430dbdc2d62ad7b34f4
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48073915"
---
# <a name="requirements-for-using-memory-optimized-tables"></a>Requisitos para utilizar las tablas con optimización para memoria
  Además el [requisitos de Hardware y Software para instalar SQL Server 2014](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md), los siguientes son requisitos para usar OLTP en memoria:  
  
-   Edición Enterprise de 64 bits, Developer o Evaluation de [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)].  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] necesita suficiente memoria para almacenar los datos en tablas optimizadas para memoria e índices. Para tener en cuenta las versiones de fila, debe proporcionar una cantidad de memoria que sea dos veces el tamaño esperado de las tablas e índices optimizados para memoria. Pero la cantidad de memoria necesaria real dependerá de la carga de trabajo. Debe supervisar el uso de la memoria y realizar ajustes según sea necesario. El tamaño de los datos en las tablas optimizadas para memoria no puede superar el porcentaje permitido del grupo. Para conocer el tamaño de una tabla optimizada para memoria, consulte [sys.dm_db_xtp_table_memory_stats &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-xtp-table-memory-stats-transact-sql).  
  
     Si la base de datos tiene tablas basadas en disco, debe proporcionar suficiente memoria para el grupo de búferes y el procesamiento de consultas de esas tablas.  
  
     Es importante conocer la cantidad de memoria que requerirá la aplicación OLTP en memoria. Vea [Estimar los requisitos de memoria para las tablas con optimización para memoria](memory-optimized-tables.md) para obtener más información.  
  
-   Espacio en disco libre equivalente al doble del tamaño de las tablas durables optimizadas para memoria.  
  
-   El procesador debe admitir la instrucción **cmpxchg16b** para utilizar OLTP en memoria. Todos los procesadores de 64 bits modernos admiten la instrucción **cmpxchg16b**.  
  
     Si usa una aplicación de host de máquina virtual y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] muestra un error provocado por un procesador anterior, compruebe si la aplicación tiene una opción de configuración para permitir **cmpxchg16b**. Si no, puede usar Hyper-V, que admite **cmpxchg16b** sin necesidad de modificar ninguna opción de configuración.  
  
-   Para instalar OLTP en memoria, seleccione **servicios de motor de base de datos** al instalar [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  
     Para instalar la generación de informes ([determinar si una tabla o procedimiento almacenado debe ser pasar a OLTP en memoria](determining-if-a-table-or-stored-procedure-should-be-ported-to-in-memory-oltp.md)) y [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] (para administrar OLTP en memoria mediante [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] Explorador de objetos), seleccione **administración Herramientas: básica** o **las herramientas de administración: Advanced** al instalar [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  
## <a name="important-notes-on-using-includehek2includeshek-2-mdmd"></a>Información importante sobre el uso de [!INCLUDE[hek_2](../../../includes/hek-2-md.md)]  
  
-   El tamaño total en memoria de todas las tablas durables de una base de datos no debe superar los 250 GB. Para obtener más información, consulte [durabilidad de las tablas con optimización para memoria](durability-for-memory-optimized-tables.md).  
  
-   Esta versión de [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] está diseñada para ofrecer un rendimiento óptimo en sistemas de 2 o 4 sockets y menos de 60 núcleos.  
  
-   Los archivos de puntos de comprobación no se deben eliminar manualmente. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] realiza automáticamente la recolección de elementos no utilizados en los archivos de puntos de comprobación innecesarios. Para obtener más información, vea la explicación sobre la combinación de archivos delta y datos de [durabilidad de las tablas con optimización para memoria](durability-for-memory-optimized-tables.md).  
  
-   En esta primera versión de OLTP en memoria (en [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]), la única forma de quitar un grupo de archivos optimizados para memoria es colocar la base de datos.  
  
-   Si intenta eliminar un lote grande de filas mientras haya una carga de trabajo de inserción o actualización que afecte al intervalo de filas que intenta eliminar, lo más probable es que la eliminación no se realice correctamente. La solución alternativa es detener la carga de trabajo de inserción o actualización antes de eliminar. Por otra parte, también puede configurar la transacción en transacciones más pequeñas, lo que comporta menos riesgos de interrupción por cargas de trabajo simultánea. Como con todas las operaciones de escritura en tablas optimizadas para memoria, debe usar lógica de reintento ([Guidelines for Retry Logic para las transacciones en tablas optimizadas para memoria](../../database-engine/guidelines-for-retry-logic-for-transactions-on-memory-optimized-tables.md)).  
  
-   Si crea una o más bases de datos con tablas optimizadas para memoria, debe habilitar la inicialización instantánea de archivos (conceda el derecho de usuario SE_MANAGE_VOLUME_NAME a la cuenta de inicio del servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]) para la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Sin la inicialización instantánea de archivos, los archivos de almacenamiento optimizados para memoria (datos y archivos delta) se inicializarán en el momento de la creación, lo cual puede tener un impacto negativo en el rendimiento de la carga de trabajo. Para obtener más información sobre la inicialización instantánea de archivos, vea [Inicialización de archivos de base de datos](../databases/database-instant-file-initialization.md). Para obtener información sobre cómo habilitar la inicialización instantánea de archivos, vea [Cómo y por qué habilitar la inicialización instantánea de archivos](http://blogs.msdn.com/b/sql_pfe_blog/archive/2009/12/23/how-and-why-to-enable-instant-file-initialization.aspx).  
  
## <a name="did-this-article-help-you-were-listening"></a>¿Le ayudó este artículo? Le escuchamos  
 ¿Qué información está buscando? ¿La encontró? Escuchamos sus comentarios para mejorar el contenido. Envíe sus comentarios a [ sqlfeedback@microsoft.com ](mailto:sqlfeedback@microsoft.com?subject=Your%20feedback%20about%20the%20Requirements%20for%20Using%20Memory-Optimized%20Tables%20page).  
  
## <a name="see-also"></a>Vea también  
 [OLTP en memoria &#40;optimización en memoria&#41;](in-memory-oltp-in-memory-optimization.md)  
  
  
