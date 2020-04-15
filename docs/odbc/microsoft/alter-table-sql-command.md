---
title: ALTER TABLE - Comando SQL ? Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 587d721522503f9b392bb8be7433850fd7449efb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304716"
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
 *NombreDeTabla1*  
 Especifica el nombre de la tabla cuya estructura se modifica.  
  
 ADD [COLUMN] *NombreDeCampo1*  
 Especifica el nombre del campo que se va a agregar.  
  
 ALTER [COLUMN] *NombreDeCampo1*  
 Especifica el nombre de un campo existente que se va a modificar.  
  
 *Tipo de campo* [( *nFieldWidth* [, *nPrecision*]])  
 Especifica el tipo de campo, el ancho del campo y la precisión del campo (número de decimales) para un campo nuevo o modificado.  
  
 *FieldType* es una sola letra que indica el tipo de [datos](../../odbc/microsoft/visual-foxpro-field-data-types.md)del campo. Algunos tipos de datos de campo requieren que especifique *nFieldWidth* o *nPrecision* o ambos.  
  
 *nFieldWidth* y *nPrecision* se omiten para los tipos D, G, I, L, M, P, T e Y. De forma predeterminada, *nPrecision* es cero (sin decimales) si *nPrecision* no se incluye para los tipos B, F o N.  
  
 NULL &#124; NOT NULL  
 Permite o impide valores nulos en el campo.  
  
 Si omite NULL y NOT NULL, el valor actual de SET NULL determina si se permiten valores NULL en el campo. Sin embargo, si omite NULL y NOT NULL e incluye la cláusula PRIMARY KEY o UNIQUE, se omite el valor actual de SET NULL y el campo NO es NULL de forma predeterminada.  
  
 CHECK *lExpression1*  
 Especifica una regla de validación para el campo. *lExpression1* debe evaluarse como una expresión lógica y puede ser una función definida por el usuario o un procedimiento almacenado. Cada vez que se anexa un registro en blanco, se comprueba la regla de validación. Se genera un error si la regla de validación no permite un valor de campo en blanco en un registro anexado.  
  
 ERROR *cMessageText1*  
 Especifica el mensaje de error que se muestra cuando la regla de validación de campos genera un error.  
  
 DEFAULT *eExpression1*  
 Especifica un valor predeterminado para el campo. El tipo de datos de *eExpression1* debe ser el mismo que el tipo de datos del campo.  
  
 PRIMARY KEY  
 Crea una etiqueta de índice principal. La etiqueta de índice tiene el mismo nombre que el campo.  
  
 UNIQUE  
 Crea una etiqueta de índice candidata con el mismo nombre que el campo.  
  
> [!NOTE]  
>  Los índices candidatos (creados mediante la inclusión de la opción UNIQUE, proporcionada para la compatibilidad ANSI en ALTER TABLE o CREATE TABLE) difieren de los índices creados mediante la opción UNIQUE en el comando INDEX. Un índice creado mediante UNIQUE en el comando INDEX permite claves de índice duplicadas; los índices candidatos no permiten claves de índice duplicadas.  
  
 Los valores nulos y los registros duplicados no se permiten en un campo que se utiliza para un índice principal o candidato.  
  
 Si va a crear un nuevo campo mediante ADD COLUMN, Visual FoxPro no generará un error si crea un índice principal o candidato para un campo que admite valores nulos. Sin embargo, Visual FoxPro generará un error si intenta escribir un valor nulo o duplicado en un campo que se usa para un índice principal o candidato.  
  
 Si está modificando un campo existente y la expresión de índice principal o candidato consta de campos en la tabla, Visual FoxPro comprueba los campos para ver si contienen valores nulos o registros duplicados. Si lo hacen, Visual FoxPro genera un error y la tabla no se modifica.  
  
 REFERENCIAS *TableName2* TAG *TagName1*  
 Especifica la tabla primaria en la que se establece una relación persistente. TAG *TagName1* especifica la etiqueta de índice de la tabla primaria en la que se basa la relación. Los nombres de etiqueta de índice pueden contener hasta 10 caracteres.  
  
 NOCPTRANS  
 Impide la traducción a una página de códigos diferente para los campos de caracteres y notas. Si la tabla se convierte en otra página de códigos, los campos para los que se ha especificado NOCPTRANS no se traducen. NOCPTRANS solo se puede especificar para los campos de caracteres y notas.  
  
 En el ejemplo siguiente se crea una tabla denominada mytable que contiene dos campos de caracteres y dos campos de nota. El segundo campo de carácter, char2, y el segundo campo de nota, memo2, incluyen NOCPTRANS para evitar la traducción.  
  
