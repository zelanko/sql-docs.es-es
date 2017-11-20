---
title: Comando INDEX | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- index command [ODBC]
ms.assetid: 694e8cf5-2f69-4001-9c1e-b735a4da3aff
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: cdec619d99c610c75b9b27de710cd4e5913602f6
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

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
 Especifica una expresión de índice que puede incluir el nombre de un campo o campos de la tabla actual. Una clave de índice basada en la expresión de índice se crea en el archivo de índice para cada registro en la tabla. Visual FoxPro utiliza estas claves para mostrar y obtener acceso a registros de la tabla.  
  
> [!NOTE]  
>  Aunque no se recomienda, *eExpression* también puede ser una variable de memoria, un elemento de matriz, o un campo o expresión de campo de una tabla en otra área de trabajo. Campos de memorando no pueden utilizarse por sí solo en las expresiones de archivo de índice; se debe combinar con otras expresiones de caracteres. Si tiene acceso a un índice que contenga una variable o un campo que ya no existe o no se encuentra, Visual FoxPro genera un mensaje de error.  
  
 Si intenta crear un índice con una clave que varían en longitud, la clave se rellenan con espacios. Las claves de índice de longitud variable no son compatibles con Visual FoxPro.  
  
 Es posible crear una clave de índice con longitud cero. Por ejemplo, se crea una clave de índice de longitud cero si la expresión de índice es una subcadena de un campo de memorando vacía. Una clave de índice de longitud cero, genera un mensaje de error. Cuando Visual FoxPro crea un índice, se evalúa como campos en el primer registro en la tabla. Si un campo está vacío, podría ser necesario introducir algunos datos temporales en el campo en el primer registro para evitar que una clave de índice de longitud 0.  
  
 PARA *IDXFileName*  
 Crea un archivo de índice .idx. El archivo de índice tiene el .idx de extensión de manera predeterminada.  
  
 Etiqueta *TagName*[OF *CDXFileName*]  
 Crea un archivo de índice compuesto. Un archivo de índice compuesto es un archivo de índice único que está formada por cualquier número de etiquetas independientes (entradas de índice). Cada etiqueta se identifica mediante su nombre de etiqueta único. Nombres de etiqueta deben empezar por una letra o un carácter de subrayado y pueden contener cualquier combinación de hasta 10 letras, dígitos o caracteres de subrayado. El número de etiquetas en un archivo de índice compuesto está limitado únicamente por la memoria disponible y espacio en disco.  
  
 Archivos de índice compuesto de usos múltiples son siempre compactos. No es necesario incluir compacto al crear un archivo de índice compuesto. Nombres de archivos de índice compuestos tienen la extensión .cdx.  
  
 Se pueden crear dos tipos de archivos de índice compuesto: estructurales y.  
  
 **Archivos de índice compuestos estructural** puede crear un archivo de índice compuesto estructural con etiqueta *TagName* Si excluye el de opcional *CDXFileName* cláusula. Un archivo de índice compuesto estructural siempre tiene el mismo nombre base que la tabla y se abre automáticamente cuando se abre la tabla.  
  
 **Archivos de índice compuestos estructurales** puede crear un archivo de índice compuesto no estructurales mediante la inclusión de *CDXFileName* después de la etiqueta *TagName*. A diferencia de un archivo de índice compuesto estructural, un archivo de índice compuesto no estructurales debe abrirse explícitamente con la cláusula de índice en uso.  
  
 Si ya se ha creado y abierto un archivo de índice compuesto, emisión de índice con etiqueta *TagName* agrega una etiqueta para el archivo de índice compuesto.  
  
 PARA *lExpression*  
 Especifica una condición por la que solo los registros que cumplen la expresión de filtro *lExpression* están disponibles para mostrar y obtener acceso; las claves de índice se crean en el archivo de índice para aquellos registros que coincidan con la expresión de filtro.  
  
 Tecnología Visual FoxPro Rushmore optimiza un índice... PARA *lExpression* comando si *lExpression* es una expresión optimizable. Para obtener el mejor rendimiento, utilice una expresión optimizable en la cláusula FOR.  
  
 COMPACTAR  
 Crea un archivo .idx compact.  
  
 ORDEN ASCENDENTE  
 Especifica un orden ascendente para el archivo .cdx. De forma predeterminada, se crean .cdx etiquetas en orden ascendente. (Puede incluir ascendente como recordatorio de orden del archivo de índice). Una tabla puede indizarse en orden inverso al incluir descendente.  
  
 ORDEN DESCENDENTE  
 Especifica un orden descendente para el archivo .cdx. No puede incluir descendente al crear .idx archivos de índice.  
  
 UNIQUE  
 Especifica que solo el primer registro que se encuentra con un valor de clave de índice determinado está incluido en un archivo .idx o una etiqueta .cdx. UNIQUE puede utilizarse para impedir la presentación de o el acceso a los registros duplicados. Se excluyen todos los registros agregados con claves de índice duplicadas del archivo de índice. Con la opción de índice única es idéntico al ejecutar SET UNIQUE ON antes de emitir el índice o REINDIZACIÓN.  
  
 Cuando un índice único o una etiqueta de índice está activa y se cambia un registro duplicado de una manera que cambie su clave de índice, se actualiza el índice o la etiqueta de índice. Sin embargo, el siguiente registro duplicado con la clave de índice original no está accesible o muestra hasta volver a indizar el archivo mediante REINDIZACIÓN.  
  
 CANDIDATO  
 Crea una etiqueta de índice estructural de candidato. Se puede incluir la palabra clave CANDIDATA sólo cuando se crea una etiqueta de índice estructural; de lo contrario, Visual FoxPro genera un mensaje de error.  
  
 Una etiqueta de índice candidato evita que los valores duplicados en el campo o la combinación de los campos especificados en la expresión del índice *eExpression*. El término *candidato* hace referencia al tipo de índice, ya que los índices candidatos impiden valores duplicados, se califican como "candidato" es un índice principal.  
  
 Visual FoxPro genera un error si se crea una etiqueta de índice candidato para un campo o una combinación de campos que ya contiene valores duplicados.  
  
 SUMA  
 Mantiene abre los archivos de índice abierto anteriormente. Si se omite la cláusula de suma cuando se crea un archivo de índice o los archivos de una tabla con índice, se cierran los archivos de índice abierto anteriormente (excepto el índice compuesto estructural).  
  
