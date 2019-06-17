---
title: Instrucciones y limitaciones de los diagramas de actualización XML (SQLXML 4.0) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- updategrams [SQLXML], about updategrams
ms.assetid: b5231859-14e2-4276-bc17-db2817b6f235
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 953fc5b7c203faa8fa6a9820993a3d0fd7a7de40
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66014826"
---
# <a name="guidelines-and-limitations-of-xml-updategrams-sqlxml-40"></a>Instrucciones y limitaciones de los diagramas de actualización XML (SQLXML 4.0)
  Recuerde lo siguiente al utilizar los diagramas de actualización XML:  
  
-   Si está utilizando un diagrama de actualización para una operación de inserción con solo un único par de  **\<antes >** y  **\<después >** bloques, el  **\<antes >** bloque puede omitirse. Por el contrario, en el caso de una operación de eliminación, la  **\<después >** bloque puede omitirse.  
  
-   Si usa un diagrama de actualización con varios  **\<antes >** y  **\<después >** bloques en el  **\<sincronización >** etiquetar, ambos  **\<antes >** bloques y  **\<después >** bloques deben especificarse al formulario  **\<antes >** y  **\<después >** pares.  
  
-   Las actualizaciones de un diagrama de actualización se aplican a la vista XML proporcionada por el esquema XML. Por consiguiente, para que la asignación predeterminada sea correcta debe especificar el nombre de archivo del esquema del diagrama de actualización o, si no se proporciona el nombre de archivo, los nombres de atributo y elemento deben coincidir con los nombres de columna y tabla de la base de datos.  
  
-   SQLXML 4.0 requiere que todos los valores de columna de un diagrama de actualización estén asignados explícitamente en el esquema (XDR o XSD) proporcionado para componer la vista XML de sus elementos secundarios. Este comportamiento difiere de las versiones anteriores de SQLXML, que permitían un valor de una columna no asignado en el esquema si estaba implícito como parte de la clave externa de una anotación `sql:relationship`. (Observe que este cambio no afecta a la propagación de los valores de clave principal a los elementos secundarios, que todavía se produce para SQLXML 4.0 si no se especifica ningún valor explícitamente para el elemento secundario).  
  
-   Si usa un diagrama de actualización para modificar datos en una columna binaria (como el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] `image` tipo de datos), debe proporcionar un esquema de asignación en el que el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tipo de datos (por ejemplo, `sql:datatype="image"`) y el tipo de datos XML (por ejemplo, `dt:type="binhex"`o `dt:type="binbase64`) debe especificarse. Los datos de la columna binaria se deben especificar en el diagrama de actualización; el diagrama de actualización omite la anotación `sql:url-encode` especificada en el esquema de asignación.  
  
-   Cuando escribe un esquema XSD, si el valor que especifica para la anotación `sql:relation` o `sql:field` incluye un carácter especial, como un carácter de espacio en blanco (por ejemplo, en el nombre de tabla "Detalles de pedido"), este valor se debe incluir entre corchetes (por ejemplo, "[Detalles de pedido]").  
  
-   Al utilizar los diagramas de actualización, no se admiten las relaciones de cadena. Por ejemplo, si las tablas A y C están relacionadas mediante una relación de cadena que utiliza la tabla B, se producirá el error siguiente al intentar ejecutar el diagrama de actualización:  
  
    ```  
    There is an inconsistency in the schema provided.  
    ```  
  
     Aun cuando el esquema y el diagrama de actualización sean correctos y tengan un formato válido, se producirá este error si está presente una relación de cadena.  
  
-   Los diagramas de actualización no permiten el paso de datos del tipo `image` como parámetros durante las actualizaciones.  
  
-   Tipos de objeto binario grande (BLOB) como `text/ntext` y no se deben usar imágenes en el  **\<antes >** bloquear al trabajar con diagramas de actualización, porque esto los incluiría para su uso en el control de simultaneidad. Esto puede producir problemas con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] debido a las limitaciones en la comparación para los tipos BLOB. Por ejemplo, la palabra clave LIKE se usa en la cláusula WHERE para comparar entre las columnas del tipo de datos `text`; sin embargo, se producirá un error en las comparaciones en el caso de los tipos BLOB donde el tamaño de los datos supere los 8 K.  
  
-   Los caracteres especiales en los datos `ntext` pueden producir problemas con SQLXML 4.0 debido a las limitaciones en la comparación para los tipos BLOB. Por ejemplo, el uso de "[Serializable]" en el  **\<antes >** bloque de un diagrama de actualización cuando se utiliza en la comprobación de simultaneidad de una columna de `ntext` se producirá un error de tipo con la descripción del error SQLOLEDB siguiente:  
  
    ```  
    Empty update, no updatable rows found   Transaction aborted  
    ```  
  
## <a name="see-also"></a>Vea también  
 [Consideraciones de seguridad de updategram &#40;SQLXML 4.0&#41;](../security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
