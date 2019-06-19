---
title: Modificar tabla - comando SQL | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- alter table [ODBC]
ms.assetid: 3a01a291-f4d9-43bc-a725-5a95546ff364
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5f656396455a8d5669debc158c3edc866491fcb5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63457629"
---
# <a name="alter-table---sql-command"></a>Modificar tabla - comando SQL
Modifica mediante programación la estructura de una tabla.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
ALTER TABLE TableName1  
   ADD | ALTER [COLUMN] FieldName1  
      FieldType [(nFieldWidth [, nPrecision])]  
      [NULL | NOT NULL]  
      [CHECK lExpression1 [ERROR cMessageText1]]  
      [DEFAULT eExpression1]  
      [PRIMARY KEY | UNIQUE]  
      [REFERENCES TableName2 [TAG TagName1]]  
      [NOCPTRANS]  
 - Or -  
ALTER TABLE TableName1  
   ALTER [COLUMN] FieldName2  
      [NULL | NOT NULL]  
      [SET DEFAULT eExpression2]  
      [SET CHECK lExpression2 [ERROR cMessageText2]]  
      [DROP DEFAULT]  
      [DROP CHECK]  
 - Or -  
ALTER TABLE TableName1  
   [DROP [COLUMN] FieldName3]  
   [SET CHECK lExpression3 [ERROR cMessageText3]]  
   [DROP CHECK]  
   [ADD PRIMARY KEY eExpression3 TAG TagName2]  
   [DROP PRIMARY KEY]  
   [ADD UNIQUE eExpression4 [TAG TagName3]]  
   [DROP UNIQUE TAG TagName4]  
   [ADD FOREIGN KEY [eExpression5] TAG TagName4  
      REFERENCES TableName2 [TAG TagName5]]  
   [DROP FOREIGN KEY TAG TagName6 [SAVE]]  
   [RENAME COLUMN FieldName4 TO FieldName5]  
   [NOVALIDATE]  
```  
  
## <a name="arguments"></a>Argumentos  
 *TableName1*  
 Especifica el nombre de la tabla cuya estructura se modifica.  
  
 Agregar [columna] *Nombredecampo1*  
 Especifica el nombre del campo que desea agregar.  
  
 ALTER [columna] *Nombredecampo1*  
 Especifica el nombre de un campo existente para modificar.  
  
 *FieldType* [( *nFieldWidth* [, *nPrecision*]])  
 Especifica el tipo de campo, el ancho de campo y la precisión (número de posiciones decimales) del campo para un campo nuevo o modificado.  
  
 *FieldType* es una letra única que indica el campo [tipo de datos](../../odbc/microsoft/visual-foxpro-field-data-types.md). Algunos tipos de campo de datos requieren que se especifique *nFieldWidth* o *nPrecision* o ambos.  
  
 *nFieldWidth* y *nPrecision* se omiten para D, G, I, L, M, P, T y Y tipos. De forma predeterminada, *nPrecision* no es cero (decimales) si *nPrecision* no se incluye para los tipos de B, F o N.  
  
 NULL &#124; NOT NULL  
 Permite o impide que los valores null en el campo.  
  
 Si omite NULL y NOT NULL, el valor actual de SET NULL determina si se permiten valores null en el campo. Sin embargo, si omite NULL y NOT NULL e incluye la clave principal o única cláusula, se omite el valor actual de SET NULL y el campo no es NULL de manera predeterminada.  
  
 CHECK *lExpression1*  
 Especifica una regla de validación para el campo. *lExpression1* debe evaluarse como una expresión lógica y puede ser una función definida por el usuario o un procedimiento almacenado. Siempre que se anexa un registro en blanco, se comprueba la regla de validación. Se genera un error si la regla de validación no se permite un valor de campo en blanco en un registro anexado.  
  
 ERROR *cMessageText1*  
 Especifica el mensaje de error aparece cuando la regla de validación de campo genera un error.  
  
 DEFAULT *eExpression1*  
 Especifica un valor predeterminado para el campo. Tipo de datos de *eExpression1* debe ser el mismo que el tipo de datos para el campo.  
  
 PRIMARY KEY  
 Crea una etiqueta de índice principal. La etiqueta de índice tiene el mismo nombre que el campo.  
  
 UNIQUE  
 Crea una etiqueta de índice candidato con el mismo nombre que el campo.  
  
> [!NOTE]  
>  Candidato difieren de los índices (creados mediante la inclusión de la opción única, proporcionada para la compatibilidad con ANSI en ALTER TABLE o CREATE TABLE) de los índices creados mediante el uso de la opción única en el comando de índice. Un índice creado mediante el uso de UNIQUE en el comando de índice permite que las claves de índice duplicados; los índices de candidato no permiten las claves de índice duplicados.  
  
 No se permiten valores NULL y los registros duplicados en un campo que se usa para un índice principales ni candidatas.  
  
 Si va a crear un nuevo campo mediante el uso de Agregar columna, Visual FoxPro no generará un error si se crea un índice principales ni candidatas para un campo que admita valores null. Sin embargo, Visual FoxPro generará un error si se intenta escribir un valor nulo o duplicado en un campo que se usa para un índice principales ni candidatas.  
  
 Si va a modificar un campo existente y la réplica principal o la expresión de índice candidato se compone de campos en la tabla, Visual FoxPro comprueba los campos para ver si contienen valores null o los registros duplicados. Si es así, Visual FoxPro genera un error y no se modifica la tabla.  
  
 REFERENCIAS *TableName2* etiqueta *TagName1*  
 Especifica la tabla primaria a la que se establece una relación persistente. Etiqueta *TagName1* especifica la etiqueta de índice de la tabla primaria en el que se basa la relación. Los nombres de etiqueta de índice pueden contener hasta 10 caracteres.  
  
 NOCPTRANS  
 Impide la traducción a una página de códigos diferentes para los campos de carácter y memorando. Si la tabla se convierte en otra página de códigos, no se traducen los campos para el que se ha especificado NOCPTRANS. NOCPTRANS puede especificarse solamente para campos de carácter y memorando.  
  
 El ejemplo siguiente crea una tabla denominada mytable que contiene dos campos de carácter y dos campos de interés. El segundo campo de carácter, char2 y el segundo campo Memorando, memo2, incluyen NOCPTRANS para evitar la traducción.  
  
```  
CREATE TABLE mytable (char1 C(10), char2 C(10) NOCPTRANS,;  
   memo1 M, memo2 M NOCPTRANS)  