```  
CREATE TABLE mytable (char1 C(10), char2 C(10) NOCPTRANS,;  
   memo1 M, memo2 M NOCPTRANS)  
```  
  
 ALTER [COLUMN] *NombreDeCampo2*  
 Especifica el nombre de un campo existente que se va a modificar.  
  
 SET DEFAULT *eExpression2*  
 Especifica un nuevo valor predeterminado para un campo existente. El tipo de datos de *eExpression2* debe ser el mismo que el tipo de datos del campo.  
  
 SET CHECK *lExpression2*  
 Especifica una nueva regla de validación para un campo existente. *lExpression2* debe evaluarse como una expresión lógica y puede ser una función definida por el usuario o un procedimiento almacenado.  
  
 ERROR *cMessageText2*  
 Especifica el mensaje de error que se muestra cuando la regla de validación de campos genera un error. El mensaje solo se muestra cuando se cambian los datos en una ventana Examinar o Editar.  
  
 DROP DEFAULT  
 Quita el valor predeterminado de un campo existente.  
  
 DROP CHECK  
 Quita la regla de validación de un campo existente.  
  
 DROP [COLUMN] *NombreDeCampo3*  
 Especifica un campo que se va a quitar de la tabla. Al quitar un campo de la tabla también se quita la configuración de valor predeterminada del campo y la regla de validación de campos.  
  
 Si las expresiones de clave de índice o desencadenador hacen referencia al campo, las expresiones pasan a ser válidas cuando se quita el campo. En este caso, no se genera un error cuando se quita el campo, pero la clave de índice no válida o las expresiones de desencadenador generarán errores en tiempo de ejecución.  
  
 SET CHECK *lExpression3*  
 Especifica la regla de validación de tabla. *lExpression3* debe evaluarse como una expresión lógica y puede ser una función definida por el usuario o un procedimiento almacenado.  
  
 ERROR *cMessageText3*  
 Especifica el mensaje de error que se muestra cuando la regla de validación de tabla genera un error. El mensaje solo se muestra cuando se cambian los datos en una ventana Examinar o Editar.  
  
 DROP CHECK  
 Quita la regla de validación de la tabla.  
  
 AGREGAR PRIMARY KEY *eExpression3*TAG *TagName2*  
 Agrega un índice principal a la tabla. *eExpression3* especifica la expresión de clave de índice principal y *TagName2* especifica el nombre de la etiqueta de índice principal. Los nombres de etiqueta de índice pueden contener hasta 10 caracteres. Si se omite TAG *TagName2* y *eExpression3* es un solo campo, la etiqueta de índice principal tiene el mismo nombre que el campo especificado en *eExpression3*.  
  
 DROP PRIMARY KEY  
 Quita el índice principal y su etiqueta de índice. Dado que una tabla solo puede tener una clave principal, no es necesario especificar el nombre de la clave principal. La eliminación del índice principal también elimina las relaciones persistentes basadas en la clave principal.  
  
 ADD UNIQUE *eExpression4*[TAG *TagName3*]  
 Agrega un índice candidato a la tabla. *eExpression4* especifica la expresión de clave de índice candidata y *TagName3* especifica el nombre de la etiqueta de índice candidata. Los nombres de etiqueta de índice pueden contener hasta 10 caracteres. Si omite TAG *TagName3* y *eExpression4* es un campo único, la etiqueta de índice candidata tiene el mismo nombre que el campo especificado en *eExpression4*.  
  
 DROP UNIQUE TAG *TagName4*  
 Quita el índice candidato y su etiqueta de índice. Dado que una tabla puede tener varias claves candidatas, debe especificar el nombre de la etiqueta de índice candidata.  
  
 ADD FOREIGN KEY [ *eExpression5*]TAG *TagName4*  
 Agrega un índice externo (no primario) a la tabla. *eExpression5* especifica la expresión de clave de índice externa y *TagName4* especifica el nombre de la etiqueta de índice externa. Los nombres de etiqueta de índice pueden contener hasta 10 caracteres.  
  
 REFERENCIAS *NombreDeTabla2*[TAG *TagName5*]  
 Especifica la tabla primaria en la que se establece una relación persistente. Incluya TAG *TagName5* para establecer una relación basada en una etiqueta de índice existente para la tabla primaria. Los nombres de etiqueta de índice pueden contener hasta 10 caracteres. Si omite TAG *TagName5*, la relación se establece mediante la etiqueta de índice principal de la tabla primaria.  
  
 DROP FOREIGN KEY TAG *TagName6*[SAVE]  
 Elimina una clave externa cuya etiqueta de índice es *TagName6*. Si omite SAVE, la etiqueta de índice se elimina del índice estructural. Incluya SAVE para evitar la eliminación de la etiqueta de índice del índice estructural.  
  
 RENAME COLUMN *FieldName4*A *FieldName5*  
 Le permite cambiar el nombre de un campo de la tabla. *FieldName4* especifica el nombre del campo al que se cambia el nombre. *FieldName5* especifica el nuevo nombre del campo.  
  
