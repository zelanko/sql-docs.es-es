---
title: SET STATISTICS PROFILE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- PROFILE
- SET_STATISTICS_PROFILE_TSQL
- PROFILE_TSQL
- SET STATISTICS PROFILE
dev_langs:
- TSQL
helpviewer_keywords:
- profiles [SQL Server], displaying
- statements [SQL Server], profile information
- SET STATISTICS PROFILE statement
- STATISTICS PROFILE option
- statistical information [SQL Server], profiles
ms.assetid: c635e262-35fa-421a-aa6f-a1c30f351647
caps.latest.revision: 34
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 6494f792c1dcfbb92bfe48d3063df533d0ff1510
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="set-statistics-profile-transact-sql"></a>SET STATISTICS PROFILE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Muestra la información de perfil de una instrucción. STATISTICS PROFILE funciona con consultas ad hoc, vistas y procedimientos almacenados.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SET STATISTICS PROFILE { ON | OFF }  
```  
  
## <a name="remarks"></a>Notas  
 Cuando STATISTICS PROFILE es ON, cada consulta ejecutada devuelve su conjunto de resultados normal, seguido de un conjunto de resultados adicional que muestra el perfil de ejecución de la consulta.  
  
 El conjunto de resultados adicional contiene las columnas SHOWPLAN_ALL de la consulta y estas columnas adicionales.  
  
|Nombre de columna|Description|  
|-----------------|-----------------|  
|**Filas**|Número real de filas que produce cada operador|  
|**Executes**|Número de veces que se ha ejecutado el operador|  
  
## <a name="permissions"></a>Permisos  
 Para utilizar SET STATISTICS PROFILE y ver el resultado, el usuario debe tener los permisos siguientes:  
  
-   Los permisos adecuados para ejecutar instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
-   El permiso SHOWPLAN para todas las bases de datos que contienen objetos a los que hacen referencia las instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 Para las instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] que no generan conjuntos de resultados de STATISTICS PROFILE, solo se necesitan los permisos adecuados para ejecutar las instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)]. Para las instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] que generan conjuntos de resultados de STATISTICS PROFILE, el permiso de ejecución de la instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] y el permiso SHOWPLAN deben ser correctos, o la ejecución de la instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] se anulará y no se generará información relativa al plan de presentación.  
  
## <a name="see-also"></a>Ver también  
 [Instrucciones SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET SHOWPLAN_ALL &#40;Transact-SQL&#41;](../../t-sql/statements/set-showplan-all-transact-sql.md)   
 [SET STATISTICS TIME &#40;Transact-SQL&#41;](../../t-sql/statements/set-statistics-time-transact-sql.md)   
 [SET STATISTICS IO &#40;Transact-SQL&#41;](../../t-sql/statements/set-statistics-io-transact-sql.md)  
  
  