```  
  
 ALTER [columna] *Nombredecampo2*  
 Especifica el nombre de un campo existente para modificar.  
  
 SET DEFAULT *eExpression2*  
 Especifica un nuevo valor predeterminado para un campo existente. Tipo de datos de *eExpression2* debe ser el mismo que el tipo de datos para el campo.  
  
 SET CHECK *lExpression2*  
 Especifica una nueva regla de validación para un campo existente. *lExpression2* debe evaluarse como una expresión lógica y puede ser una función definida por el usuario o un procedimiento almacenado.  
  
 ERROR *cMessageText2*  
 Especifica el mensaje de error aparece cuando la regla de validación de campo genera un error. El mensaje se muestra solo cuando se cambian los datos dentro de una ventana Examinar o modificar.  
  
 DROP DEFAULT  
 Quita el valor predeterminado para un campo existente.  
  
 COMPROBACIÓN DE COLOCACIÓN  
 Quita la regla de validación para un campo existente.  
  
 DROP [COLUMN] *FieldName3*  
 Especifica un campo para quitar de la tabla. Quitar un campo de la tabla también quita la regla de validación de campo y de configuración del valor predeterminado del campo.  
  
 Si las expresiones de índice de clave o un desencadenador, haga referencia al campo, las expresiones dejan de ser válidas cuando se quita el campo. En este caso, no se genera un error cuando se quita el campo, pero las expresiones de índice no válido de clave o el desencadenador generará errores en tiempo de ejecución.  
  
 SET CHECK *lExpression3*  
 Especifica la regla de validación de la tabla. *lExpression3* debe evaluarse como una expresión lógica y puede ser una función definida por el usuario o un procedimiento almacenado.  
  
 ERROR *cMessageText3*  
 Especifica el mensaje de error aparece cuando la regla de validación de la tabla genera un error. El mensaje se muestra solo cuando se cambian los datos dentro de una ventana Examinar o modificar.  
  
 COMPROBACIÓN DE COLOCACIÓN  
 Quita la regla de validación de la tabla.  
  
 CLAVE principal de agregar *eExpression3*etiqueta *TagName2*  
 Agrega un índice principal a la tabla. *eExpression3* especifica la expresión de clave de índice principal y *TagName2* especifica el nombre de la etiqueta de índice principal. Los nombres de etiqueta de índice pueden contener hasta 10 caracteres. Si etiqueta *TagName2* se omite y *eExpression3* es un campo único, la etiqueta de índice principal tiene el mismo nombre que el campo especificado en *eExpression3*.  
  
 QUITAR CLAVE PRINCIPAL  
 Quita el índice principal y su etiqueta de índice. Dado que una tabla puede tener sólo una clave principal, no es necesario especificar el nombre de la clave principal. Quitar el índice principal, también elimina las relaciones persistentes en función de la clave principal.  
  
 Agregar UNIQUE *eExpression4*[etiqueta *TagName3*]  
 Agrega un índice de candidato a la tabla. *eExpression4* especifica la expresión de clave de índice de candidato, y *TagName3* especifica el nombre de la etiqueta de índice candidato. Los nombres de etiqueta de índice pueden contener hasta 10 caracteres. Si se omite la etiqueta *TagName3* y si *eExpression4* es un campo único, la etiqueta de índice candidato tiene el mismo nombre que el campo especificado en *eExpression4*.  
  
 COLOCACIÓN de etiqueta único *TagName4*  
 Quita el índice del candidato y su etiqueta de índice. Dado que una tabla puede tener varias claves candidatas, debe especificar el nombre de la etiqueta de índice del candidato.  
  
 Agregar clave externa [ *eExpression5*] etiqueta *TagName4*  
 Agrega un índice (no principal) externo a la tabla. *eExpression5* especifica la expresión de clave externa de índice, y *TagName4* especifica el nombre de la etiqueta externa del índice. Los nombres de etiqueta de índice pueden contener hasta 10 caracteres.  
  
 REFERENCIAS *TableName2*[etiqueta *TagName5*]  
 Especifica la tabla primaria a la que se establece una relación persistente. Incluir etiqueta *TagName5* para establecer una relación basada en una etiqueta de índice existente para la tabla primaria. Los nombres de etiqueta de índice pueden contener hasta 10 caracteres. Si se omite la etiqueta *TagName5*, la relación se establece mediante la etiqueta de índice principal de la tabla primaria.  
  
 COLOCAR etiquetas de clave externa *TagName6*[Guardar]  
 Elimina una clave externa es cuya etiqueta índice *TagName6*. Si se omite, guardar, se elimina la etiqueta de índice desde el índice estructural. Incluir Guardar para impedir la eliminación de la etiqueta de índice desde el índice estructural.  
  
 COLUMNA de cambio de nombre *FieldName4*TO *FieldName5*  
 Permite cambiar el nombre de un campo en la tabla. *FieldName4* especifica el nombre del campo que se cambia el nombre. *FieldName5* especifica el nuevo nombre del campo.  
  
> [!CAUTION]  
>  Tener cuidado al cambiar el nombre de campos de tabla porque las expresiones de índice, las reglas de validación de campo y la tabla, los comandos y las funciones pueden hacer referencia a los nombres de campo original.  
  
 NOVALIDATE  
 Especifica que Visual FoxPro permite que se realicen cambios en la estructura de la tabla. estos cambios podrían dañar la integridad de los datos en la tabla. De forma predeterminada, Visual FoxPro evita que realicen los cambios que infrinjan la integridad de los datos en la tabla ALTER TABLE. Incluir NOVALIDATE para invalidar este comportamiento predeterminado.  
  
## <a name="remarks"></a>Comentarios  
 ALTER TABLE puede utilizarse para modificar la estructura de una tabla que no se ha agregado a una base de datos. Sin embargo, Visual FoxPro genera un error si incluyen el predeterminado, FOREIGN KEY, PRIMARY KEY, referencias o establecer cláusulas cuando se modifica una tabla libre.  
  
 ALTER TABLE puede volver a generar la tabla mediante la creación de un nuevo encabezado de tabla y anexar los registros para el encabezado de tabla. Por ejemplo, cambiar el tipo o el ancho de un campo podría hacer que la tabla se vuelvan a generar.  
  
 Una vez que se vuelve a generar una tabla, se ejecutan las reglas de validación de campo para todos los campos cuyo tipo o el ancho se cambian. Si cambia el tipo o el ancho de un campo en la tabla, se ejecuta la regla de la tabla.  
  
 Si modifica las reglas de validación de campo o una tabla para una tabla que contenga los registros, Visual FoxPro comprueba las reglas de validación de campo o una tabla nueva con datos existentes y emite una advertencia en la primera aparición de una regla de validación de campo o una tabla o de una infracción de desencadenador.  
  
 Si la tabla que se modifica en una base de datos, ALTER TABLE - SQL requiere el uso exclusivo de la base de datos. Para abrir una base de datos para uso exclusivo, incluir exclusivo en Abrir base de datos.  
  
## <a name="see-also"></a>Vea también  
 [Crear tabla - comando SQL](../../odbc/microsoft/create-table-sql-command.md)   
 [Comando de índice](../../odbc/microsoft/index-command.md)
