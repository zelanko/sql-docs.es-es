---
title: Instrucciones y limitaciones de diagramas (SQLXML)
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- updategrams [SQLXML], about updategrams
ms.assetid: b5231859-14e2-4276-bc17-db2817b6f235
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 9eb717968b191bb7d80f5d68542178bf32734b00
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/19/2019
ms.locfileid: "75241295"
---
# <a name="guidelines-and-limitations-of-xml-updategrams-sqlxml-40"></a>Instrucciones y limitaciones de los diagramas de actualización XML (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Recuerde lo siguiente al utilizar los diagramas de actualización XML:  
  
-   Si usa un diagrama para una operación de inserción con un solo par de ** \<>** y ** \<después de>** bloques, el ** \<bloque Before>** se puede omitir. Por el contrario, en el caso de una operación de eliminación, el ** \<bloque After>** se puede omitir.  
  
-   Si usa un diagrama con varios ** \<de antes>** y ** \<después de>** bloques en la ** \<** etiqueta de>de sincronización, ** \<antes de>** los bloques y ** \<después de>** bloques deben especificarse para formar ** \<antes de>** y ** \<después** de>pares.  
  
-   Las actualizaciones de un diagrama de actualización se aplican a la vista XML proporcionada por el esquema XML. Por consiguiente, para que la asignación predeterminada sea correcta debe especificar el nombre de archivo del esquema del diagrama de actualización o, si no se proporciona el nombre de archivo, los nombres de atributo y elemento deben coincidir con los nombres de columna y tabla de la base de datos.  
  
-   SQLXML 4.0 requiere que todos los valores de columna de un diagrama de actualización estén asignados explícitamente en el esquema (XDR o XSD) proporcionado para componer la vista XML de sus elementos secundarios. Este comportamiento difiere de las versiones anteriores de SQLXML, que permitían un valor para una columna no asignada en el esquema si estaba implícita como parte de la clave externa en una anotación **SQL: Relationship** . (Observe que este cambio no afecta a la propagación de los valores de clave principal a los elementos secundarios, que todavía se produce para SQLXML 4.0 si no se especifica ningún valor explícitamente para el elemento secundario).  
  
-   Si usa un diagrama para modificar los datos de una columna binaria (como el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tipo de datos de **imagen** ), debe proporcionar un esquema de asignación en el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que se debe especificar el tipo de datos (por ejemplo, **SQL: DataType = "Image"**) y el tipo de datos XML (por ejemplo, **DT: type = "BinHex"** o **DT: type = "binbase64**). Los datos de la columna binaria deben especificarse en el diagrama; diagrama omite la anotación **SQL: URL-encode** que se especifica en el esquema de asignación.  
  
-   Cuando se escribe un esquema XSD, si el valor que se especifica para la anotación **SQL: relation** o **SQL: Field** incluye un carácter especial, como un carácter de espacio (por ejemplo, en el nombre de la tabla "Order Details"), este valor se debe incluir entre corchetes (por ejemplo, "[Order Details]").  
  
-   Al utilizar los diagramas de actualización, no se admiten las relaciones de cadena. Por ejemplo, si las tablas A y C están relacionadas mediante una relación de cadena que utiliza la tabla B, se producirá el error siguiente al intentar ejecutar el diagrama de actualización:  
  
    ```  
    There is an inconsistency in the schema provided.  
    ```  
  
     Aun cuando el esquema y el diagrama de actualización sean correctos y tengan un formato válido, se producirá este error si está presente una relación de cadena.  
  
-   Diagramas no permiten el paso de datos de tipo de **imagen** como parámetros durante las actualizaciones.  
  
-   Los tipos de objetos binarios grandes (BLOB) como **text/ntext** e imágenes no se deben usar en el bloque ** \<Before>** en cuando se trabaja con diagramas, ya que se incluirán para su uso en el control de simultaneidad. Esto puede producir problemas con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] debido a las limitaciones en la comparación para los tipos BLOB. Por ejemplo, la palabra clave LIKE se usa en la cláusula WHERE para comparar entre las columnas del tipo de datos **Text** ; sin embargo, se producirá un error en las comparaciones en el caso de los tipos BLOB donde el tamaño de los datos es mayor que 8 k.  
  
-   Los caracteres especiales en los datos **ntext** pueden producir problemas con SQLXML 4,0 debido a las limitaciones de la comparación de los tipos de BLOB. Por ejemplo, el uso de "[Serializable]" en el bloque ** \<Before>** de diagramas cuando se usa en la comprobación de simultaneidad de una columna de tipo **ntext** producirá un error con la siguiente descripción del error SQLOLEDB:  
  
    ```  
    Empty update, no updatable rows found   Transaction aborted  
    ```  
  
## <a name="see-also"></a>Véase también  
 [Consideraciones de seguridad de diagrama &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
