---
title: "Nombre de intercalación de SQL Server (Transact-SQL) | Documentos de Microsoft"
ms.custom: 
ms.date: 05/11/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- collations [SQL Server], SQL collations
- SQL collations
- names [SQL Server], collations
ms.assetid: 56483d24-add7-483d-9b96-c6fda460ddbc
caps.latest.revision: 30
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: fc7265f4efe0d790ab61e4e522af83d6b91b710a
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="sql-server-collation-name-transact-sql"></a>Nombre de intercalación de SQL Server (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Es una cadena que especifica el nombre de intercalación de una intercalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite intercalaciones de Windows. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] también admite un número limitado (<80) de las intercalaciones denominadas intercalaciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se desarrollaron antes de que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admitiera intercalaciones de Windows. Las intercalaciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se siguen admitiendo por compatibilidad con versiones anteriores, pero no se deben utilizar en nuevos trabajos de desarrollo. Para obtener más información acerca de las intercalaciones de Windows, vea [nombre de intercalación de Windows &#40; Transact-SQL &#41; ](../../t-sql/statements/windows-collation-name-transact-sql.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
<SQL_collation_name> :: =   
SQL_SortRules[_Pref]_CPCodepage_<ComparisonStyle>  
  
<ComparisonStyle> ::=  
_CaseSensitivity_AccentSensitivity | _BIN  
```  
  
## <a name="arguments"></a>Argumentos  
 *SortRules*  
 Cadena que identifica el alfabeto o el idioma cuyas reglas de ordenación se aplican cuando se especifica el orden del diccionario. Por ejemplo: Latin1_General o Polish.  
  
 **Pref**  
 Especifica la preferencia de mayúsculas. Aunque la comparación distinga entre mayúsculas y minúsculas, la versión en mayúsculas de una letra se ordena antes que la versión en minúsculas, cuando no existe ningún otro tipo de diferenciación.  
  
 *Codepage*  
 Especifica un número de uno a cuatro dígitos que identifica la página de códigos que la intercalación utiliza. **CP1** especifica la página de códigos 1252, se especifica para el número de página de código completo de páginas de todo el código. Por ejemplo, **CP1251** especifica la página de códigos 1251 y **CP850** especifica la página de códigos 850.  
  
 *Propiedades CaseSensitivity*  
 **CI** especifica mayúsculas de minúsculas, **CS** especifica entre mayúsculas y minúsculas.  
  
 *AccentSensitivity*  
 **AI** especifica acentos, **AS** especifica la distinción de acentos.  
  
 **PAPELERA**  
 Especifica el criterio de ordenación binario que se va a utilizar.  
  
## <a name="remarks"></a>Comentarios  
 Para enumerar las intercalaciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admitidas por el servidor, ejecute la consulta siguiente.  
  
```  
SELECT * FROM sys.fn_helpcollations()   
WHERE name LIKE 'SQL%';  
```  

>  [!NOTE]  
>  Para la ordenación Order ID. de 80, utilice cualquiera de las intercalaciones de Windows con la página de códigos de 1250 y orden binario. Por ejemplo: Albanian_BIN, Croatian_BIN, Czech_BIN, Romanian_BIN, Slovak_BIN, Slovenian_BIN.  
  
## <a name="see-also"></a>Vea también  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [Constantes &#40; Transact-SQL &#41;](../../t-sql/data-types/constants-transact-sql.md)   
 [CREATE DATABASE &#40;Transact-SQL de SQL Server&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [tabla &#40; Transact-SQL &#41;](../../t-sql/data-types/table-transact-sql.md)   
 [sys.fn_helpcollations &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md)  
  
  

