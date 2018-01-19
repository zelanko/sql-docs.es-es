---
title: Convenciones de sintaxis de Transact-SQL (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: sql13.TSQLExpandPortal.f1
dev_langs: TSQL
helpviewer_keywords:
- conventions [SQL Server]
- Applies to section in Transact-SQL topics
- code example conventions [SQL Server]
- objects [SQL Server], names
- code [SQL Server], conventions
- multipart names [SQL Server]
- Transact-SQL syntax conventions
- syntax conventions [SQL Server]
- code [SQL Server]
- Transact-SQL
- naming conventions [SQL Server]
- syntax [SQL Server], Transact-SQL
ms.assetid: 35fbcf7f-8b55-46cd-a957-9b8c7b311241
caps.latest.revision: "55"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: f7cb61a12af903aa444462a7a67c9c71231b96fa
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/19/2018
---
# <a name="transact-sql-syntax-conventions-transact-sql"></a>Convenciones de sintaxis de Transact-SQL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  En la siguiente tabla se incluyen y describen las convenciones utilizadas en los diagramas de sintaxis de la referencia de [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
|Convención|Se usa para|  
|----------------|--------------|  
|MAYÚSCULAS|Palabras clave de [!INCLUDE[tsql](../../includes/tsql-md.md)].|  
|*cursiva*|Parámetros proporcionados por el usuario para la sintaxis de [!INCLUDE[tsql](../../includes/tsql-md.md)].|  
|**Negrita**|Nombres de bases de datos, tablas, columnas e índices, procedimientos almacenados, utilidades, nombres de tipos de datos y texto que debe escribirse exactamente como se muestra.|  
|**underline**|Indica el valor predeterminado que se aplica cuando la cláusula que contiene el valor subrayado se omite en la instrucción.|  
|&#124; (barra vertical)|Separa los elementos de sintaxis escritos entre corchetes o llaves. Solo puede utilizar uno de los elementos.|  
|`[ ]` (corchetes)|Elementos opcionales de sintaxis. No escriba los corchetes.|  
|{} (llaves)|Elementos obligatorios de sintaxis. No escriba las llaves.|  
|[**,**...*n*]|Indica que el elemento anterior puede repetirse  *n*  número de veces. Cada repetición se separa de la siguiente con una coma.|  
|[...*n*]|Indica que el elemento anterior puede repetirse  *n*  número de veces. Cada repetición se separa del siguiente con un espacio en blanco.|  
|;|Terminador de instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)]. Aunque el punto y coma no se requiere en la mayoría de las instrucciones de esta versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se requerirá en una versión futura.|  
|\<etiqueta >:: =|Nombre de un bloque de sintaxis. Esta convención sirve para agrupar y etiquetar secciones de sintaxis extensas o una unidad de sintaxis que se puede usar en varias ubicaciones dentro de una instrucción. Cada ubicación en la que se puede utilizar el bloque de sintaxis se indica con la etiqueta incluida entre comillas angulares: \<etiqueta >.<br /><br /> Un conjunto es una colección de expresiones, por ejemplo \<conjunto de agrupaciones >; y una lista es una colección de conjuntos, por ejemplo \<lista de elementos compuestos >.|  
  
## <a name="multipart-names"></a>Nombres de varias partes  
 A menos que se especifique lo contrario, todas las referencias de [!INCLUDE[tsql](../../includes/tsql-md.md)] al nombre de un objeto de base de datos pueden ser un nombre de cuatro partes con el formato siguiente:  
  
 *server_name* **.**[*database_name*]**.**[*schema_name*]**.***object_name*  
  
 | *database_name***.**[*schema_name*]**.***object_name*  
  
 | *schema_name***.***object_name*  
  
 *| object_name*  
  
 *server_name*  
 Especifica un nombre de servidor vinculado o un nombre de servidor remoto.  
  
 *database_name*  
 Especifica el nombre de una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] si el objeto reside en una instancia local de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Cuando el objeto está en un servidor vinculado, *database_name* especifica un catálogo de OLE DB.  
  
 *schema_name*  
 Especifica el nombre del esquema que contiene el objeto si dicho objeto se encuentra en una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Cuando el objeto está en un servidor vinculado, *schema_name* especifica un nombre de esquema de OLE DB.  
  
 *object_name*  
 Hace referencia al nombre del objeto.  
  
 Cuando se hace referencia a un objeto específico, no siempre hay que especificar el servidor, la base de datos y el esquema del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] para identificar el objeto. Sin embargo, si no se encuentra el objeto, se devuelve un error.  
  
