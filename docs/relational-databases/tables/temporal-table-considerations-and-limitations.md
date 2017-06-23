---
title: Limitaciones y consideraciones de las tablas temporales | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 05/22/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-tables
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c8a21481-0f0e-41e3-a1ad-49a84091b422
caps.latest.revision: 18
author: CarlRabeler
ms.author: carlrab
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 30791ad9733446f664db1592b95d1ffec5fc9a1b
ms.openlocfilehash: 5ee3aa9223ae8ab832eff23a1da1755278e86d0b
ms.contentlocale: es-es
ms.lasthandoff: 06/23/2017

---
# <a name="temporal-table-considerations-and-limitations"></a>Limitaciones y consideraciones de las tablas temporales
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Hay algunas consideraciones y limitaciones que deben tenerse en cuenta al trabajar con tablas temporales debido a la naturaleza de las versiones del sistema.  
  
 Tenga en cuenta lo siguiente al trabajar con tablas temporales.  
  
-   Una tabla temporal debe tener una clave principal definida para correlacionar los registros entre la tabla actual y la de historial; esta última no puede tener definida una clave principal.  
  
-   Las columnas de periodo SYSTEM_TIME que se usan para registrar los valores **SysStartTime** y **SysEndTime** deben definirse con una propiedad datatype de datetime2.  
  
-   Si el nombre de una tabla de historial se especifica durante su creación, debe determinar el nombre del esquema y la tabla.  
  
-   De forma predeterminada, es la tabla de historial es **PAGE** comprimida.  
  
-   Si la tabla actual tiene particiones, la tabla de historial se crea en el grupo de archivos predeterminado, ya que la configuración de particiones no se replica automáticamente desde la tabla actual a la de historial.  
  
-   Las tablas temporales y de historial no pueden ser **FILETABLE** y pueden contener columnas de cualquier tipo de datos compatible que no sea **FILESTREAM** , ya que **FILETABLE** y **FILESTREAM** permiten que se puedan manipular datos fuera de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ; por tanto, no se puede garantizar el control de versiones del sistema.  
  
-   Aunque las tablas temporales son compatibles con los tipos de datos BLOB, como **(n)varchar(max)**, **varbinary(max)**, **(n)text** e **image**, acarrearán importantes costos de almacenamiento y afectarán al rendimiento debido a su tamaño. Por lo tanto, al diseñar el sistema, debe tener cuidado al usar estos tipos de datos.  
  
-   La tabla de historial debe crearse en la misma base de datos que donde reside la actual. No se admiten las consultas temporales en **Linked Server** .  
  
-   La tabla de historial no puede tener restricciones (de clave principal, clave externa, tabla o columna).  
  
-   No se admiten vistas indexadas con consultas temporales (las consultas que usan la cláusula **FOR SYSTEM_TIME** ).  
  
