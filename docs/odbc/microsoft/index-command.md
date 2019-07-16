---
title: Comando de índice | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- index command [ODBC]
ms.assetid: 694e8cf5-2f69-4001-9c1e-b735a4da3aff
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 61e55bec7a35009f0d83a43550a434e0966559b4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68019469"
---
# <a name="index-command"></a>Comando de índice
Crea un archivo de índice para mostrar y obtener acceso a registros de la tabla en un orden lógico.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
INDEX ON eExpression TO IDXFileName | TAG TagName [OF CDXFileName]  
   [FOR lExpression]  
   [COMPACT]  
   [ASCENDING | DESCENDING]  
   [UNIQUE | CANDIDATE]  
   [ADDITIVE]  
```  
  
## <a name="arguments"></a>Argumentos  
 *eExpression*  
 Especifica una expresión de índice que puede incluir el nombre de uno o varios campos de la tabla actual. Se crea una clave de índice basada en la expresión de índice en el archivo de índice para cada registro en la tabla. Visual FoxPro usa estas claves para mostrar y obtener acceso a registros de la tabla.  
  
> [!NOTE]  
>  Aunque no se recomienda, *eExpression* también puede ser una variable de memoria, un elemento de matriz, o un campo o expresión de campo de una tabla en otra área de trabajo. Campos de recordatorio no se puede usar por sí solo en las expresiones del archivo de índice; se debe combinar con otras expresiones de caracteres. Si tiene acceso a un índice que contenga una variable o campo que ya no existe o no se encuentra, Visual FoxPro genera un mensaje de error.  
  
 Si se intenta crear un índice con una clave que varían en longitud, la clave se rellenarán con espacios. Las claves de índice de longitud variable no se admiten en Visual FoxPro.  
  
 Es posible crear una clave de índice con longitud cero. Por ejemplo, se crea una clave de índice de longitud cero cuando la expresión de índice es una subcadena de un campo Memorando vacío. Una clave de índice de longitud cero, genera un mensaje de error. Cuando Visual FoxPro crea un índice, se evalúa como campos en el primer registro en la tabla. Si un campo está vacío, podría ser necesario introducir algunos datos temporales en el campo en el primer registro para evitar que una clave de índice de longitud 0.  
  
 PARA *IDXFileName*  
 Crea un archivo de índice .idx. El archivo de índice tiene el .idx de extensión predeterminado.  
  
 Etiqueta *TagName*[OF *CDXFileName*]  
 Crea un archivo de índice compuesto. Un archivo de índice compuesto es un archivo de índice único que consta de cualquier número de etiquetas independientes (entradas de índice). Cada etiqueta se identifica mediante su nombre de etiqueta única. Los nombres de etiqueta deben comenzar con una letra o un carácter de subrayado y pueden constar de cualquier combinación de hasta 10 letras, dígitos o caracteres de subrayado. El número de etiquetas en un archivo de índice compuesto está limitado sólo por la memoria disponible y espacio en disco.  
  
 Archivos de índice compuesto de usos múltiples son siempre compactos. No es necesario incluir compacto al crear un archivo de índice compuesto. Una extensión .cdx, se proporcionan nombres de archivos de índice compuesto.  
  
 Se pueden crear dos tipos de archivos de índice compuesto: estructurales y.  
  
 **Archivos de índice compuestos estructural** puede crear un archivo de índice compuesto estructural con etiqueta *TagName* excluyendo la opcional de *CDXFileName* cláusula. Un archivo de índice compuesto estructural siempre tiene el mismo nombre base que la tabla y se abre automáticamente cuando se abre en la tabla.  
  
 **Archivos de índice compuesto no estructurales** puede crear un archivo de índice compuesto no estructurales mediante la inclusión de *CDXFileName* después de la etiqueta *TagName*. A diferencia de un archivo de índice compuesto estructural, un archivo de índice compuesto no estructurales debe abrirse explícitamente con la cláusula de índice en uso.  
  
 Si ya se crea y abre un archivo de índice compuesto, al emitir el índice con etiqueta *TagName* agrega una etiqueta para el archivo de índice compuesto.  
  
 PARA *lExpression*  
 Especifica una condición mediante el cual solo los registros que cumplen la expresión de filtro *lExpression* están disponibles para mostrar y obtener acceso; claves de índice se crean en el archivo de índice para aquellos registros que coincidan con la expresión de filtro.  
  
 Tecnología de Visual FoxPro Rushmore optimiza un índice... PARA *lExpression* comando si *lExpression* es una expresión optimizable. Para mejorar el rendimiento, utilice una expresión optimizable en la cláusula FOR.  
  
 COMPACTO  
 Crea un archivo .idx compact.  
  
 ORDEN ASCENDENTE  
 Especifica un orden ascendente para el archivo .cdx. De forma predeterminada, se crean etiquetas cdx en orden ascendente. (Puede incluir ascendente como recordatorio del orden del archivo de índice). Una tabla puede indizarse en orden inverso al incluir descendente.  
  
 DESCENDENTE  
 Especifica un orden descendente para el archivo .cdx. No puede incluir descendente al crear .idx archivos de índice.  
  
 UNIQUE  
 Especifica que solo el primer registro encontrado con un valor de clave de índice determinado está incluido en un archivo .idx o etiqueta .cdx. UNIQUE puede usarse para evitar la presentación de o el acceso a los registros duplicados. Todos los registros agregados con claves de índice duplicados se excluyen del archivo de índice. Con la opción de índice única es idéntico al ejecutar SET UNIQUE ON antes de emitir REINDEX o índice.  
  
 Cuando un índice único o una etiqueta de índice está activo y se cambia un registro duplicado de una manera que cambia su clave de índice, se actualiza el índice o la etiqueta de índice. Sin embargo, el siguiente registro duplicado con la clave de índice original no está accesible o muestra hasta volver a indizar el archivo mediante REINDEX.  
  
 CANDIDATO  
 Crea una etiqueta de índice estructural de candidato. Se puede incluir la palabra clave CANDIDATA sólo cuando se crea una etiqueta de índice estructural; en caso contrario, Visual FoxPro genera un mensaje de error.  
  
 Una etiqueta de índice candidato impide que los valores duplicados en el campo o la combinación de campos especificados en la expresión del índice *eExpression*. El término *candidato* hace referencia al tipo de índice; porque índices candidatos evitar valores duplicados, se califican como "candidato" es un índice principal.  
  
 Visual FoxPro genera un error si se crea una etiqueta de índice candidato para un campo o una combinación de campos que ya contiene valores duplicados.  
  
 ADITIVO  
 Mantiene abra los archivos de índice abierto anteriormente. Si se omite la cláusula ADITIVO al crear un archivo de índice o archivos de una tabla con índice, se cierran los archivos de índice abierto anteriormente (excepto el índice compuesto estructural).  
  
## <a name="remarks"></a>Comentarios  
 Se muestran los registros en una tabla que tiene un archivo de índice y se obtiene acceso en el orden especificado por la expresión del índice. No se cambia el orden físico de los registros de la tabla mediante un archivo de índice.  
  
## <a name="index-types"></a>Tipos de índices  
 Visual FoxPro le permite crear dos tipos de archivos de índice:  
  
-   Archivos de índice .cdx que contiene varias entradas de índice que se denominan etiquetas compuestos  
  
-   archivos de índice .idx que contiene una entrada de índice  
  
 También puede crear un archivo de índice compuesto estructural, que se abre automáticamente con la tabla.  
  
> [!NOTE]  
>  Dado que los archivos de índice compuesto estructural se abren automáticamente cuando se abre en la tabla, son el tipo de índice preferido.  
  
 Incluir compacto para crear archivos de índice de .idx compact. Archivos de índice compuesto siempre son compactos.  
  
## <a name="index-order-and-updating"></a>Orden de índice y actualización  
 Sólo un índice (el archivo índice maestro) o (etiqueta de la maestra) controla el orden en el que se muestra o se tiene acceso a la tabla. Ciertos comandos (por ejemplo, SEEK) usan el archivo de índice maestro o una etiqueta para buscar registros. Sin embargo, todos los abiertos .idx y .cdx con archivos de índice se actualizan cuando se realizan cambios en la tabla.  
  
## <a name="user-defined-functions"></a>Funciones definidas por el usuario  
 Aunque una expresión de índice puede contener una función definida por el usuario, no se deben usar las funciones definidas por el usuario en una expresión de índice. Funciones definidas por el usuario en una expresión de índice aumentan el tiempo necesario para crear o actualizar el índice. Además, las actualizaciones del índice podrían no producirse cuando se utiliza una función definida por el usuario para una expresión de índice.  
  
 Si usa una función definida por el usuario en una expresión de índice, Visual FoxPro debe ser capaz de encontrar la función definida por el usuario. Cuando Visual FoxPro crea un índice, la expresión del índice se guarda en el archivo de índice, pero solo una referencia a la función definida por el usuario se incluye en la expresión del índice.  
  
## <a name="see-also"></a>Vea también  
 [Modificar tabla - comando SQL](../../odbc/microsoft/alter-table-sql-command.md)   
 [Eliminar etiqueta, comando](../../odbc/microsoft/delete-tag-command.md)   
 [Comando COLLATE SET](../../odbc/microsoft/set-collate-command.md)   
 [CONJUNTO único comando](../../odbc/microsoft/set-unique-command.md)
