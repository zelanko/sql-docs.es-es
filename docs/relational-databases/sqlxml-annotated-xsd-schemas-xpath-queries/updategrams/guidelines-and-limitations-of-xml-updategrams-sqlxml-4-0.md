---
title: Instrucciones y limitaciones de los diagramas de actualización XML (SQLXML 4.0) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- updategrams [SQLXML], about updategrams
ms.assetid: b5231859-14e2-4276-bc17-db2817b6f235
caps.latest.revision: 31
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 9dda62acddf1dbda2fe37c4ed458c37f5725ffdd
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="guidelines-and-limitations-of-xml-updategrams-sqlxml-40"></a>Instrucciones y limitaciones de los diagramas de actualización XML (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Recuerde lo siguiente al utilizar los diagramas de actualización XML:  
  
-   Si está utilizando un diagrama de actualización para una operación de inserción con solo un único par de  **\<antes >** y  **\<después >** bloques, el  **\<antes de >** bloque puede omitirse. Por el contrario, en el caso de una operación de eliminación, el  **\<después >** bloque puede omitirse.  
  
-   Si usa un diagrama de actualización con varios  **\<antes >** y  **\<después >** bloques en el  **\<sincronización >** etiqueta, ambos  **\<antes >** bloques y  **\<después >** se deben especificar al formulario  **\<antes >** y  **\<después >** pares.  
  
-   Las actualizaciones de un diagrama de actualización se aplican a la vista XML proporcionada por el esquema XML. Por consiguiente, para que la asignación predeterminada sea correcta debe especificar el nombre de archivo del esquema del diagrama de actualización o, si no se proporciona el nombre de archivo, los nombres de atributo y elemento deben coincidir con los nombres de columna y tabla de la base de datos.  
  
-   SQLXML 4.0 requiere que todos los valores de columna de un diagrama de actualización estén asignados explícitamente en el esquema (XDR o XSD) proporcionado para componer la vista XML de sus elementos secundarios. Este comportamiento difiere de las versiones anteriores de SQLXML, que permite un valor para una columna no asignada en el esquema si estaba implícito como parte de la clave externa de una **SQL: Relationship** anotación. (Observe que este cambio no afecta a la propagación de los valores de clave principal a los elementos secundarios, que todavía se produce para SQLXML 4.0 si no se especifica ningún valor explícitamente para el elemento secundario).  
  
-   Si usa un diagrama de actualización para modificar los datos de una columna binaria (como el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **imagen** tipo de datos), debe proporcionar un esquema de asignación en el que el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tipo de datos (por ejemplo, **SQL: DataType = "image"** ) y el tipo de datos XML (por ejemplo, **dt: Type = "binhex"** o **dt: Type = "binbase64**) debe especificarse. Los datos de la columna binaria deben especificarse en el diagrama de actualización; el **SQL-codificar** anotación que se especifica en el esquema de asignación es omitido por el diagrama de actualización.  
  
-   Cuando se escribe un esquema XSD, si el valor especificado para la **SQL: relation** o **SQL: Field** anotación incluye un carácter especial, como un carácter de espacio (por ejemplo, en "Order Details" nombre de la tabla), este valor debe ir entre corchetes (por ejemplo, "[detalles de pedido]").  
  
-   Al utilizar los diagramas de actualización, no se admiten las relaciones de cadena. Por ejemplo, si las tablas A y C están relacionadas mediante una relación de cadena que utiliza la tabla B, se producirá el error siguiente al intentar ejecutar el diagrama de actualización:  
  
    ```  
    There is an inconsistency in the schema provided.  
    ```  
  
     Aun cuando el esquema y el diagrama de actualización sean correctos y tengan un formato válido, se producirá este error si está presente una relación de cadena.  
  
-   Los diagramas de actualización no permiten el paso de **imagen** tipo de datos como parámetros durante las actualizaciones.  
  
-   Tipos de objeto binario grande (BLOB) como **texto/ntext** y las imágenes no deben usarse en el  **\<antes >** bloquear al trabajar con diagramas de actualización, porque esto los incluiría para su uso en control de simultaneidad. Esto puede producir problemas con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] debido a las limitaciones en la comparación para los tipos BLOB. Por ejemplo, se utiliza la palabra clave LIKE en la cláusula WHERE para comparar entre las columnas de la **texto** tipo de datos; sin embargo, las comparaciones se producirá un error en el caso de los tipos BLOB donde el tamaño de los datos es mayor que 8 KB.  
  
-   Caracteres especiales en **ntext** datos pueden causar problemas con SQLXML 4.0 debido a las limitaciones en la comparación para los tipos de BLOB. Por ejemplo, el uso de "[Serializable]" en la  **\<antes >** bloque de un diagrama de actualización cuando se utiliza en la comprobación de simultaneidad de una columna de **ntext** se producirá un error de tipo con SQLOLEDB siguiente Descripción del error:  
  
    ```  
    Empty update, no updatable rows found   Transaction aborted  
    ```  
  
## <a name="see-also"></a>Vea también  
 [Consideraciones de seguridad de updategram &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