> [!CAUTION]  
>  Tenga cuidado al cambiar el nombre de los campos de tabla porque las expresiones de índice, las reglas de validación de campos y tablas, los comandos y las funciones pueden hacer referencia a los nombres de campo originales.  
  
 NOVALIDATE  
 Especifica que Visual FoxPro permite realizar cambios en la estructura de la tabla; estos cambios podrían infringir la integridad de los datos de la tabla. De forma predeterminada, Visual FoxPro impide que ALTER TABLE realice cambios que infrinjan la integridad de los datos de la tabla. Incluya NOVALIDATE para invalidar este comportamiento predeterminado.  
  
## <a name="remarks"></a>Observaciones  
 ALTER TABLE se puede utilizar para modificar la estructura de una tabla que no se ha agregado a una base de datos. Sin embargo, Visual FoxPro genera un error si incluye las cláusulas DEFAULT, FOREIGN KEY, PRIMARY KEY, REFERENCES o SET al modificar una tabla libre.  
  
 ALTER TABLE puede reconstruir la tabla creando un nuevo encabezado de tabla y anexando registros al encabezado de tabla. Por ejemplo, cambiar el tipo o el ancho de un campo puede hacer que se vuelva a generar la tabla.  
  
 Después de volver a generar una tabla, se ejecutan reglas de validación de campos para cualquier campo cuyo tipo o ancho cambie. Si cambia el tipo o el ancho de cualquier campo de la tabla, se ejecuta la regla de tabla.  
  
 Si modifica las reglas de validación de campos o tablas para una tabla que tiene registros, Visual FoxPro prueba las nuevas reglas de validación de campos o tablas con los datos existentes y emite una advertencia en la primera aparición de una regla de validación de campo o tabla o de una infracción de desencadenador.  
  
 Si la tabla que modifica está en una base de datos, ALTER TABLE - SQL requiere el uso exclusivo de la base de datos. Para abrir una base de datos de uso exclusivo, incluya EXCLUSIVA en OPEN DATABASE.  
  
## <a name="see-also"></a>Consulte también  
 [CREATE TABLE - Comando SQL](../../odbc/microsoft/create-table-sql-command.md)   
 [Comando de índice](../../odbc/microsoft/index-command.md)
