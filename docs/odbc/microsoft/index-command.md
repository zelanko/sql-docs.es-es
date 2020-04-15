---
title: Comando INDEX (Comando INDEX) Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bcb30a49cb9f11ddd4c61621116aa4bd8ddcf186
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300035"
---
# <a name="index-command"></a>Comando de índice
Crea un archivo de índice para mostrar y tener acceso a los registros de tabla en un orden lógico.  
  
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
 Especifica una expresión de índice que puede incluir el nombre de un campo o campos de la tabla actual. Se crea una clave de índice basada en la expresión de índice en el archivo de índice para cada registro de la tabla. Visual FoxPro usa estas claves para mostrar y acceder a los registros de la tabla.  
  
> [!NOTE]  
>  Aunque no se recomienda, *eExpression* también puede ser una variable de memoria, un elemento de matriz o una expresión de campo o campo de una tabla de otro área de trabajo. Los campos de nota no se pueden utilizar solos en expresiones de archivo de índice; deben combinarse con otras expresiones de caracteres. Si tiene acceso a un índice que contiene una variable o campo que ya no existe o no se puede encontrar, Visual FoxPro genera un mensaje de error.  
  
 Si intenta crear un índice con una clave que varía en longitud, la clave se rellenará con espacios. Las claves de índice de longitud variable no se admiten en Visual FoxPro.  
  
 Es posible crear una clave de índice con longitud cero. Por ejemplo, se crea una clave de índice de longitud cero cuando la expresión de índice es una subcadena de un campo de nota vacío. Una clave de índice de longitud cero genera un mensaje de error. Cuando Visual FoxPro crea un índice, evalúa los campos del primer registro de la tabla. Si un campo está vacío, puede ser necesario introducir algunos datos temporales en el campo del primer registro para evitar una clave de índice de longitud 0.  
  
 A *IDXFileName*  
 Crea un archivo de índice .idx. El archivo de índice recibe la extensión predeterminada .idx.  
  
 TAG *TagName*[OF *CDXFileName*]  
 Crea un archivo de índice compuesto. Un archivo de índice compuesto es un único archivo de índice que consta de cualquier número de etiquetas independientes (entradas de índice). Cada etiqueta se identifica por su nombre de etiqueta único. Los nombres de etiqueta deben comenzar con una letra o un carácter de subrayado y pueden consistir en cualquier combinación de hasta 10 letras, dígitos o guiones bajos. El número de etiquetas en un archivo de índice compuesto está limitado únicamente por la memoria disponible y el espacio en disco.  
  
 Los archivos de índice compuesto de entrada múltiple siempre son compactos. No es necesario incluir COMPACT al crear un archivo de índice compuesto. Los nombres de los archivos de índice compuesto se les da una extensión .cdx.  
  
 Se pueden crear dos tipos de archivos de índice compuesto: estructurales y no estructurales.  
  
 **Archivos de índice de compuestos estructurales** Puede crear un archivo de índice compuesto estructural con TAG *TagName* excluyendo la cláusula opcional OF *CDXFileName.* Un archivo de índice compuesto estructural siempre tiene el mismo nombre base que la tabla y se abre automáticamente cuando se abre la tabla.  
  
 **Archivos** de índice compuesto no estructural Puede crear un archivo de índice compuesto no estructural incluyendo OF *CDXFileName* después de TAG *TagName*. A diferencia de un archivo de índice compuesto estructural, un archivo de índice compuesto no estructural debe abrirse explícitamente con la cláusula INDEX en USE.  
  
 Si ya se ha creado y abierto un archivo de índice compuesto, la emisión de INDEX con TAG *TagName* agrega una etiqueta al archivo de índice compuesto.  
  
 FOR *lExpression*  
 Especifica una condición por la que solo los registros que satisfacen la expresión de filtro *lExpression* están disponibles para su visualización y acceso; las claves de índice se crean en el archivo de índice solo para los registros que coinciden con la expresión de filtro.  
  
 La tecnología Visual FoxPro Rushmore optimiza un INDEX ... FOR *lExpression* si *lExpression* es una expresión optimizable. Para obtener el mejor rendimiento, utilice una expresión optimizable en la cláusula FOR.  
  
 Compacto  
 Crea un archivo .idx compacto.  
  
 Ascendente  
 Especifica un orden ascendente para el archivo .cdx. De forma predeterminada, las etiquetas .cdx se crean en orden ascendente. (Puede incluir ASCENDING como recordatorio del orden del archivo de índice.) Una tabla se puede indizar en orden inverso incluyendo DESCENDING.  
  
 Descendente  
 Especifica un orden descendente para el archivo .cdx. No se puede incluir DESCENDING al crear archivos de índice .idx.  
  
 UNIQUE  
 Especifica que solo el primer registro encontrado con un valor de clave de índice determinado se incluye en un archivo .idx o una etiqueta .cdx. UNIQUE se puede utilizar para impedir la visualización o el acceso a registros duplicados. Todos los registros agregados con claves de índice duplicadas se excluyen del archivo de índice. El uso de la opción UNIQUE de INDEX es idéntico a ejecutar SET UNIQUE ON antes de emitir INDEX o REINDEX.  
  
 Cuando una etiqueta de índice o índice UNIQUE está activa y un registro duplicado se cambia de una manera que cambia su clave de índice, se actualiza la etiqueta de índice o índice. Sin embargo, no se puede acceder ni mostrar el siguiente registro duplicado con la clave de índice original hasta que vuelva a indexar el archivo mediante REINDEX.  
  
 Candidato  
 Crea una etiqueta de índice estructural candidata. La palabra clave CANDIDATE solo se puede incluir al crear una etiqueta de índice estructural; de lo contrario, Visual FoxPro genera un mensaje de error.  
  
 Una etiqueta de índice candidata impide valores duplicados en el campo o la combinación de campos especificados en la expresión de índice *eExpression*. El término *candidato* hace referencia al tipo de índice; debido a que los índices candidatos impiden valores duplicados, califican como "candidatos" para ser un índice principal.  
  
 Visual FoxPro genera un error si crea una etiqueta de índice candidata para un campo o una combinación de campos que ya contiene valores duplicados.  
  
 Aditivo  
 Mantiene abiertos los archivos de índice abiertos anteriormente. Si omite la cláusula ADDITIVE al crear un archivo de índice o archivos para una tabla con INDEX, se cierran los archivos de índice abiertos anteriormente (excepto el índice compuesto estructural).  
  
