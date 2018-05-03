---
title: COLLATIONPROPERTY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- COLLATIONPROPERTY_TSQL
- COLLATIONPROPERTY
dev_langs:
- TSQL
helpviewer_keywords:
- collations [SQL Server], properties
- COLLATIONPROPERTY function
ms.assetid: f5029e74-a1db-4f69-b0f5-5ee920c3311d
caps.latest.revision: 44
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 041b1bdcc190980d471b48e7525da0fa035d087a
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="collation-functions---collationproperty-transact-sql"></a>Funciones de intercalación: COLLATIONPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Esta función devuelve la propiedad de una intercalación especificada en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
COLLATIONPROPERTY( collation_name , property )  
```  
  
## <a name="arguments"></a>Argumentos  
*collation_name*  
El nombre de la intercalación. El argumento *nombre_de_la_intercalación* tiene un tipo de datos **nvarchar (128)**, sin valor predeterminado.
  
*property*  
La propiedad de intercalación. El argumento *propiedad* tiene un tipo de datos **varchar (128)** y puede tener uno de los valores siguientes:
  
|Nombre de propiedad|Description|  
|---|---|
|**CodePage**|La página de códigos no Unicode de la intercalación. Vea [Appendix G DBCS/Unicode Mapping Tables](https://msdn.microsoft.com/en-us/library/cc194886.aspx) (Apéndice G: tablas de asignaciones DBCS/Unicode) y [Appendix H Code Pages](https://msdn.microsoft.com/en-us/library/cc195051.aspx) (Apéndice H: páginas de código) para traducir estos valores y ver sus asignaciones de caracteres.|  
|**LCID**|LCID de Windows de la intercalación. Vea [LCID Structure](https://msdn.microsoft.com/en-us/library/cc233968.aspx) (Estructura de LCID) para traducir estos valores (primero hay que convertirlos a **varbinary**).|  
|**ComparisonStyle**|Estilo de comparación de Windows de la intercalación. Devuelve 0 para todas las intercalaciones binarias, tanto (\_BIN) como (\_BIN2), así como cuando todas las propiedades distinguen entre mayúsculas y minúsculas. Valores de máscara de bits:<br /><br /> Omitir mayúsculas y minúsculas: 1<br /><br /> Omitir acento: 2<br /><br /> Omitir Kana: 65536<br /><br /> Omitir ancho: 131072<br /><br /> Nota: La opción de distinción de selector de variación (\_VSS) no se representa en este valor, aunque afecta al comportamiento de las comparaciones.|  
|**Versión**|La versión de la intercalación, derivada del campo Id. de versión de la intercalación. Devuelve un valor entero comprendido entre 0 y 3.<br /><br /> Las intercalaciones con "140" en el nombre devuelven 3.<br /><br /> Las intercalaciones con "100" en el nombre devuelven 2.<br /><br /> Las intercalaciones con "90" en el nombre devuelven 1.<br /><br /> Todas las demás intercalaciones devuelven 0.|  
  
## <a name="return-types"></a>Tipos de valores devueltos
**sql_variant**
  
## <a name="examples"></a>Ejemplos  
  
```sql
SELECT COLLATIONPROPERTY('Traditional_Spanish_CS_AS_KS_WS', 'CodePage');  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
1252   
```  
  
[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
```sql
SELECT COLLATIONPROPERTY('Traditional_Spanish_CS_AS_KS_WS', 'CodePage')  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
1252   
```  
  
## <a name="see-also"></a>Vea también
[sys.fn_helpcollations &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md)
  
  

