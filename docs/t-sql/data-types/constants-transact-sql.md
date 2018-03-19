---
title: Constantes (Transact-SQL) | Microsoft Docs
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
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: aae955a177f637e3c359eabf02679025cbecdb3a
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
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
>  Las constantes de caracteres con más de 8000 bytes se consideran como tipos de datos **varchar(max)**.  
  
## <a name="unicode-strings"></a>Cadenas Unicode
Las cadenas Unicode tienen un formato similar al de las cadenas de caracteres, pero están precedidas por el identificador N (N es el idioma nacional en el estándar SQL-92). El prefijo N tiene que estar en mayúsculas. Por ejemplo, 'Michél' es una constante de caracteres, mientras que N'Michél' es una constante Unicode. Las constantes Unicode se interpretan como datos Unicode y no se evalúan mediante una página de códigos. Las constantes Unicode tienen intercalación. Esta intercalación controla principalmente las comparaciones y la distinción entre mayúsculas y minúsculas. A las constantes Unicode se les asigna la intercalación predeterminada de la base de datos actual, a menos que se utilice la cláusula COLLATE para especificar una intercalación. Los datos Unicode se almacenan con 2 bytes por carácter en lugar de 1 byte por carácter, como los datos de cadenas de caracteres. Para más información, consulte [Compatibilidad con la intercalación y Unicode](../../relational-databases/collations/collation-and-unicode-support.md).
  
Las constantes de cadena Unicode aceptan intercalaciones mejoradas.
  
> [!NOTE]  
>  Las constantes Unicode con más de 8000 bytes se consideran como tipos de datos **nvarchar(max)**.  
  
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
>  Las constantes binarias con más de 8000 bytes se consideran como tipos de datos **varbinary(max)**.  
  
## <a name="bit-constants"></a>Constantes de tipo bit
Las constantes de tipo **bit** se representan con los números 0 o 1, y no se incluyen entre comillas. Si se utiliza un número mayor que uno, se convierte en uno.
  
## <a name="datetime-constants"></a>Constantes de tipo datetime
Las constantes de tipo **datetime** se representan mediante valores de fecha en formatos específicos de cadenas de caracteres, y se incluyen entre comillas simples.
  
Estos son algunos ejemplos de constantes **datetime**:
  
```sql
'December 5, 1985'  
'5 December, 1985'  
'851205'  
'12/5/98'  
```  
  
Ejemplos de constantes datetime:
  
```sql
'14:30:24'  
'04:24 PM'  
```  
  
## <a name="integer-constants"></a>constantes de enteros
Las constantes de tipo **integer** se representan mediante una cadena de números sin comillas y sin separadores decimales. Las constantes de tipo **integer** deben ser números enteros y no pueden contener decimales.
  
Estos son algunos ejemplos de constantes **integer**:
  
```sql
1894  
2  
```  
  
## <a name="decimal-constants"></a>Constantes de tipo decimal
Las constantes de tipo **decimal** se representan mediante una cadena de números sin comillas y con separador decimal.
  
Estos son algunos ejemplos de constantes **decimal**:
  
```sql
1894.1204  
2.0  
```  
  
## <a name="float-and-real-constants"></a>Constantes de tipo float y real
Las constantes de tipo **float** y **real** se representan en notación científica.
  
Estos son algunos ejemplos de valores de **float** o **real**:
  
```sql
101.5E5  
0.5E-2  
```  
  
## <a name="money-constants"></a>Constantes de tipo money
Las constantes de tipo **money** se representan como una cadena de números con un separador decimal y un símbolo de moneda opcionales como prefijo. Las constantes de tipo **money** no se incluyen entre comillas.
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no impone ninguna clase de reglas de agrupamiento, como la inserción de una coma (,) cada tres dígitos, en las cadenas que representan dinero.
  
> [!NOTE]  
>  Las comas no se tienen en cuenta en ningún lugar del valor literal **money** especificado.  
  
Estos son algunos ejemplos de constantes **money**:
  
```sql
$12  
$542023.14  
```  
  
## <a name="uniqueidentifier-constants"></a>Constantes de tipo uniqueidentifier
Las constantes de tipo **uniqueidentifier** son una cadena que representa un GUID. Se pueden especificar en formato de cadena de caracteres o binario.
  
Estos dos ejemplos especifican el mismo GUID:
  
```sql
'6F9619FF-8B86-D011-B42D-00C04FC964FF'  
0xff19966f868b11d0b42d00c04fc964ff  
```  
  
## <a name="specifying-negative-and-positive-numbers"></a>Especificar números negativos y positivos  
Para indicar si un número es positivo o negativo, aplique los operadores unarios **+** o **-** a una constante numérica. Esto crea una expresión numérica que representa el valor numérico con signo. Las constantes numéricas usan positivos cuando no se aplican los operadores unarios **+** o **-**.
  
Expresiones **integer** con signo:  
  
```sql
+145345234
-2147483648
```
Expresiones **decimal** con signo:  
  
```sql
+145345234.2234
-2147483648.10
```
  
Expresiones **float** con signo:  
  
```sql
+123E-3
-12E5
```
  
Expresiones **money** con signo:  
  
```sql
-$45.56
+$423456.99
```
  
## <a name="enhanced-collations"></a>Intercalaciones mejoradas  
SQL Server admite las constantes de cadena de caracteres y Unicode compatibles con las intercalaciones mejoradas. Para más información, vea la cláusula [COLLATE &#40;Transact-SQL&#41;](http://msdn.microsoft.com/library/4ba6b7d8-114a-4f4e-bb38-fe5697add4e9).
  
## <a name="see-also"></a>Vea también
[Tipos de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[Expresiones &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
[Operadores &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)
  
  
