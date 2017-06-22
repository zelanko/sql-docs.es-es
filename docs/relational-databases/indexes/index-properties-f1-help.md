---
title: "Propiedades del índice (Ayuda F1) | Microsoft Docs"
ms.custom: 
ms.date: 02/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-indexes
ms.tgt_pltfrm: 
ms.topic: reference
f1_keywords:
- sql13.swb.indexproperties.filter.f1
- sql13.swb.indexproperties.partitions.f1
- sql13.swb.indexproperties.general.f1
- sql13.swb.indexproperties.storage.f1
- sql13.swb.indexproperties.columns.f1
- sql13.swb.indexproperties.options.f1
- sql13.swb.indexproperties.spatial.f1
ms.assetid: 45efd81a-3796-4b04-b0cc-f3deec94c733
caps.latest.revision: 38
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 0d646d06bd41ce4db35011d65ecab45109326c15
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="index-properties-f1-help"></a>Propiedades del índice (Ayuda F1)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Las secciones de este tema hacen referencia a las distintas propiedades de índice disponibles mediante cuadros de diálogo de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] .  
  
 **En este tema:**  
  
 [Propiedades del índice (página General)](#General)  
  
 [Cuadro de diálogo Seleccionar columnas de (índice)](#Columns)  
  
 [Propiedades del índice (página Almacenamiento)](#Storage)  
  
 [Propiedades del índice (página Espacial)](#Spatial)  
  
 [Propiedades del índice (página Filtro)](#Filter)  
  
##  <a name="General"></a> Propiedades del índice (página General)  
 Use la página General para ver o modificar las propiedades del índice para la tabla o vista seleccionada. Las opciones para cada página pueden cambiar según el tipo de índice seleccionado.  
  
 **Nombre de la tabla**  
 Muestra el nombre de la tabla o vista en la que se ha creado el índice. Este campo es de solo lectura. Para seleccionar una tabla diferente, cierre la página Propiedades del índice, seleccione la tabla correcta y vuelva a abrir la página Propiedades del índice.  
  
 Los índices espaciales no se pueden especificar en vistas indizadas. Los índices espaciales solo se pueden definir para una tabla que tenga una clave principal. El número máximo de columnas de clave principal en la tabla es de 15. El tamaño por fila combinado de las columnas de clave principal está limitado a un valor máximo de 895 bytes.  
  
 **Nombre del índice**  
 Muestra el nombre del índice. Este campo es de solo lectura para un índice existente. Si está creando un nuevo índice, escriba el nombre del índice.  
  
 **Tipo de índice**  
 Indica el tipo de índice. Para los índices nuevos, indica el tipo de índice seleccionado al abrir el cuadro de diálogo. Los índices pueden ser: **Clúster**, **No agrupado**, **XML principal**, **XML secundario**, **Espacial**o **Almacén de columnas en clúster**o **Almacén de columnas no clúster**.  
  
 **Nota** : solo se permite un índice clúster por tabla. Solo se permite un índice de almacén de columnas optimizado de memoria one xVelocity por tabla.  
  
 **Único**  
 Si selecciona esta casilla, el índice será único. No está permitido que dos filas tengan el mismo valor de índice. De forma predeterminada, esta casilla no está activada. Cuando se modifica un índice existente, la creación de índice generará un error si dos filas tienen el mismo valor. En las columnas donde se permite NULL, un índice único admite un valor NULL.  
  
 Si selecciona **Espacial** en el campo **Tipo de índice** , la casilla **Único** aparece atenuada.  
  
 **Columnas de clave de índice**  
 Agregue las columnas deseadas a la cuadrícula **Columnas de clave de índice** . Cuando se agrega más de una columna, las columnas deben aparecer en una lista con el orden deseado. El orden de las columnas en un índice puede tener un gran impacto en el rendimiento del índice.  
  
 No pueden participar más de 16 columnas en un solo índice compuesto. Para más de 16 columnas, vea Columnas incluidas al final de este tema.  
  
 Un índice espacial solo se puede definir en una única columna que contenga un tipo de datos espaciales (una *columna espacial*).  
  
 **Nombre**  
 Muestra el nombre de la columna que participa en la clave de índice.  
  
 **Criterio de ordenación**  
 Especifica la ordenación de la columna de índice seleccionada, es decir, **Ascendente** o **Descendente**.  
  
> [!NOTE]  
>  Si el tipo de índice es **XML principal** o **Espacial**, esta columna no aparece en la tabla.  
  
 **Tipo de datos**  
 Muestra la información sobre el tipo de datos.  
  
> [!NOTE]  
>  Si la columna de tabla es una columna calculada, **Tipo de datos** mostrará "columna calculada".  
  
 **Tamaño**  
 Muestra el número máximo de bytes necesarios para almacenar el tipo de datos de la columna. Muestra cero (0) para las columnas espaciales o XML.  
  
 **Identidad**  
 Muestra si la columna que participa en la clave de índice es una columna de identidad.  
  
 **Permitir valores NULL**  
 Muestra si la columna que participa en la clave de índice permite almacenar valores NULL en la columna de vista o tabla.  
  
 **Agregar**  
 Agrega una columna a la clave de índice. Seleccione columnas de tabla del cuadro de diálogo **Seleccionar columnas de** *\<nombre de tabla>* que aparece al hacer clic en **Agregar**. Para un índice espacial, después de seleccionar una columna, este botón aparece atenuado.  
  
 **Quitar**  
 Quita la columna seleccionada de la clave de índice.  
  
 **Subir**  
 Sube la columna seleccionada en la cuadrícula de la clave de índice.  
  
 **Bajar**  
 Baja la columna seleccionada en la cuadrícula de la clave de índice.  
  
 **Columnas de almacén de columnas**  
 Haga clic en **Agregar** para seleccionar columnas para el índice de almacén de columnas. Para conocer las limitaciones de un índice de almacén de columnas, vea [CREATE COLUMNSTORE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-columnstore-index-transact-sql.md).  
  
 **Columnas incluidas**  
 Incluye columnas sin clave en el índice no clúster. Esta opción le permite superar los límites actuales del índice relativos al tamaño total de una clave de índice y el número máximo de columnas que participan en una clave de índice agregando columnas como columnas sin clave en el nivel hoja del índice no clúster. Para obtener más información, vea [Crear índices con columnas incluidas](../../relational-databases/indexes/create-indexes-with-included-columns.md).  
  
##  <a name="Columns"></a> Cuadro de diálogo Seleccionar columnas de (índice)  
 Use esta página para agregar columnas a la página General de **Propiedades del índice** cuando cree o modifique un índice.  
  
 **casilla**  
 Seleccione esta opción para agregar columnas.  
  
 **Nombre**  
 Nombre de la columna.  
  
 **Tipo de datos**  
 Tipo de datos de la columna.  
  
 **Bytes**  
 Tamaño de la columna, en bytes.  
  
 **Identidad**  
 Muestra **Sí** para columnas de identidad y **No** cuando la columna no es una columna de identidad.  
  
 **Allow Nulls**  
 Muestra **Sí** cuando la definición de la tabla permite valores NULL para la columna. Muestra **No** cuando la definición de la tabla no permite valores NULL para la columna.  
  
##  <a name="Storage"></a> Opciones de la página Almacenamiento  
 Utilice esta página para ver o modificar las propiedades del grupo de archivos o del esquema de partición para el índice seleccionado. Solo muestra las opciones relacionadas con el tipo de índice.  
  
 **Grupo de archivos**  
 Almacena el índice en el grupo de archivos especificado. En la lista solo se muestran los grupos de archivos (fila) estándar. La selección de lista predeterminada es el grupo de archivos PRIMARY de la base de datos. Para más información, consulte [Database Files and Filegroups](../../relational-databases/databases/database-files-and-filegroups.md).  
  
 **Grupo de archivos de flujo de archivos**  
 Especifica el grupo de archivos para los datos FILESTREAM. En esta lista solo se muestran los grupos de archivos FILESTREAM. La selección de lista predeterminada es el grupo de archivos PRIMARY FILESTREAM. Para obtener más información, vea [FILESTREAM &#40;SQL Server&#41;](../../relational-databases/blob/filestream-sql-server.md).  
  
 **Esquema de partición**  
 Almacena el índice en un esquema de partición. Al hacer clic en **Esquema de partición** , se habilita la cuadrícula que se muestra a continuación. La selección de lista predeterminada es el esquema de partición utilizado para almacenar los datos de la tabla. Si se selecciona un esquema de partición distinto de la lista, se actualizará la información en la cuadrícula. Para obtener más información, consulte [Partitioned Tables and Indexes](../../relational-databases/partitions/partitioned-tables-and-indexes.md).  
  
 La opción de esquema de partición no estará disponible si no hay ningún esquema de partición en la base de datos.  
  
 **Esquema de partición Filestream**  
 Especifica el esquema de partición de los datos FILESTREAM. El esquema de partición debe ser simétrico al esquema especificado en la opción **Esquema de partición** .  
  
 Si no tiene particiones, el campo está en blanco.  
  
 **Parámetro del esquema de partición**  
 Muestra el nombre de la columna que participa en el esquema de partición.  
  
 **Columna de la tabla**  
 Seleccione la tabla o vista que se asignará al esquema de partición.  
  
 **Tipo de datos de la columna**  
 Muestra información de tipo de datos de la columna.  
  
> [!NOTE]  
>  Si la columna de tabla es una columna calculada, **Tipo de datos de la columna** mostrará "columna calculada".  
  
 **Permitir procesamiento en línea de instrucciones DML al mover el índice**  
 Permite a los usuarios obtener acceso a los datos de la tabla subyacente o del índice clúster, así como a todos los índices no clúster asociados durante las operaciones de índice. Para más información, consulte [Perform Index Operations Online](../../relational-databases/indexes/perform-index-operations-online.md).  
  
> [!NOTE]  
>  Esta opción no estará disponible para los índices XML ni cuando el índice sea un índice clúster deshabilitado.  
  
 **Establecer grado máximo de paralelismo**  
 Limita el número de procesadores que se van a utilizar durante la ejecución de planes paralelos. El valor predeterminado es 0, que utiliza el número real de CPU disponibles. Si el valor se establece en 1, se suprime la generación de planes paralelos; si el valor se establece en un número mayor que 1, se restringe el número máximo de procesadores que se utilizan en la ejecución de una única consulta. Esta opción solo está disponible si el cuadro de diálogo está en los estados **Volver a generar** o **Volver a crear** . Para más información, consulte [PerformanceEstablecer la opción Grado máximo de paralelismo para lograr un rendimiento óptimo](../../relational-databases/policy-based-management/set-the-max-degree-of-parallelism-option-for-optimal-performance.md).  
  
> [!NOTE]  
>  Si especifica un valor superior al número de CPU disponibles, se utilizará el número real de CPU disponibles.  
  
##  <a name="Spatial"></a> Opciones de índice de la página Espacial  
 Use la página **Espacial** para ver o especificar los valores de las propiedades espaciales. Para obtener más información, vea [Datos espaciales &#40;SQL Server&#41;](../../relational-databases/spatial/spatial-data-sql-server.md).  
  
### <a name="bounding-box"></a>Cuadro de límite  
 El *cuadro de límite* es el perímetro de la cuadrícula de nivel superior de un plano geométrico. Los parámetros de cuadro de límite solo existen en la teselación de cuadrícula de geometría. Estos parámetros no están disponibles si **Esquema de teselación** es **Cuadrícula de geografía**.  
  
 El panel muestra las coordenadas **(***X-min***,***Y-min***)** y **(***X-max***,***Y-max***)** del cuadro de límite. No hay valores predeterminados para las coordenadas. Por consiguiente, cuando cree un nuevo índice espacial en una columna de tipo **geometry** , deberá especificar los valores de las coordenadas.  
  
 **X-min**  
 La coordenada x de la esquina inferior izquierda del cuadro de límite.  
  
 **Y-min**  
 La coordenada y de la esquina inferior izquierda del cuadro de límite.  
  
 **X-max**  
 La coordenada x de la esquina superior derecha del cuadro de límite.  
  
 **Y-max**  
 La coordenada y de la esquina superior derecha del cuadro de límite.  
  
### <a name="general"></a>General  
 **Esquema de teselación**  
 Indica el esquema de teselación del índice. Los esquemas de teselación admitidos son los siguientes.  
  
 **Cuadrícula de geometría**  
 Especifica el esquema de teselación de cuadrícula de geometría que se aplica a una columna del tipo de datos **geometry** .  
  
 **Cuadrícula automática de geometría**  
 Esta opción está habilitada para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cuando el nivel de compatibilidad de base de datos se ha establecido en 110 o superior.  
  
 **Cuadrícula de geografía**  
 Especifica el esquema de teselación de cuadrícula de geografía, que se aplica a una columna del tipo de datos **geography** .  
  
 **Cuadrícula automática de geografía**  
 Esta opción está habilitada para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cuando el nivel de compatibilidad de base de datos se ha establecido en 110 o superior.  
  
 Para obtener información sobre el modo en que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] implementa la teselación, vea [Datos espaciales &#40;SQL Server&#41;](../../relational-databases/spatial/spatial-data-sql-server.md).  
  
 **Celdas por objeto**  
 Indica el número de celdas por objeto de teselación que se pueden usar para un único objeto espacial en el índice. Este número puede ser un entero comprendido entre 1 y 8192, ambos incluidos. El valor predeterminado es 16, y 8 para versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cuando el nivel de compatibilidad de base de datos se ha establecido en 110 o superior.  
  
 En el nivel superior, si un objeto abarca más celdas de las especificadas mediante *n*, la indexación usa tantas celdas como sean necesarias para proporcionar una teselación de nivel superior completa. En tales casos, un objeto podría recibir más celdas de las especificadas. En este caso, el número máximo es la cantidad de celdas generadas por la cuadrícula de nivel superior, que depende de la densidad de **Nivel 1** .  
  
### <a name="grids"></a>Cuadrículas  
 Este panel muestra la densidad de la cuadrícula en cada nivel del esquema de la teselación. La densidad se especifica como **Baja**, **Media**o **Alta**. El valor predeterminado es **Media**. **Baja** representa una cuadrícula de 4 x 4 (16 celdas), **Media** representa una cuadrícula de 8 x 8 (64 celdas) y **Alta** representa una cuadrícula de 16 x 16 (256 celdas). Estas opciones no están disponibles cuando se eligen las opciones de teselación **Cuadrícula automática de geometría** o **Cuadrícula automática de geografía** .  
  
 **Nivel 1**  
 La densidad de la cuadrícula del primer nivel (superior).  
  
 **Nivel 2**  
 La densidad de la cuadrícula del segundo nivel.  
  
 **Nivel 3**  
 La densidad de la cuadrícula del tercer nivel.  
  
 **Nivel 4**  
 La densidad de la cuadrícula del cuarto nivel.  
  
##  <a name="Filter"></a> Página Filtro  
 Use esta página para especificar el predicado de filtro para un índice filtrado. Para obtener más información, consulte [Create Filtered Indexes](../../relational-databases/indexes/create-filtered-indexes.md).  
  
 **Expresión de filtro**  
 Define qué filas de datos para incluir en el índice filtrado. Por ejemplo, `StartDate > '20000101' AND EndDate IS NOT NULL'.`  
  
## <a name="see-also"></a>Vea también  
 [Establecer opciones de índice](../../relational-databases/indexes/set-index-options.md)   
 [INDEXPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/indexproperty-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)  
  
  