> [!NOTE]  
>  Para evitar los errores de resolución de nombres, se recomienda especificar el nombre de esquema siempre que se especifique un objeto del ámbito del esquema.  
  
 Para omitir los nodos intermedios, utilice puntos para indicar estas posiciones. En la siguiente tabla se muestran los formatos válidos para los nombres de objetos.  
  
|Formato de referencia a objetos|Description|  
|-----------------------------|-----------------|  
|*servidor* **.** *database* **.** *schema* **.** *objeto*|Nombre de cuatro partes.|  
|*servidor* **.** *database* **..** *objeto*|Se omite el nombre del esquema.|  
|*server* **..** *schema* **.** *objeto*|Se omite el nombre de la base de datos.|  
|*server* **...** *object*|Se omiten los nombres de la base de datos y el esquema.|  
|*database* **.** *schema* **.** *objeto*|Se omite el nombre del servidor.|  
|*database* **..** *objeto*|Se omiten los nombres del servidor y el esquema.|  
|*schema* **.** *objeto*|Se omiten los nombres del servidor y la base de datos.|  
|*objeto*|Se omiten los nombres del servidor, la base de datos y el esquema.|  
  
## <a name="code-example-conventions"></a>Convenciones de los ejemplos de código  
 A menos que se indique lo contrario, los ejemplos proporcionados en la referencia de [!INCLUDE[tsql](../../includes/tsql-md.md)] se han probado con [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] y los valores predeterminados para las siguientes opciones:  
  
-   ANSI_NULLS  
  
-   ANSI_NULL_DFLT_ON  
  
-   ANSI_PADDING  
  
-   ANSI_WARNINGS  
  
-   CONCAT_NULL_YIELDS_NULL  
  
-   QUOTED_IDENTIFIER  
  
 La mayoría de los ejemplos de código de la referencia de [!INCLUDE[tsql](../../includes/tsql-md.md)] se han comprobado en servidores que se ejecutan en un orden que distingue entre mayúsculas y minúsculas. Normalmente, los servidores de prueba ejecutaban la página de códigos ANSI/ISO 1252.  
  
 Constantes de cadena de caracteres Unicode con la letra de prefijo de muchos ejemplos de código **N**. Sin el **N** prefijo, la cadena se convierte en la página de códigos predeterminada de la base de datos. Esta página de códigos predeterminada puede no reconocer determinados caracteres.  
  
## <a name="applies-to-references"></a>Referencias de "Se aplica a"  
 El [!INCLUDE[tsql](../../includes/tsql-md.md)] referencia incluye artículos relacionados con [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], y [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]. En la parte superior de cada artículo es una sección que indica qué productos son compatibles con el asunto del artículo. Si se omite un producto, la característica descrita en este artículo no está disponible en ese producto. Por ejemplo, los grupos de disponibilidad se introdujeron en [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]. El **CREATE AVAILABILITY GROUP** artículo indica que se aplica a **SQL Server (SQL Server 2012 a través de la versión actual)** porque no se aplica a [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], o [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 En algunos casos, el asunto general del artículo puede usarse en un producto, pero no se admiten todos los argumentos. Por ejemplo, los usuarios de bases de datos independientes se introdujeron en [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]. El **CREATE USER** instrucción se puede usar en cualquier [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] producto, sin embargo, el **WITH PASSWORD** sintaxis no se puede usar con versiones anteriores. En este caso, adicional **se aplica a** secciones se insertan en las descripciones del argumento correspondiente en el cuerpo del artículo.  
  
## <a name="see-also"></a>Vea también  
 [Referencia de Transact-SQL &#40;motor de base de datos&#41;](../../t-sql/transact-sql-reference-database-engine.md)  
  
  


