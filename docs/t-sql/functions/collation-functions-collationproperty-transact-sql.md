---
title: COLLATIONPROPERTY (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: aecf422ca2289b2a417147eb402921bb8530d969
ms.openlocfilehash: 166a85e5fe33a95cd8a36f221c2a774e4a0a9fb2
ms.contentlocale: es-es
ms.lasthandoff: 10/24/2017

---
# <a name="collation-functions---collationproperty-transact-sql"></a>Funciones de intercalación - COLLATIONPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Devuelve la propiedad de una intercalación especificada en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
COLLATIONPROPERTY( collation_name , property )  
```  
  
## <a name="arguments"></a>Argumentos  
*collation_name*  
Es el nombre de la intercalación. *collation_name* es **nvarchar (128)**, y no tiene valor predeterminado.
  
*propiedad*  
Es la propiedad de la intercalación. *propiedad* es **varchar (128)**, y puede tener uno de los siguientes valores:
  
|Nombre de la propiedad|Description|  
|---|---|
|**CodePage**|La página de códigos no Unicode de la intercalación. Vea [asignar tablas del apéndice G DBCS/Unicode](https://msdn.microsoft.com/en-us/library/cc194886.aspx) y [páginas de códigos de Apéndice H](https://msdn.microsoft.com/en-us/library/cc195051.aspx) para traducir estos valores y ver sus asignaciones de caracteres.|  
|**LCID**|LCID de Windows de la intercalación. Vea [LCID estructura](https://msdn.microsoft.com/en-us/library/cc233968.aspx) para traducir estos valores (debe convertir a `VARBINARY` primera).|  
|**ComparisonStyle**|Estilo de comparación de Windows de la intercalación. Devuelve 0 para todas las intercalaciones binarias (ambos `_BIN` y `_BIN2`), así como cuando todas las propiedades son confidenciales. Valores de máscara de bits:<br /><br /> Omitir mayúsculas y minúsculas: 1<br /><br /> Omitir acento: 2<br /><br /> Omitir Kana: 65536<br /><br /> Omitir ancho: 131072|  
|**Versión**|Versión de la intercalación, derivada del campo de versión del identificador de intercalación. Devuelve un valor entero entre 0 y 3.<br /><br /> Intercalaciones con "140" en el nombre devuelven 3.<br /><br /> Intercalaciones con "100" en el nombre devuelven 2.<br /><br /> Intercalaciones con "90" en el nombre devuelven 1.<br /><br /> Todas las demás intercalaciones devuelven 0.|  
  
## <a name="return-types"></a>Tipos de valor devuelto
**sql_variant**
  
## <a name="examples"></a>Ejemplos  
  
```sql
SELECT COLLATIONPROPERTY('Traditional_Spanish_CS_AS_KS_WS', 'CodePage');  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
1252   
```  
  
[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]y[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
```sql
SELECT COLLATIONPROPERTY('Traditional_Spanish_CS_AS_KS_WS', 'CodePage')  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
1252   
```  
  
## <a name="see-also"></a>Vea también
[sys.fn_helpcollations &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md)
  
  


