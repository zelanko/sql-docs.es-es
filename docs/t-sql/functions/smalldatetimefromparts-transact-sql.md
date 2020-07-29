---
title: SMALLDATETIMEFROMPARTS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SMALLDATETIMEFROMPARTS
- SMALLDATETIMEFROMPARTS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- SMALLDATETIMEFROMPARTS function
ms.assetid: 7467fdab-e588-419c-9e29-42caec34a9ea
author: julieMSFT
ms.author: jrasnick
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0850f263a786cbb22b00bb526e0efc2229adfd50
ms.sourcegitcommit: 768f046107642f72693514f51bf2cbd00f58f58a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/23/2020
ms.locfileid: "87111334"
---
# <a name="smalldatetimefromparts-transact-sql"></a>SMALLDATETIMEFROMPARTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  Devuelve un valor **smalldatetime** de la fecha y la hora especificadas.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
SMALLDATETIMEFROMPARTS ( year, month, day, hour, minute )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *year*  
 Expresión entera que especifica un año.  
  
 *month*  
 Expresión entera que especifica un mes.  
  
 *day*  
 Expresión entera que especifica un día.  
  
 *hour*  
 Expresión entera que especifica horas.  
  
 *minute*  
 Expresión entera que especifica minutos.  
  
## <a name="return-types"></a>Tipos de valor devuelto  
 **smalldatetime**  
  
## <a name="remarks"></a>Observaciones  
 Esta función actúa como un constructor para un valor **smalldatetime** totalmente inicializado. Si los argumentos no son válidos, se generará un error. Si los argumentos necesarios son NULL, se devuelve un valor NULL.  
  
 Esta función se puede enviar de forma remota a servidores de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] y superiores. No se puede enviar de forma remota a servidores que tengan una versión inferior a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
## <a name="examples"></a>Ejemplos  
  
```  
SELECT SMALLDATETIMEFROMPARTS ( 2010, 12, 31, 23, 59 ) AS Result  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
---------------------------  
2010-12-31 23:59:00  
  
(1 row(s) affected)  
```  
  

