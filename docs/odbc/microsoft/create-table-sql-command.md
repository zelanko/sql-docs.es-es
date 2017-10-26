---
title: Crear tabla - comando SQL | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- CREATE TABLE [ODBC]
ms.assetid: be2143ba-fc16-42c9-84f7-8985cd924860
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 35a22420b5ecaf21539fd16aecb3870e3f3049dc
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="create-table---sql-command"></a>Crear tabla - comando SQL
Crea una tabla que tiene los campos especificados.  
  
 El controlador ODBC de Visual FoxPro admite la sintaxis del lenguaje Visual FoxPro nativo para este comando. Para obtener información específica del controlador, consulte **controlador comentarios**.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
CREATE TABLE | DBF TableName1 [NAME LongTableName] [FREE]  
   (FieldName1FieldType [(nFieldWidth [, nPrecision])]  
      [NULL | NOT NULL]   
      [CHECK lExpression1 [ERROR cMessageText1]]  
      [DEFAULT eExpression1]  
      [PRIMARY KEY | UNIQUE]  
      [REFERENCES TableName2 [TAG TagName1]]  
      [NOCPTRANS]  
   [, FieldName2 ...]  
      [, PRIMARY KEY eExpression2 TAG TagName2  
      |, UNIQUE eExpression3 TAG TagName3]  
      [, FOREIGN KEY eExpression4 TAG TagName4 [NODUP]  
            REFERENCES TableName3 [TAG TagName5]]  
      [, CHECK lExpression2 [ERROR cMessageText2]])  
| FROM ARRAY ArrayName  
```  
  
## <a name="arguments"></a>Argumentos  
 Crear tabla &#124; DBF *TableName1*  
 Especifica el nombre de la tabla que se va a crear. Las opciones de tabla y DBF son idénticas.  
  
 NOMBRE *LongTableName*  
 Especifica un nombre largo de la tabla. Puede especificarse un nombre de tabla larga sólo cuando una base de datos está abierta, ya que los nombres de tabla largos se almacenan en bases de datos.  
  
 Los nombres largos pueden contener hasta 128 caracteres y pueden usarse en lugar de nombres cortos de archivo en la base de datos.  
  
 GRATUITO  
 Especifica que la tabla no se agregarán a una base de datos abierta. LIBRE no es necesario si una base de datos no está abierto.  
  
 *(Nombredecampo1 FieldType* [( *nFieldWidth* [, *nPrecision*])]  
 Especifica el nombre del campo, el tipo de campo, el ancho de campo y la precisión del campo (número de posiciones decimales), respectivamente.  
  
 *FieldType* es una letra única que indica el campo [tipo de datos](../../odbc/microsoft/visual-foxpro-field-data-types.md). Algunos tipos de datos de campo requieren que se especifiquen *nFieldWidth* o *nPrecision* o ambos.  
  
 *nFieldWidth* y *nPrecision* se omiten para D, G, I, L, M, P, T y Y tipos. *nPrecision* valor predeterminado es cero (sin decimales) si *nPrecision* no se incluye para los tipos de B, F o N.  
  
 NULL  
 Permite valores null en el campo.  
  
 NOT NULL  
 Impide que los valores null en el campo.  
  
 Si omite NULL y NOT NULL, el valor actual de SET NULL determina si se permiten valores null en el campo. Sin embargo, si omite NULL y NOT NULL e incluye la clave principal o única cláusula, se omite el valor actual de SET NULL y el campo predeterminado es NOT NULL.  
  
 COMPROBAR *lExpression1*  
 Especifica una regla de validación para el campo. *lExpression1* puede ser una función definida por el usuario. Cada vez que se anexa un registro en blanco, se comprueba la regla de validación. Se genera un error si no permite que la regla de validación de un valor de campo en blanco en un registro anexado.  
  
 ERROR *cMessageText1*  
 Especifica el mensaje de error de Visual FoxPro muestra cuando la regla de campo genera un error. El mensaje se muestra solo cuando se modifican datos en una ventana del explorador o una ventana de edición.  
  
 PREDETERMINADO *eExpression1*  
 Especifica un valor predeterminado para el campo. Tipo de datos de *eExpression1* debe coincidir con el tipo de datos del campo.  
  
 PRIMARY KEY  
 Crea un índice principal para el campo. La etiqueta de índice principal tiene el mismo nombre que el campo.  
  
 UNIQUE  
 Crea un índice de candidato para el campo. La etiqueta de índice candidato tiene el mismo nombre que el campo.  
  
> [!NOTE]  
>  Candidato índices (creados mediante la inclusión de la opción única en CREATE TABLE o ALTER TABLE - SQL) no son los mismos que los índices creados con la opción en el comando de índice única. Un índice creado con la opción en el comando de índice única permite a las claves de índice duplicados; índices candidatos no permiten que las claves de índice duplicadas. Vea [índice](../../odbc/microsoft/index-command.md) para obtener más información sobre su única opción.  
  
 No se permiten valores NULL y los registros duplicados en un campo que se usa para un índice principales ni candidatas. Sin embargo, Visual FoxPro no generará un error si se crea un índice principales ni candidatas para un campo que admite valores null. Visual FoxPro generará un error si se intenta escribir un valor nulo o duplicado en un campo que se usa para un índice principales ni candidatas.  
  
 REFERENCIAS *TableName2*[etiqueta *TagName1*]  
 Especifica la tabla primaria a la que se establece una relación persistente. Si se omite la etiqueta *TagName1*, la relación se establece mediante la clave de índice principal de la tabla primaria. Si la tabla primaria no tiene un índice principal, Visual FoxPro genera un error.  
  
 Include (etiqueta) *TagName1* para establecer una relación basada en una etiqueta de índice existente para la tabla primaria. Los nombres de etiqueta de índice pueden contener hasta 10 caracteres.  
  
 La tabla primaria no puede ser una tabla libre.  
  
 NOCPTRANS  
 Evita la conversión a una página de códigos diferentes para los campos de carácter y memorando. Si la tabla se convierte en otra página de códigos, no se convierten los campos para los que se ha especificado NOCPTRANS. NOCPTRANS puede especificarse únicamente para los campos de carácter y memorando.  
  
 En el ejemplo siguiente se crea una tabla denominada mytable que contiene dos campos de caracteres y los dos campos de memorando. El segundo campo de carácter, char2 y el segundo campo de memorando, memo2, incluir NOCPTRANS para evitar la traducción.  
  
```  
CREATE TABLE mytable (char1 C(10), char2 C(10) NOCPTRANS,;  
   memo1 M, memo2 M NOCPTRANS)  
