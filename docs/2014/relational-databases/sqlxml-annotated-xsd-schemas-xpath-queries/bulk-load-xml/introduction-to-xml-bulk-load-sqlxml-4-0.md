---
title: Introducción a la carga masiva XML (SQLXML 4,0) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d257b6eee1fb3adc0ba611f58a1d5eea5adf3f86
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66013386"
---
# <a name="introduction-to-xml-bulk-load-sqlxml-40"></a>Introducción a la carga masiva XML (SQLXML 4.0)
  La carga masiva XML es un objeto COM independiente que permite cargar datos XML semiestructurados en tablas de Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
 Puede insertar datos XML en una base de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] mediante una instrucción INSERT y la función OPENXML; sin embargo, la utilidad Carga masiva proporciona mejor rendimiento cuando es necesario insertar grandes cantidades de datos XML.  
  
 El método Execute del modelo de objetos de carga masiva XML toma dos parámetros:  
  
-   Una definición de esquema XML anotado (XSD) o un esquema reducido de datos XML (XDR). La utilidad Carga masiva XML interpreta este esquema de asignación y las anotaciones que se especifican en el esquema para identificar las tablas de SQL Server donde se insertarán los datos XML.  
  
-   Un documento o fragmento de documento XML (un fragmento de documento es un documento sin un elemento de nivel superior único). Se puede especificar un nombre de archivo o un flujo del que Carga masiva XML pueda leer.  
  
 Carga masiva XML interpreta el esquema de asignación e identifica las tablas donde se insertarán los datos XML.  
  
 Se supone que está familiarizado con las siguientes características de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]:  
  
-   Esquemas XSD y XDR anotados. Para obtener más información acerca de los esquemas XSD anotados, vea [Introducción a los esquemas XSD anotados &#40;SQLXML 4,0&#41;](../../sqlxml/annotated-xsd-schemas/introduction-to-annotated-xsd-schemas-sqlxml-4-0.md). Para obtener información acerca de los esquemas XDR anotados, vea [esquemas XDR anotados &#40;en desuso en SQLXML 4,0&#41;](../../sqlxml/annotated-xsd-schemas/annotated-xdr-schemas-deprecated-in-sqlxml-4-0.md).  
  
-   Los mecanismos de inserción masiva de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], como la instrucción BULK INSERT de [!INCLUDE[tsql](../../../includes/tsql-md.md)] y la utilidad bcp. Para obtener más información, vea BULK INSERT &#40;la utilidad&#41;y [BCP](../../../tools/bcp-utility.md)de [Transact-SQL](/sql/t-sql/statements/bulk-insert-transact-sql) .  
  
## <a name="streaming-of-xml-data"></a>Transmitir datos XML por secuencias  
 Dado que el documento XML de origen puede ser grande, en el procesamiento de carga masiva no se carga en memoria todo el documento. En su lugar, Carga masiva XML interpreta los datos XML como un flujo y lo lee. A medida que la utilidad lee los datos, identifica las tablas de base de datos, genera los registros adecuados a partir del origen de datos XML y, a continuación, envía los registros a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para la inserción.  
  
 Por ejemplo, el siguiente documento XML de origen se compone de elementos ** \<>del cliente** y ** \<un pedido>** elementos secundarios:  
  
```  
<Customer ...>  
    <Order.../>  
    <Order .../>  
     ...  
</Customer>  
...  
```  
  
 A medida que la carga masiva XML lee el elemento ** \<>del cliente** , genera un registro para el Customertable. Cuando lee la ** \</Customer>** etiqueta de cierre, la carga masiva XML inserta el registro en la tabla de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Del mismo modo, cuando lee el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ** \<elemento Order>** , la carga masiva XML genera un registro para el Ordertable y, a continuación, inserta ese registro en la tabla al leer la ** \<** etiqueta de cierre/Order>.  
  
## <a name="transacted-and-nontransacted-xml-bulk-load-operations"></a>Operaciones de Carga masiva XML con y sin transacciones  
 Carga masiva XML puede funcionar tanto en modo con transacciones como en modo sin transacciones. El rendimiento suele ser óptimo si se realiza una carga masiva en un modo no transactd: es decir, la propiedad de transacción se establece en FALSE y se cumple cualquiera de las condiciones siguientes:  
  
-   Las tablas donde se realiza la carga masiva de los datos están vacías y no tienen índices.  
  
-   Las tablas tienen datos e índices únicos.  
  
 El enfoque sin transacciones no garantiza una reversión si se produce algún error en el proceso de carga masiva (si bien se pueden producir reversiones parciales). La carga masiva sin transacciones es adecuada cuando la base de datos está vacía. Por tanto, si algo sale mal, puede limpiar la base de datos e iniciar de nuevo Carga masiva XML.  
  
> [!NOTE]  
>  En modo sin transacciones, Carga masiva XML utiliza una transacción interna predeterminada y la confirma. Cuando la propiedad de transacción se establece en TRUE, la carga masiva XML no llama a commit en esta transacción.  
  
 Si la propiedad de transacción se establece en TRUE, la carga masiva XML crea archivos temporales, uno para cada tabla que se identifica en el esquema de asignación. Carga masiva XML almacena en primer lugar los registros del documento XML de origen en estos archivos temporales. A continuación, la instrucción BULK INSERT de [!INCLUDE[tsql](../../../includes/tsql-md.md)] recupera estos registros de los archivos y los almacena en las tablas correspondientes. Puede especificar la ubicación de estos archivos temporales mediante la propiedad TempFilePath. Debe asegurarse de que la cuenta de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que se utiliza con Carga masiva XML tiene acceso a esta ruta. Si no se especifica la propiedad TempFilePath, se usa la ruta de acceso de archivo predeterminada que se especifica en la variable de entorno TEMP para crear los archivos temporales.  
  
 Si la propiedad Transaction está establecida en FALSE (el valor predeterminado), la carga masiva XML usa la interfaz OLE DB IRowsetFastLoad para cargar los datos de forma masiva.  
  
 Si la propiedad ConnectionString establece la cadena de conexión y la propiedad Transaction está establecida en TRUE, la carga masiva XML funciona en su propio contexto de transacción. (Por ejemplo, Carga masiva XML inicia su propia transacción y confirma o revierte según corresponda.)  
  
 Si la propiedad ConnectionCommand establece la conexión con un objeto de conexión existente y la propiedad de transacción está establecida en TRUE, la carga masiva XML no emite una instrucción COMMIT o ROLLBACK en caso de que se produzca un error o un error, respectivamente. Si se produce un error, Carga masiva XML devuelve el mensaje de error adecuado. La decisión de emitir una instrucción COMMIT o ROLLBACK queda en manos del cliente que inició la carga masiva. El objeto de conexión que se usa para la carga masiva XML debe ser de tipo ICommand o ser un objeto de comando de ADO.  
  
 En SQLXML 4,0, no se puede usar un ConnectionObject con la propiedad de transacción establecida en FALSE. El modo no transactd no es compatible con ConnectionObject porque es imposible abrir más de una interfaz IRowsetFastLoad en una sesión pasada.  
  
  
