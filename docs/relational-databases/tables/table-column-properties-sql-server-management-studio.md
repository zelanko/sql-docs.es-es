---
title: Propiedades de columnas de tablas (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 08/08/2016
ms.prod: sql
ms.prod_service: table-view-index, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
f1_keywords:
- vdtsql.chm:65558
- vdtsql.chm:69657
- vdt.ppg.columns
ms.assetid: 09830897-cc10-46b8-95f5-e0e9681b668c
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9e10bb43295df9fac711792f65ed22e4b55a1605
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47628923"
---
# <a name="table-column-properties-sql-server-management-studio"></a>Propiedades de columnas de tablas (SQL Server Management Studio)
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  Estas propiedades aparecen en el panel inferior del Diseñador de tablas. A menos que se especifique lo contrario, podrá modificar estas propiedades en la ventana Propiedades cuando la columna esté seleccionada. Las **Propiedades de columna** pueden mostrarse en categorías o en orden alfabético. Muchas propiedades solo aparecen o solo se pueden cambiar por ciertos tipos de datos.  
  
> [!NOTE]  
>  Si se publica la tabla para replicación, debe modificar el esquema mediante la instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) o SMO (Objetos de administración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ). Si se modifica el esquema mediante el Diseñador de tablas o el Diseñador de diagramas de base de datos, se intentará eliminar la tabla y volver a crearla. No se pueden eliminar objetos publicados, por lo que la modificación del esquema generará un error.  
  
 **General**  
 Se expande para mostrar **Nombre**, **Permitir valores NULL**, **Tipo de datos**, **Valor o enlace predeterminado**, **Longitud**, **Precisión**y **Escala**.  
  
 **Nombre**  
 Muestra el nombre de la columna seleccionada.  
  
 **Permitir valores NULL**  
 Indica si esta columna permite valores NULL. Para editar esta propiedad, haga clic en la casilla Permitir valores nulos correspondiente a la columna del panel superior del Diseñador de tablas.  
  
 **Tipo de datos**  
 Muestra el tipo de datos de la columna seleccionada. Para editar esta propiedad, haga clic en su valor, expanda la lista desplegable y elija otro valor.  
  
 **Valor o enlace predeterminado**  
 Muestra el valor predeterminado de esta columna cuando no se especifica ningún valor para la misma. El valor de este campo puede ser el de una restricción predeterminada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o el nombre de una restricción global con la que está enlazada la columna. La lista desplegable contiene todos los valores predeterminados globales definidos en la base de datos. Para enlazar la columna con un valor predeterminado global, realice una selección en la lista desplegable. Otra opción para crear una restricción predeterminada para la columna es escribir directamente el valor predeterminado como texto.  
  
 **Longitud**  
 Muestra el número de caracteres permitidos para los tipos de datos basados en caracteres. Esta propiedad solo está disponible para tipos de datos basados en caracteres.  
  
 **Escala**  
 Muestra el número máximo de dígitos que pueden aparecer a la derecha del separador decimal para los valores de esta columna. Esta propiedad muestra **0** para tipos de datos no numéricos.  
  
 **Precisión**  
 Muestra el número máximo de dígitos para los valores de esta columna. Esta propiedad muestra **0** para tipos de datos no numéricos.  
  
 **Diseñador de tablas**  
 Expande la sección **Diseñador de tablas** .  
  
 **Intercalación**  
 Muestra la secuencia de intercalación que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aplica de forma predeterminada a la columna cuando se utilizan los valores de la misma para ordenar las filas de los resultados de una consulta. Para editar la intercalación, seleccione la propiedad y haga clic en los puntos suspensivos (...) que aparecen a la derecha del valor de propiedad para que aparezca el cuadro de diálogo **Intercalación** .  
  
 **Especificación de columna calculada**  
 Muestra información sobre una columna calculada. El valor que se muestra para la propiedad es el mismo que el de la propiedad secundaria **Fórmula** y muestra la fórmula de la columna calculada.  
  
> [!NOTE]  
>  Para cambiar el valor que se muestra para la propiedad **Especificación de columna calculada** , debe expandirla y editar la propiedad secundaria **Fórmula** .  
  
-   **Fórmula** Muestra la fórmula de la columna calculada. Para editar esta propiedad, escriba una nueva fórmula directamente.  
  
