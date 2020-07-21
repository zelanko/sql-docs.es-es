---
title: Instrucciones y limitaciones de diagramas (SQLXML)
description: Obtenga información sobre las instrucciones y limitaciones del uso de diagramas XML en SQLXML 4,0.
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
ms.openlocfilehash: fb774fd8dbb05b52e4f57fcf78d4ecd4c923ccb8
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85790653"
---
# <a name="guidelines-and-limitations-of-xml-updategrams-sqlxml-40"></a>Instrucciones y limitaciones de los diagramas de actualización XML (SQLXML 4.0)
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  Recuerde lo siguiente al utilizar los diagramas de actualización XML:  
  
-   Si usa un diagrama para una operación de inserción con un solo par de **\<before>** **\<after>** bloques y, **\<before>** se puede omitir el bloque. Por el contrario, en el caso de una operación de eliminación, el **\<after>** bloque se puede omitir.  
  
-   Si usa un diagrama con varios **\<before>** **\<after>** bloques y en la **\<sync>** etiqueta, **\<before>** **\<after>** se deben especificar bloques y bloques para formar **\<before>** y **\<after>** pares.  
  
-   Las actualizaciones de un diagrama de actualización se aplican a la vista XML proporcionada por el esquema XML. Por consiguiente, para que la asignación predeterminada sea correcta debe especificar el nombre de archivo del esquema del diagrama de actualización o, si no se proporciona el nombre de archivo, los nombres de atributo y elemento deben coincidir con los nombres de columna y tabla de la base de datos.  
  
-   SQLXML 4.0 requiere que todos los valores de columna de un diagrama de actualización estén asignados explícitamente en el esquema (XDR o XSD) proporcionado para componer la vista XML de sus elementos secundarios. Este comportamiento difiere de las versiones anteriores de SQLXML, que permitían un valor para una columna no asignada en el esquema si estaba implícita como parte de la clave externa en una anotación **SQL: Relationship** . (Observe que este cambio no afecta a la propagación de los valores de clave principal a los elementos secundarios, que todavía se produce para SQLXML 4.0 si no se especifica ningún valor explícitamente para el elemento secundario).  
  
-   Si usa un diagrama para modificar los datos de una columna binaria (como el tipo de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **imagen** ), debe proporcionar un esquema de asignación en el que [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] se debe especificar el tipo de datos (por ejemplo, **SQL: DataType = "Image"**) y el tipo de datos XML (por ejemplo, **DT: type = "BinHex"** o **DT: type = "binbase64**). Los datos de la columna binaria deben especificarse en el diagrama; diagrama omite la anotación **SQL: URL-encode** que se especifica en el esquema de asignación.  
  
-   Cuando se escribe un esquema XSD, si el valor que se especifica para la anotación **SQL: relation** o **SQL: Field** incluye un carácter especial, como un carácter de espacio (por ejemplo, en el nombre de la tabla "Order Details"), este valor se debe incluir entre corchetes (por ejemplo, "[Order Details]").  
  
-   Al utilizar los diagramas de actualización, no se admiten las relaciones de cadena. Por ejemplo, si las tablas A y C están relacionadas mediante una relación de cadena que utiliza la tabla B, se producirá el error siguiente al intentar ejecutar el diagrama de actualización:  
  
    ```  
    There is an inconsistency in the schema provided.  
    ```  
  
     Aun cuando el esquema y el diagrama de actualización sean correctos y tengan un formato válido, se producirá este error si está presente una relación de cadena.  
  
-   Diagramas no permiten el paso de datos de tipo de **imagen** como parámetros durante las actualizaciones.  
  
-   Los tipos de objetos binarios grandes (BLOB) como **text/ntext** e imágenes no se deben usar en el **\<before>** bloque de cuando se trabaja con diagramas, porque se incluirán para su uso en el control de simultaneidad. Esto puede producir problemas con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] debido a las limitaciones en la comparación para los tipos BLOB. Por ejemplo, la palabra clave LIKE se usa en la cláusula WHERE para comparar entre las columnas del tipo de datos **Text** ; sin embargo, se producirá un error en las comparaciones en el caso de los tipos BLOB donde el tamaño de los datos es mayor que 8 k.  
  
-   Los caracteres especiales en los datos **ntext** pueden producir problemas con SQLXML 4,0 debido a las limitaciones de la comparación de los tipos de BLOB. Por ejemplo, el uso de "[Serializable]" en el **\<before>** bloque de un diagramas cuando se usa en la comprobación de simultaneidad de una columna de tipo **ntext** producirá un error con la siguiente descripción del error SQLOLEDB:  
  
    ```  
    Empty update, no updatable rows found   Transaction aborted  
    ```  
  
## <a name="see-also"></a>Consulte también  
 [Consideraciones de seguridad de diagrama &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