-   La opción en línea (**WITH (ONLINE = ON**) no tiene ningún efecto sobre **ALTER TABLE ALTER COLUMN** en las tablas temporales con versiones del sistema. La columna ALTER no se realiza como en línea, independientemente del valor que se especificó para la opción ONLINE.  
  
-   Las instrucciones**INSERT** y **UPDATE** no pueden hacer referencia a las columnas de periodo SYSTEM_TIME. Se bloquearán los intentos de insertar valores directamente en estas columnas.  
  
-   **TRUNCATE TABLE** is not supported while **SYSTEM_VERSIONING** is **ON**  
  
-   No se permite la modificación directa de los datos en una tabla de historial.  
  
-   **ON DELETE CASCADE** y **ON UPDATE CASCADE** no se permiten en la tabla actual. Es decir, cuando la tabla temporal hace referencia a la tabla de la relación de clave externa (correspondiente a *parent_object_id* en sys.foreign_keys), no se permiten las opciones CASCADE. Para abordar esta limitación, use la lógica de aplicación o los desencadenadores AFTER para mantener la coherencia de eliminación en la tabla de clave principal (correspondiente a  *referenced_object_id* en sys.foreign_keys). Si la tabla de clave principal es temporal y de referencia no lo es, significa que no hay ninguna limitación de este tipo. 

    **Nota:** esta limitación sólo se aplica a SQL Server 2016. Se admiten opciones CASCADE en [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] y a partir de la versión 2.0 de CTP de SQL Server 2017.  
  
-   Los desencadenadores**INSTEAD OF** no se permiten en la tabla actual o de historial para evitar que se invalide la lógica DML. Los desencadenadores**AFTER** solo se permiten en la tabla actual. Se bloquean en la tabla de historial para evitar que se invalide la lógica DML.  
  
-   El uso de tecnologías de replicación está limitado.  
  
    -   **Always On** : totalmente compatible.  
  
    -   **Captura de datos y seguimiento de datos modificados** : solo es compatible con la tabla actual.  
  
    -   **Replicación transaccional y de instantáneas**: solo es compatible con un publicador único sin la función de temporalidad habilitada, y con un suscriptor que tenga dicha función habilitada. En este caso, el publicador se usa para una carga de trabajo OLTP, mientras que el suscriptor se emplea para la descarga de informes (incluidas las consultas "AS OF").    
        No se admite el uso de varios suscriptores, puesto que este escenario puede provocar que los datos temporales sean incoherentes (cada uno de ellos dependería del reloj del sistema local).  
  
    -   **Replicación de mezcla:** no es compatible con las tablas temporales.  
  
-   Las consultas normales solo afectan a los datos de la tabla actual. Para consultar los datos en la tabla de historial, debe usar consultas temporales. Este asunto se explica más adelante en este documento, en la sección titulada "Consulta de datos temporales".  
  
-   Una estrategia de indexación óptima consiste en incluir un índice de almacén de columnas agrupado o un índice de almacén de filas de árbol B en la tabla actual, así como un índice de almacén de columnas agrupado en la tabla de historial para que el rendimiento y el tamaño de almacenamiento sean óptimos. Si crea o usa su propia tabla de historial, recomendamos encarecidamente que genere este tipo de índice que consta de columnas de periodo empezando por el fin de la columna de periodo con el fin de acelerar las consultas temporales y las que forman parte de la comprobación de coherencia de datos. La tabla de historial predeterminada cuenta con un índice de almacén de filas agrupado que se ha creado en función de las columnas de periodo (fin e inicio). Como mínimo, se recomienda un índice de almacén de filas no agrupado.  
  
-   Los siguientes objetos o propiedades no se replican desde la tabla actual a la de historial cuando se crea la tabla de historial.  
  
    -   Definición de periodo  
  
    -   Definición de identidad  
  
    -   Índices  
  
    -   Estadísticas  
  
    -   Restricciones CHECK  
  
    -   Desencadenadores  
  
    -   Configuración de partición  
  
    -   Permisos  
  
    -   Predicados de seguridad de nivel de fila  
  
-   Una tabla de historial no puede configurarse como actual en una cadena de tablas de historial.  
  
## <a name="did-this-article-help-you-were-listening"></a>¿Le ayudó este artículo? Le escuchamos  
 ¿Qué información está buscando? ¿La encontró? Escuchamos sus comentarios para mejorar el contenido. Envíe sus comentarios a [sqlfeedback@microsoft.com](mailto:sqlfeedback@microsoft.com?subject=Your%20feedback%20about%20the%20Temporal%20Table%20Considerations%20and%20Limitations%20page)  
  
## <a name="see-also"></a>Vea también  
 [Tablas temporales](../../relational-databases/tables/temporal-tables.md)   
 [Introducción a las tablas temporales con versión del sistema](../../relational-databases/tables/getting-started-with-system-versioned-temporal-tables.md)   
 [Comprobaciones de coherencia del sistema de la tabla temporal](../../relational-databases/tables/temporal-table-system-consistency-checks.md)   
 [Creación de particiones con tablas temporales](../../relational-databases/tables/partitioning-with-temporal-tables.md)   
 [Seguridad de la tabla temporal](../../relational-databases/tables/temporal-table-security.md)   
 [Administración de la retención de datos históricos en las tablas temporales con versiones del sistema](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)   
 [Tablas temporales con control de versiones del sistema con tablas con optimización para memoria](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)   
 [Funciones y vistas de metadatos de la tabla temporal](../../relational-databases/tables/temporal-table-metadata-views-and-functions.md)  
  
  