```  
  
 CLAVE principal *eExpression2* etiqueta *TagName2*  
 Especifica un índice principal para crear. *eExpression2* especifica cualquier campo o una combinación de campos de la tabla. Etiqueta *TagName2 s*especifica el nombre de la etiqueta de índice principal que se crea. Los nombres de etiqueta de índice pueden contener hasta 10 caracteres.  
  
 Dado que una tabla puede tener un único índice principal, no puede incluir esta cláusula si ya ha creado un índice principal para un campo. Visual FoxPro genera un error si incluye más de una cláusula de clave principal en CREATE TABLE.  
  
 ÚNICO *eExpression3*etiqueta *TagName3*  
 Crea un índice de candidato. *eExpression3* especifica cualquier campo o una combinación de campos de la tabla. Sin embargo, si ha creado un índice principal con una de las opciones de clave principal, no puede incluir el campo que se especificó para el índice principal. Etiqueta *TagName3 s*especifica un nombre de etiqueta para la etiqueta de índice de candidato que se crea. Los nombres de etiqueta de índice pueden contener hasta 10 caracteres.  
  
 Una tabla puede tener varios índices candidatos.  
  
 CLAVE externa *eExpression4*etiqueta *TagName4*[NODUP]  
 Crea un índice (no principal) externo y establece una relación a una tabla primaria. *eExpression4* especifica la expresión de clave de índice externa, y *TagName4* especifica el nombre de la etiqueta de clave de índice externa que se crea*.* Los nombres de etiqueta de índice pueden contener hasta 10 caracteres. Incluir NODUP para crear un índice externa del candidato.  
  
 Puede crear varios índices externos para la tabla, pero las expresiones de índice externa deben especificar distintos campos en la tabla.  
  
 REFERENCIAS *TableName3*[etiqueta *TagName5*]  
 Especifica la tabla primaria a la que se establece una relación persistente. Include (etiqueta) *TagName5* para establecer una relación basada en una etiqueta de índice para la tabla primaria. Los nombres de etiqueta de índice pueden contener hasta 10 caracteres. De forma predeterminada, si se omite la etiqueta *TagName5,* la relación se establece mediante la clave de índice principal de la tabla primaria.  
  
 COMPROBAR *eExpression2*[ERROR *cMessageText2*]  
 Especifica la regla de validación de la tabla. ERROR *cMessageText2* especifica el mensaje de error de Visual FoxPro muestra cuando se ejecuta la regla de validación de la tabla. El mensaje se muestra solo cuando los datos se cambia dentro de una ventana del explorador o ventana de edición.  
  
 DE matriz *ArrayName*  
 Especifica el nombre de una matriz existente cuyo contenido es el nombre, el tipo, la precisión y la escala para cada campo en la tabla. El contenido de la matriz se puede definir con la **AFIELDS**función ().  
  
## <a name="remarks"></a>Comentarios  
 La nueva tabla se abre en el área de trabajo disponible más bajo y puede obtenerse mediante su alias. La nueva tabla se abre en modo exclusivo, independientemente de la configuración actual del conjunto exclusivo.  
  
 Si una base de datos está abierta y no incluye la cláusula libre, se agrega la nueva tabla a la base de datos. No se puede crear una nueva tabla con el mismo nombre que una tabla en la base de datos.  
  
 Si una base de datos está abierta, CREATE TABLE - SQL requiere el uso exclusivo de la base de datos. Para abrir una base de datos para uso exclusivo, incluir exclusivo en Abrir base de datos.  
  
 Si una base de datos no está abierto cuando se crea la nueva tabla, incluidas las cláusulas de nombre, CHECK, DEFAULT, FOREIGN KEY, PRIMARY KEY o referencias genera un error.  
  
> [!NOTE]  
>  Sintaxis de CREATE TABLE utiliza comas para separar ciertas opciones de CREATE TABLE. Además, se deben colocar el NULL, no es NULL, verificación, predeterminado, PRIMARY KEY y cláusula único dentro de los paréntesis que contiene las definiciones de columna.  
  
## <a name="driver-remarks"></a>Comentarios del controlador  
 Cuando la aplicación envía la instrucción ODBC SQL CREATE TABLE para el origen de datos, el controlador ODBC de Visual FoxPro traduce el comando en el comando de tabla de FoxProCREATE Visual mediante la sintaxis mostrada en la tabla siguiente.  
  
|Sintaxis de ODBC|Sintaxis de Visual FoxPro|  
|-----------------|--------------------------|  
|CREATE TABLE *nombre de la tabla de base*<br /><br /> (*identificador de la columna tipo de datos*<br /><br /> [NO NULO]<br /><br /> [,*identificador de la columna tipo de datos*<br /><br /> [NOT NULL]...)|Crear tabla *TableName1* [nombre *LongTableName*]<br /><br /> (*Nombredecampo1* *FieldType*<br /><br /> [(*nFieldWidth* [, *nPrecision*])]<br /><br /> [NO ES NULL)]|  
  
 Cuando se crea una tabla con el controlador, el controlador cierra la tabla inmediatamente después de crear para permitir el acceso a la tabla por otros usuarios. Esto difiere de Visual FoxPro, lo que deja abierto exclusivamente al crear la tabla. Sin embargo, si se ejecuta un procedimiento almacenado en el origen de datos que contiene una instrucción CREATE TABLE, la tabla se deja abierta.  
  
 Si el origen de datos es una base de datos (archivo .dbc), el controlador ODBC de Visual FoxPro crea una tabla denominada *LongTableName* con el mismo nombre que el *nombre de la tabla de base*.  
  
### <a name="using-data-definition-language-ddl"></a>Mediante el lenguaje de definición de datos (DDL)  
 No se puede incluir DDL en los lugares siguientes:  
  
-   En una instrucción SQL por lotes requiere una transacción  
  
-   En el modo de confirmación manual, después de una instrucción que requiere una transacción, a menos que la aplicación llama primero **SQLTransact**.  
  
 Por ejemplo, si desea crear una tabla temporal, debe crear la tabla antes de comenzar la instrucción que requiere una transacción. Si incluye la instrucción CREATE TABLE en una instrucción SQL que requiere una transacción por lotes, el controlador devuelve un mensaje de error.  
  
## <a name="see-also"></a>Vea también  
 [Modificar tabla - comando SQL](../../odbc/microsoft/alter-table-sql-command.md)   
 [Tipos de datos admitidos (controlador ODBC de Visual FoxPro)](../../odbc/microsoft/supported-data-types-visual-foxpro-odbc-driver.md)   
 [Insertar: comando SQL](../../odbc/microsoft/insert-sql-command.md)   
 [Seleccione - comando SQL](../../odbc/microsoft/select-sql-command.md)

