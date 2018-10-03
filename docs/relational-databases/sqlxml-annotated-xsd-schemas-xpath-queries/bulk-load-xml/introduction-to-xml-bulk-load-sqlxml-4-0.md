---
title: Introducción a la carga masiva XML (SQLXML 4.0) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- nontransacted XML Bulk Load operations
- XML Bulk Load [SQLXML], about XML Bulk Load
- bulk load [SQLXML], about bulk load
- transacted XML Bulk Load operations
- streaming XML data
ms.assetid: 38bd3cbd-65ef-4c23-9ef3-e70ecf6bb88a
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a5ab69b03d15eaed8fffcbf88f78804160d11595
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47617823"
---
# <a name="introduction-to-xml-bulk-load-sqlxml-40"></a>Introducción a la carga masiva XML (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Carga masiva XML es un objeto COM independiente que permite cargar datos XML semiestructurados en Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tablas.  
  
 Puede insertar datos XML en una base de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] mediante una instrucción INSERT y la función OPENXML; sin embargo, la utilidad Carga masiva proporciona mejor rendimiento cuando es necesario insertar grandes cantidades de datos XML.  
  
 El método Execute del modelo de objetos carga masiva XML toma dos parámetros:  
  
-   Una definición de esquema XML anotado (XSD) o un esquema reducido de datos XML (XDR). La utilidad Carga masiva XML interpreta este esquema de asignación y las anotaciones que se especifican en el esquema para identificar las tablas de SQL Server donde se insertarán los datos XML.  
  
-   Un documento o fragmento de documento XML (un fragmento de documento es un documento sin un elemento de nivel superior único). Se puede especificar un nombre de archivo o un flujo del que Carga masiva XML pueda leer.  
  
 Carga masiva XML interpreta el esquema de asignación e identifica las tablas donde se insertarán los datos XML.  
  
 Se supone que está familiarizado con las siguientes características de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]:  
  
-   Esquemas XSD y XDR anotados. Para obtener más información acerca de los esquemas XSD anotados, vea [Introducción a los esquemas XSD anotados &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml/annotated-xsd-schemas/introduction-to-annotated-xsd-schemas-sqlxml-4-0.md). Para obtener información acerca de los esquemas XDR anotados, vea [esquemas XDR anotados &#40;desusado en SQLXML 4.0&#41;](../../../relational-databases/sqlxml/annotated-xsd-schemas/annotated-xdr-schemas-deprecated-in-sqlxml-4-0.md).  
  
-   Los mecanismos de inserción masiva de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], como la instrucción BULK INSERT de [!INCLUDE[tsql](../../../includes/tsql-md.md)] y la utilidad bcp. Para obtener más información, consulte [BULK INSERT &#40;Transact-SQL&#41; ](../../../t-sql/statements/bulk-insert-transact-sql.md) y [bcp (utilidad)](../../../tools/bcp-utility.md).  
  
## <a name="streaming-of-xml-data"></a>Transmitir datos XML por secuencias  
 Dado que el documento XML de origen puede ser grande, en el procesamiento de carga masiva no se carga en memoria todo el documento. En su lugar, Carga masiva XML interpreta los datos XML como un flujo y lo lee. A medida que la utilidad lee los datos, identifica las tablas de base de datos, genera los registros adecuados a partir del origen de datos XML y, a continuación, envía los registros a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para la inserción.  
  
 Por ejemplo, el siguiente documento XML de origen consta de  **\<cliente >** elementos y  **\<orden >** elementos secundarios:  
  
```  
<Customer ...>  
    <Order.../>  
    <Order .../>  
     ...  
</Customer>  
...  
```  
  
 Como la carga masiva XML lee el  **\<cliente >** elemento, genera un registro para el Customertable. Cuando lee el  **\</Customer >** etiqueta, carga masiva XML inserta ese registro en la tabla final [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. En la misma manera, cuando lee el  **\<orden >** elemento, carga masiva XML genera un registro para el ordertable fue y, a continuación, inserta ese registro en el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tabla al leer el  **\< / Ordenar >** etiqueta de cierre.  
  
## <a name="transacted-and-nontransacted-xml-bulk-load-operations"></a>Operaciones de Carga masiva XML con y sin transacciones  
 Carga masiva XML puede funcionar tanto en modo con transacciones como en modo sin transacciones. El rendimiento es normalmente óptimo si es la carga masiva en un modo sin transacciones: es decir, la propiedad de transacción se establece en FALSE) y se cumple alguna de las condiciones siguientes:  
  
-   Las tablas donde se realiza la carga masiva de los datos están vacías y no tienen índices.  
  
-   Las tablas tienen datos e índices únicos.  
  
 El enfoque sin transacciones no garantiza una reversión si se produce algún error en el proceso de carga masiva (si bien se pueden producir reversiones parciales). La carga masiva sin transacciones es adecuada cuando la base de datos está vacía. Por tanto, si algo sale mal, puede limpiar la base de datos e iniciar de nuevo Carga masiva XML.  
  
> [!NOTE]  
>  En modo sin transacciones, Carga masiva XML utiliza una transacción interna predeterminada y la confirma. Cuando la propiedad de transacción se establece en TRUE, carga masiva XML no llama a commit en esta transacción.  
  
 Si la propiedad de transacción se establece en TRUE, carga masiva XML crea archivos temporales, uno para cada tabla que se identifica en el esquema de asignación. Carga masiva XML almacena en primer lugar los registros del documento XML de origen en estos archivos temporales. A continuación, la instrucción BULK INSERT de [!INCLUDE[tsql](../../../includes/tsql-md.md)] recupera estos registros de los archivos y los almacena en las tablas correspondientes. Puede especificar la ubicación de estos archivos temporales mediante la propiedad TempFilePath. Debe asegurarse de que la cuenta de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que se utiliza con Carga masiva XML tiene acceso a esta ruta. Si no se especifica la propiedad TempFilePath, la ruta de acceso de archivo predeterminado que se especifica en la variable de entorno TEMP se usa para crear los archivos temporales.  
  
 Si la propiedad de transacción se establece en FALSE (valor predeterminado), carga masiva XML utiliza la interfaz IRowsetFastLoad de OLE DB para cargar los datos de forma masiva.  
  
 Si la propiedad ConnectionString establece la cadena de conexión y la propiedad de transacción se establece en TRUE, carga masiva XML funciona en su propio contexto de transacción. (Por ejemplo, Carga masiva XML inicia su propia transacción y confirma o revierte según corresponda.)  
  
 Si establece la propiedad ConnectionCommand la conexión con un objeto de conexión existente y la propiedad Transaction está establecida en TRUE, carga masiva XML no emite una instrucción COMMIT o ROLLBACK en el caso de una operación correcta o incorrecta, respectivamente. Si se produce un error, Carga masiva XML devuelve el mensaje de error adecuado. La decisión de emitir una instrucción COMMIT o ROLLBACK queda en manos del cliente que inició la carga masiva. El objeto de conexión que se usa para la carga masiva XML debe ser del tipo ICommand o ser un objeto de comando ADO.  
  
 En SQLXML 4.0, no se puede usar un ConnectionObject con la propiedad de transacción establecida en FALSE. No se admite el modo sin transacciones con un ConnectionObject porque es imposible abrir más de una interfaz IRowsetFastLoad en una sesión pasada.  
  
  
