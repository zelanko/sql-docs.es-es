---
title: Constantes (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 7/22/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|data-types
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- uniqueidentifier data type
- bit data type
- constants [SQL Server]
- scalar values
- money data type, constants
- binary [SQL Server], constants
- float data type
- Unicode [SQL Server], constants
- constants [Transact-SQL]
- integer constants
- decimal data type, constants
- character strings [SQL Server], constants
- positive values [SQL Server]
- formats [SQL Server], constants
- datetime data type [SQL Server]
- literals [SQL Server], constants
- real data type
- negative values
ms.assetid: 58ae3ff3-b1d5-41b2-9a2f-fc7ab8c83e0e
caps.latest.revision: 22
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d9b212354492b96ca69ebf29afbc39c8ed1de6e3
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="constants-transact-sql"></a>Constantes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Una constante, también conocida como valor literal o escalar, es un símbolo que representa un valor de datos específico. El formato de las constantes depende del tipo de datos del valor que representan.
  
## <a name="character-string-constants"></a>Constantes de cadena de caracteres
Las constantes de cadena de caracteres van entre comillas simples e incluyen caracteres alfanuméricos (a-z, A-Z y 0-9) y caracteres especiales, como el signo de exclamación (!), la arroba (@) y el signo de número (#). A las constantes de cadena de caracteres se les asigna la intercalación predeterminada de la base de datos actual, a menos que se utilice la cláusula COLLATE para especificar una intercalación. Las cadenas de caracteres escritas por los usuarios se evalúan a través de la página de códigos del equipo y, si es necesario, se traducen a la página de códigos predeterminada de la base de datos.
  
Si la opción QUOTED_IDENTIFIER se ha establecido en OFF para una conexión, las cadenas de caracteres también pueden encerrarse entre comillas dobles, pero el proveedor de Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client y el controlador ODBC utilizan automáticamente SET QUOTED_IDENTIFIER ON. Se recomienda el uso de comillas simples.
  
Si una cadena de caracteres entre comillas simples contiene una comilla, represente la comilla interna con dos comillas simples. Esto no es necesario en las cadenas incluidas entre comillas dobles.
  
Éstos son algunos ejemplos de cadenas de caracteres:
  
```sql
'Cincinnati'  
'O''Brien'  
'Process X is 50% complete.'  
'The level for job_id: %d should be between %d and %d.'  
"O'Brien"  
```  
  
Las cadenas vacías se representan como dos comillas simples sin nada entre ellas. En el modo de compatibilidad 6.x, una cadena vacía se trata como un espacio.
  
Las constantes de cadena de caracteres admiten intercalaciones mejoradas.
  
> [!NOTE]  
>  Constantes con más de 8.000 bytes se consideran como tipos de caracteres **varchar (max)** datos.  
  
## <a name="unicode-strings"></a>Cadenas Unicode
Las cadenas Unicode tienen un formato similar al de las cadenas de caracteres, pero están precedidas por el identificador N (N es el idioma nacional en el estándar SQL-92). El prefijo N tiene que estar en mayúsculas. Por ejemplo, 'Michél' es una constante de caracteres, mientras que N'Michél' es una constante Unicode. Las constantes Unicode se interpretan como datos Unicode y no se evalúan mediante una página de códigos. Las constantes Unicode tienen intercalación. Esta intercalación controla principalmente las comparaciones y la distinción entre mayúsculas y minúsculas. A las constantes Unicode se les asigna la intercalación predeterminada de la base de datos actual, a menos que se utilice la cláusula COLLATE para especificar una intercalación. Los datos Unicode se almacenan con 2 bytes por carácter en lugar de 1 byte por carácter, como los datos de cadenas de caracteres. Para más información, consulte [Compatibilidad con la intercalación y Unicode](../../relational-databases/collations/collation-and-unicode-support.md).
  
Las constantes de cadena Unicode aceptan intercalaciones mejoradas.
  
> [!NOTE]  
>  Las constantes Unicode superiores a 8.000 bytes se consideran tipos como **nvarchar (max)** datos.  
  
## <a name="binary-constants"></a>Constantes binarias
Las constantes binarias tienen el prefijo `0x` y son cadenas de números hexadecimales. No se incluyen entre comillas.
  
Éstos son algunos ejemplos de cadenas binarias:
  
```sql
0xAE  
0x12Ef  
0x69048AEFDD010E  
0x  (empty binary string)  
```  
  
> [!NOTE]  
>  Constantes binarias con más de 8.000 bytes se consideran como tipos **varbinary (max)** datos.  
  
## <a name="bit-constants"></a>constantes de tipo bit
**bit** constantes se representan mediante los números 0 ó 1 y no se incluyen entre comillas. Si se utiliza un número mayor que uno, se convierte en uno.
  
## <a name="datetime-constants"></a>constantes de fecha y hora
**fecha y hora** constantes se representan mediante valores de fecha de caracteres en formatos específicos, entre comillas simples.
  
Los siguientes son ejemplos de **datetime** constantes:
  
```sql
'December 5, 1985'  
'5 December, 1985'  
'851205'  
'12/5/98'  
```  
  
Ejemplos de constantes de fecha y hora son:
  
```sql
'14:30:24'  
'04:24 PM'  
```  
  
## <a name="integer-constants"></a>constantes de enteros
**entero** constantes se representan mediante una cadena de números que no se incluyen entre comillas y no contienen decimales. **entero** constantes deben ser números enteros; no pueden contener decimales.
  
Los siguientes son ejemplos de **entero** constantes:
  
```sql
1894  
2  
```  
  
## <a name="decimal-constants"></a>constantes de tipo decimal
**decimal** constantes se representan mediante una cadena de números que no se incluyen entre comillas y contienen un separador decimal.
  
Los siguientes son ejemplos de **decimal** constantes:
  
```sql
1894.1204  
2.0  
```  
  
## <a name="float-and-real-constants"></a>constantes de tipo float y real
**float** y **real** constantes se representan mediante la notación científica.
  
Los siguientes son ejemplos de **float** o **real** valores:
  
```sql
101.5E5  
0.5E-2  
```  
  
## <a name="money-constants"></a>constantes de tipo Money
**Money** constantes se representan como una cadena de números con un punto decimal opcional y un símbolo de moneda opcionales como prefijo. **dinero** no van entrecomilladas entre comillas.
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no impone ninguna clase de reglas de agrupamiento, como la inserción de una coma (,) cada tres dígitos, en las cadenas que representan dinero.
  
> [!NOTE]  
>  Comas se omiten en cualquier parte de la manera especificada **dinero** literal.  
  
Los siguientes son ejemplos de **dinero** constantes:
  
```sql
$12  
$542023.14  
```  
  
## <a name="uniqueidentifier-constants"></a>constantes de tipo uniqueidentifier
**uniqueidentifier** constantes consisten en una cadena que representa un GUID. Se pueden especificar en formato de cadena de caracteres o binario.
  
Estos dos ejemplos especifican el mismo GUID:
  
```sql
'6F9619FF-8B86-D011-B42D-00C04FC964FF'  
0xff19966f868b11d0b42d00c04fc964ff  
```  
  
## <a name="specifying-negative-and-positive-numbers"></a>Especificar números negativos y positivos  
Para indicar si un número es positivo o negativo, aplique la  **+**  o  **-**  operadores unarios una constante numérica. Esto crea una expresión numérica que representa el valor numérico con signo. Constantes numéricas usar positivo cuando el  **+**  o  **-**  no se aplican los operadores unarios.
  
Firmado **entero** expresiones:  
  
```sql
+145345234
-2147483648
```
Firmado **decimal** expresiones:  
  
```sql
+145345234.2234
-2147483648.10
```
  
Firmado **float** expresiones:  
  
```sql
+123E-3
-12E5
```
  
Firmado **dinero** expresiones:  
  
```sql
-$45.56
+$423456.99
```
  
## <a name="enhanced-collations"></a>Intercalaciones mejoradas  
SQL Server admite las constantes de cadena de caracteres y Unicode compatibles con las intercalaciones mejoradas. Para obtener más información, consulte el [COLLATE &#40; Transact-SQL &#41; ](http://msdn.microsoft.com/library/4ba6b7d8-114a-4f4e-bb38-fe5697add4e9) cláusula.
  
## <a name="see-also"></a>Vea también
[Tipos de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[Expresiones &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
[Operadores &#40; Transact-SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)
  
  