## <a name="remarks"></a>Observaciones  
 Los registros de una tabla que tiene un archivo de índice se muestran y se tiene acceso a ellos en el orden especificado por la expresión de índice. Un archivo de índice no cambia el orden físico de los registros de la tabla.  
  
## <a name="index-types"></a>Tipos de índice  
 Visual FoxPro le permite crear dos tipos de archivos de índice:  
  
-   Archivos de índice .cdx compuestos que contienen varias entradas de índice llamadas etiquetas  
  
-   Archivos de índice .idx que contienen una entrada de índice  
  
 También puede crear un archivo de índice compuesto estructural, que se abre automáticamente con la tabla.  
  
> [!NOTE]  
>  Dado que los archivos de índice compuesto estructural se abren automáticamente cuando se abre la tabla, son el tipo de índice preferido.  
  
 Incluya COMPACT para crear archivos de índice .idx compactos. Los archivos de índice compuestos siempre son compactos.  
  
## <a name="index-order-and-updating"></a>Orden y actualización del índice  
 Solo un archivo de índice (el archivo de índice maestro) o una etiqueta (la etiqueta maestra) controla el orden en que se muestra o se accede a la tabla. Ciertos comandos (SEEK, por ejemplo) utilizan el archivo de índice maestro o la etiqueta para buscar registros. Sin embargo, todos los archivos de índice .idx y .cdx abiertos se actualizan a medida que se realizan cambios en la tabla.  
  
## <a name="user-defined-functions"></a>Funciones definidas por el usuario  
 Aunque una expresión de índice puede contener una función definida por el usuario, no debe utilizar funciones definidas por el usuario en una expresión de índice. Las funciones definidas por el usuario en una expresión de índice aumentan el tiempo que se tarda en crear o actualizar el índice. Además, es posible que las actualizaciones de índice no se produzcan cuando se utiliza una función definida por el usuario para una expresión de índice.  
  
 Si utiliza una función definida por el usuario en una expresión de índice, Visual FoxPro debe poder localizar la función definida por el usuario. Cuando Visual FoxPro crea un índice, la expresión de índice se guarda en el archivo de índice, pero solo se incluye una referencia a la función definida por el usuario en la expresión de índice.  
  
## <a name="see-also"></a>Consulte también  
 [ALTER TABLE - Comando SQL](../../odbc/microsoft/alter-table-sql-command.md)   
 [COMANDO DELETE TAG](../../odbc/microsoft/delete-tag-command.md)   
 [Comando SET COLLATE](../../odbc/microsoft/set-collate-command.md)   
 [CONJUNTO único comando](../../odbc/microsoft/set-unique-command.md)