## <a name="remarks"></a>Comentarios  
 Registros de una tabla que tiene un archivo de índice se muestran y se obtiene acceso en el orden especificado por la expresión del índice. No se cambia el orden físico de los registros de la tabla mediante un archivo de índice.  
  
## <a name="index-types"></a>Tipos de índices  
 Visual FoxPro le permite crear dos tipos de archivos de índice:  
  
-   Archivos de índice .cdx que contiene varias entradas de índice que se denominan etiquetas compuestos  
  
-   archivos de índice .idx que contiene una entrada de índice  
  
 También puede crear un archivo de índice compuesto estructural, que se abre automáticamente con la tabla.  
  
> [!NOTE]  
>  Dado que los archivos de índice compuesto estructural se abren automáticamente cuando se abre la tabla, son el tipo de índice preferido.  
  
 Incluir compacto para crear archivos de índice de .idx compact. Archivos de índice compuesto siempre están compactos.  
  
## <a name="index-order-and-updating"></a>Orden del índice y actualizar  
 Solo un índice (el archivo índice maestro) o una etiqueta (la etiqueta principal) controla el orden en el que se muestra o se tiene acceso a la tabla. Ciertos comandos (por ejemplo, búsqueda) usan el archivo de índice maestro o la etiqueta para buscar registros. Sin embargo, todos los abiertos .idx y archivos de índice .cdx se actualizan cuando se realizan cambios en la tabla.  
  
## <a name="user-defined-functions"></a>Funciones definidas por el usuario  
 Aunque una expresión de índice puede contener una función definida por el usuario, no debe utilizar funciones definidas por el usuario en una expresión de índice. Funciones definidas por el usuario en una expresión de índice aumentan el tiempo necesario para crear o actualizar el índice. Además, las actualizaciones del índice no se pueden producir cuando se utiliza una función definida por el usuario para una expresión de índice.  
  
 Si utilizas una función definida por el usuario en una expresión de índice, Visual FoxPro debe ser capaz de encontrar la función definida por el usuario. Cuando Visual FoxPro crea un índice, la expresión del índice se guarda en el archivo de índice, pero solo una referencia a la función definida por el usuario se incluye en la expresión del índice.  
  
## <a name="see-also"></a>Vea también  
 [Modificar tabla - comando SQL](../../odbc/microsoft/alter-table-sql-command.md)   
 [Eliminar etiqueta, comando](../../odbc/microsoft/delete-tag-command.md)   
 [Comando COLLATE Set.](../../odbc/microsoft/set-collate-command.md)   
 [CONJUNTO único comando](../../odbc/microsoft/set-unique-command.md)

