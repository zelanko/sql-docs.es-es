---
title: Escribir instrucciones Transact-SQL internacionales | Microsoft Docs
ms.custom: ''
ms.date: 04/24/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- writing international statements
- Transact-SQL international considerations
- international considerations [SQL Server], Transact-SQL
- Database Engine international considerations [SQL Server], Transact-SQL
- statements [SQL Server], international
- database international considerations [SQL Server], Transact-SQL
- dates [SQL Server], international considerations
ms.assetid: f0b10fee-27f7-45fe-aece-ccc3f63bdcdb
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 20e587aeb7c0ed34762bf1f90488a06cafc0ec93
ms.sourcegitcommit: 0a4879dad09c6c42ad1ff717e4512cfea46820e9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/27/2019
ms.locfileid: "67412998"
---
# <a name="write-international-transact-sql-statements"></a>Escribir instrucciones Transact-SQL internacionales
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  Las bases de datos y las aplicaciones de bases de datos que utilizan instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] obtendrán una mayor portabilidad de un idioma a otro, o admitirán varios idiomas, si se siguen estas directrices:  

-   A partir de [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)], use:
    -   Los tipos de datos **char**, **varchar** y **varchar(max)** con una intercalación compatible con [ UTF-8](../../relational-databases/collations/collation-and-unicode-support.md#utf8).
    -   Los tipos de datos **nchar**, **nvarchar** y **nvarchar(max)** con una intercalación habilitada para [caracteres complementarios](../../relational-databases/collations/collation-and-unicode-support.md#Supplementary_Characters).      

    Esto evita problemas de conversión de página de códigos. Para otras consideraciones, consulte [Diferencias de almacenamiento entre UTF-8 y UTF-16](../../relational-databases/collations/collation-and-unicode-support.md#storage_differences).  

-   Hasta [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)], reemplace todos los usos de los tipos de datos **char**, **varchar** y **varchar(max)** por **nchar**, **nvarchar** y **nvarchar(max)** . Esto evita problemas de conversión de página de códigos. Para más información, consulte [Compatibilidad con la intercalación y Unicode](../../relational-databases/collations/collation-and-unicode-support.md). 
    > [!IMPORTANT]
    > El tipo de datos **text** está en desuso y no debe usarse en nuevos trabajos de desarrollo. Planee la conversión de datos de tipo **text** a **varchar (max)** .
  
-   Cuando realice comparaciones y operaciones con los meses y días de la semana, utilice las partes numéricas de la fecha en lugar de cadenas de nombres. Las distintas configuraciones de idioma devuelven nombres diferentes para los meses y los días de la semana. Por ejemplo, `DATENAME(MONTH,GETDATE())` devuelve `May` cuando el idioma está establecido en inglés de EE. UU., devuelve `Mai` cuando el idioma está establecido en alemán y `mai` cuando el idioma está establecido en francés. En su lugar, utilice una función como [DATEPART](../../t-sql/functions/datepart-transact-sql.md) que utiliza el número del mes en lugar del nombre. Utilice los nombres DATEPART cuando genere conjuntos de resultados que se van a mostrar al usuario ya que, generalmente, los nombres de fecha resultan más significativos que una representación numérica. No codifique, sin embargo, ninguna lógica que dependa de que los nombres mostrados estén en un idioma determinado.  
  
-   Cuando especifique fechas en las comparaciones o como entrada de las instrucciones INSERT o UPDATE, utilice constantes que se interpretan igual en todas las configuraciones de idioma:  
  
    -   Las aplicaciones ADO, OLE DB y ODBC deben utilizar la siguiente marca de tiempo, fecha y cláusulas de escape de hora ODBC:  
  
         **{ ts"** _yyyy_ **-** _mm_ **-** _dd_ _hh_ **:** _mm_ **:** _ss_ [ **.** _fff_] **"}** como: **{ ts"1998-09-24 10:02:20"}**  
  
         **{ d"** _yyyy_ **-** _mm_ **-** _dd_ **"}** como: **{ d"1998-09-24"}**
  
         **{ t"** _hh_ **:** _mm_ **:** _ss_ **"}** como: **{ t"10:02:20"}**  
  
    -   Las aplicaciones que utilizan otras API o desencadenadores, procedimientos almacenados y scripts [!INCLUDE[tsql](../../includes/tsql-md.md)] deben utilizar las cadenas numéricas sin separar. Por ejemplo, *yyyymmdd* como en 19980924.  
  
    -   Las aplicaciones que usan otras API o scripts, procedimientos almacenados y desencadenadores [!INCLUDE[tsql](../../includes/tsql-md.md)] deben usar la instrucción [CONVERT](../../t-sql/functions/cast-and-convert-transact-sql.md) con un parámetro de estilo explícito para todas las conversiones entre los tipos de datos **time**, **date**, **smalldate**, **datetime**, **datetime2** y **datetimeoffset** y los tipos de datos de cadenas de caracteres. Por ejemplo, la siguiente instrucción se interpreta igual en todas las configuraciones de conexión de formato de fecha o de idioma:  
  
        ```sql  
        SELECT *  
        FROM AdventureWorks2012.Sales.SalesOrderHeader  
        WHERE OrderDate = CONVERT(DATETIME, '20060719', 101)  
        ```  
  
## <a name="see-also"></a>Vea también
[CAST y CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)     
[DATEPART &#40;Transact-SQL&#41;](../../t-sql/functions/datepart-transact-sql.md)        
[Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md)      
