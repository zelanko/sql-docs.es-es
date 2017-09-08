---
title: float y real (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 07/22/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- float
- real_TSQL
- real
- float_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- numeric data type, floating point
- float data type
- floating point data [SQL Server]
- real data type
ms.assetid: 08ea66b7-624e-4d8b-86bc-750ff76cdfc5
caps.latest.revision: 40
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 913aa9c71234d1b170a14f9707be82d45b1cd5b8
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="float-and-real-transact-sql"></a>float y real (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Tipos de datos numéricos y aproximados que se utilizan con datos numéricos de coma flotante. Los datos de coma flotante son aproximados; por tanto, no todos los valores del rango del tipo de datos se pueden representar con exactitud. El sinónimo ISO para **real** es **float (24)**.
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
**float** [ **(***n***)** ] donde  *n*  es el número de bits que se utilizan para almacenar la mantisa de la **float** número en notación científica y, por lo tanto, dicta el tamaño de almacenamiento y precisión. Si  *n*  se especifica, debe ser un valor entre **1** y **53**. El valor predeterminado de  *n*  es **53**.
  
|*n*valor|Precisión|Tamaño de almacenamiento|  
|---|---|---|
|**1-24**|7 dígitos|4 bytes|  
|**25-53**|15 dígitos|8 bytes|  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]trata  *n*  como uno de dos valores posibles. Si **1**<=n<=**24**,  *n*  se trata como **24**. Si **25**<=n<=**53**,  *n*  se trata como **53**.  
  
El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **float**[**(n)**] tipo de datos cumple con el estándar ISO para todos los valores de  *n*  de **1** a través de **53**. El sinónimo de **doble precisión** es **float (53)**.
  
## <a name="remarks"></a>Comentarios  
  
|Tipo de datos|Intervalo|Almacenamiento|  
|---|---|---|
|**float**|De - 1,79E+308 a -2,23E-308, 0 y de 2,23E-308 a 1,79E+308|Depende del valor de*n*|  
|**real**|De - 3,40E + 38 a -1,18E - 38, 0 y de 1,18E - 38 a 3,40E + 38|4 bytes|  
  
##  <a name="converting-float-and-real-data"></a>Convertir datos float y real  
Los valores de **float** se truncan cuando se convierten a cualquier tipo entero.
  
Cuando va a convertir de **float** o **real** datos de caracteres mediante la función de cadena STR es normalmente más útil que CAST (). Esto se debe a que STR permite más control sobre el formato. Para obtener más información, vea [STR &#40; Transact-SQL &#41; ](../../t-sql/functions/str-transact-sql.md) y [funciones &#40; Transact-SQL &#41; ](../../t-sql/functions/functions.md).
  
Conversión de **float** valores que utiliza la notación científica a **decimal** o **numérico** está restringida a valores de precisión de 17 dígitos solo. Cualquier valor con una precisión mayor de 17 se redondea a cero.
  
## <a name="see-also"></a>Vea también
[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
[CAST y CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[Conversiones de tipos de datos &#40; motor de base de datos &#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)  
[Tipos de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
[SET @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)
  
  

