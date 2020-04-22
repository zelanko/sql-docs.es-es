---
title: Usar la opción BINARY BASE64 | Microsoft Docs
description: Obtenga información acerca de cómo usar la opción BINARY BASE64 en una consulta SQL para devolver datos binarios en el formato de codificación Base64.
ms.custom: ''
ms.date: 04/03/2020
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- AUTO FOR XML mode, BINARY BASE64 option
ms.assetid: 86a7bb85-7f83-412a-b775-d2c379702fe9
author: RothJa
ms.author: jroth
ms.openlocfilehash: fffd3833256ee6afa9dd3731d5cf02e99913e565
ms.sourcegitcommit: a3f5c3742d85d21f6bde7c6ae133060dcf1ddd44
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/15/2020
ms.locfileid: "81388359"
---
# <a name="use-the-binary-base64-option"></a>Usar la opción BINARY BASE64

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

Si en la consulta se especifica la opción BINARY BASE64, los datos binarios se devuelven en formato de codificación en base64.

De manera predeterminada, si no se especifica en la consulta la opción BINARY BASE64, el modo AUTO admite la codificación URL de datos binarios. Se devuelve una referencia a una URL relativa a la raíz virtual de la base de datos. Esta referencia está en la base de datos donde se ha ejecutado la consulta. La referencia devuelta se puede utilizar para obtener acceso a los datos binarios reales en operaciones posteriores. Este acceso se logra mediante la consulta de SQLXML dbobject ISAPI. La consulta debe proporcionar suficiente información para identificar la imagen. Dicha información podría incluir las columnas de la clave principal.

## <a name="column-alias"></a>Alias de columna

No utilice un alias para una columna binaria al consultar una vista y usar el modo FOR XML AUTO. Si se utiliza un alias, este se devuelve en la codificación de la dirección URL de los datos binarios. En operaciones posteriores, el alias no tiene ningún significado. El alias sin significado y la codificación de dirección URL no se pueden utilizar para recuperar la imagen.

### <a name="cast-to-a-blob"></a>Conversión a un BLOB

En una consulta SELECT, la conversión de cualquier columna en un objeto binario grande (BLOB) convierte la columna en una entidad temporal. Como es temporal, el BLOB pierde el nombre de la tabla y de la columna asociados. Esta conversión hace que las consultas en modo AUTO generen un error, ya que el sistema no sabe dónde colocar este valor en la jerarquía XML.

Por ejemplo, considere la siguiente tabla con una fila.

```sql
CREATE TABLE MyTable (Col1 int PRIMARY KEY, Col2 binary)
INSERT INTO MyTable VALUES (1, 0x7);
```

La consulta siguiente produce un error debido a la conversión en un objeto binario grande (BLOB):

```sql
SELECT Col1,
CAST(Col2 as image) as Col2
FROM MyTable
FOR XML AUTO;
```

La solución consiste en agregar la opción BINARY BASE64 a la cláusula FOR XML. Si se quita la conversión, la consulta produce buenos resultados.

```sql
SELECT Col1,
CAST(Col2 as image) as Col2
FROM MyTable
FOR XML AUTO, BINARY BASE64;
```

Espere el siguiente resultado correcto:

```console
<MyTable Col1="1" Col2="Bw==" />
```

## <a name="see-also"></a>Consulte también

[Usar el modo AUTO con FOR XML](../../relational-databases/xml/use-auto-mode-with-for-xml.md)