-   **Persistente** Indica si se almacenan los resultados de la fórmula. Si se selecciona el valor **No** para esta propiedad, solo se almacenará la fórmula y se calcularán los valores cada vez que se haga referencia a esta columna. Para editar esta propiedad, haga clic en su valor, expanda la lista desplegable y elija otro valor.  
  
 Para más información, consulte [Specify Computed Columns in a Table](../../relational-databases/tables/specify-computed-columns-in-a-table.md).  
  
 **Tipo de datos comprimido**  
 Muestra información sobre el tipo de datos del campo con el mismo formato que la instrucción SQL CREATE TABLE. Por ejemplo, un campo que contenga una cadena de longitud variable con una longitud máxima de 20 caracteres se representará como "varchar(20)". Para cambiar esta propiedad, escriba el valor directamente.  
  
 **Descripción**  
 Muestra la descripción de esta columna. Para editar la descripción, seleccione la propiedad, haga clic en los puntos suspensivos (...) que aparecen a la derecha del valor de propiedad y edite la descripción en el cuadro de diálogo **Propiedad Description** .  
  
 **Determinista**  
 Muestra si se puede determinar con exactitud el tipo de dato de la columna seleccionada.  
  
 **Publicado por DTS**  
 Muestra si la columna está publicada con DTS. ([Los Servicios de transformación de datos están en desuso](https://msdn.microsoft.com/library/cc707786(v=sql.130).aspx#Anchor_0)). 
  
 **Especificación de texto completo**  
 Muestra información sobre un índice de texto completo. El valor de esta propiedad es el de la propiedad secundaria **Está indexado por texto completo** e indica si esta columna tiene un índice de texto completo.  
  
> [!NOTE]  
>  Para cambiar el valor que se muestra para la propiedad **Especificación de texto completo** , debe expandirla y editar la propiedad secundaria **Está indexado por texto completo** .  
  
-   **Está indexado por texto completo** Indica si esta columna tiene un índice de texto completo. Esta propiedad solo puede establecerse en **Sí** si el tipo de datos de la columna se puede buscar por texto completo y si la tabla a la que pertenece esta columna tiene especificado un índice de texto completo. Para editar esta propiedad, haga clic en su valor, expanda la lista desplegable y elija otro valor.  
  
-   **Columna de tipo de texto completo** Muestra el nombre de la columna en la que esta columna tiene un índice de texto. Esta propiedad se debe establecer si la propiedad **Tipo de datos** de esta columna es **image** o **varbinary**. La columna citada en esta propiedad debe ser del tipo **[n]char, [n]varchar,** o **xml**, y la lista desplegable de esta propiedad solo contiene columnas que tienen uno de estos tres tipos de datos. Las filas de la columna citada por esta propiedad indican el tipo de documento de las filas correspondientes de la columna en la que se pueden realizar búsquedas de texto completo. Para editar esta propiedad, haga clic en su valor, expanda la lista desplegable y elija otro valor.  
  
-   **Idioma** Indica el idioma del separador de palabras utilizado para indizar la columna. El valor almacenado en la propiedad es en realidad el identificador de configuración regional del separador de palabras. Para obtener más información sobre los separadores de palabras y los LCID, vea Separadores de palabras y lematizadores. Para editar esta propiedad, haga clic en su valor, expanda la lista desplegable y elija otro valor.  
  
 **Semántica estadística**  
 Seleccione si desea habilitar la indización semántica estadística para la columna seleccionada. Para obtener más información, vea [Búsqueda semántica &#40;SQL Server&#41;](../../relational-databases/search/semantic-search-sql-server.md).  
  
 Si selecciona **Idioma** antes de seleccionar **Semántica estadística**y el idioma seleccionado no tiene un modelo de idioma semántico asociado, la opción **Semántica estadística** se establece en **No** y no puede modificarse. Si selecciona **Sí** para la opción de **Semántica estadística** antes de seleccionar **Idioma**, los idiomas disponibles en la columna **Idioma** estarán limitados a aquellos para los que exista un modelo de idioma semántico.  
  
 **Suscriptor que no es de SQL Server**  
 Indica si la columna se está replicando en un suscriptor que no es de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **Especificación de identidad**  
 Muestra información sobre si esta columna exige la unicidad de sus valores y cómo lo hace. El valor de esta propiedad indica si esta columna es o no una columna de identidad y si es o no igual al valor de la propiedad secundaria **Identidad**.  
  
> [!NOTE]  
>  Para cambiar el valor que se muestra para la propiedad **Especificación de identidad** , debe expandirla y editar la propiedad secundaria **Identidad** .  
  
-   **Identidad** Indica si esta columna es o no una columna de identidad. Para editar esta propiedad, haga clic en su valor, expanda la lista desplegable y elija otro valor.  
  
-   **Inicialización de identidad** Muestra el valor de inicialización especificado durante la creación de esta columna de identidad. Este valor se asignará a la primera fila de la tabla. Si deja esta celda en blanco, se le asignará el valor 1 de forma predeterminada. Para editar esta propiedad, escriba el nuevo valor directamente.  
  
-   **Incremento de identidad** Muestra el valor de incremento especificado durante la creación de esta columna de identidad. Este valor es el incremento que se agregará a **Inicialización de identidad** en cada fila siguiente. Si deja esta celda en blanco, se le asignará el valor 1 de forma predeterminada. Para editar esta propiedad, escriba el nuevo valor directamente.  
  
 **Indizable**  
 Muestra si la columna seleccionada se puede indizar. Por ejemplo, no se pueden indizar las columnas calculadas no deterministas.  
  
 **Publicado por combinación**  
 Muestra si la columna está publicada por combinación.  
  
 **No disponible para replicación**  
 Indica si los valores de identidad originales se conservan durante la replicación. Para obtener más información sobre la replicación, vea CREATE TABLE. Para editar esta propiedad, haga clic en su valor, expanda la lista desplegable y elija otro valor.  
  
 **Replicada**  
 Muestra si esta columna se replica en otra ubicación.  
  
 **RowGuid**  
 Indica si SQL Server utiliza la columna como ROWGUID. Solo se puede seleccionar el valor **Sí** para una columna de identidad única. Para editar esta propiedad, haga clic en su valor, expanda la lista desplegable y elija otro valor.  
  
 **Tamaño**  
 Muestra el tamaño en bytes permitido por el tipo de datos de la columna. Por ejemplo, un tipo de datos nchar puede tener una longitud de 10 (número de caracteres) pero tendría un tamaño de 20 para los juegos de caracteres Unicode.  
  
> [!NOTE]  
>  La longitud de un tipo de datos **(max)** varía en cada fila. **sp_help** devuelve (- 1) como longitud de columnas **(max)** . [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] muestra -1 como tamaño de columna.  
  
  
