---
title: "Establezca el perfil de estadísticas (Transact-SQL) | Documentos de Microsoft"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 69ceaedf2cfe62b20217b4e218568cec1bc2a933
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="set-statistics-profile-transact-sql"></a>SET STATISTICS PROFILE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Muestra la información de perfil de una instrucción. STATISTICS PROFILE funciona con consultas ad hoc, vistas y procedimientos almacenados.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SET STATISTICS PROFILE { ON | OFF }  
```  
  
## <a name="remarks"></a>Comentarios  
 Cuando STATISTICS PROFILE es ON, cada consulta ejecutada devuelve su conjunto de resultados normal, seguido de un conjunto de resultados adicional que muestra el perfil de ejecución de la consulta.  
  
 El conjunto de resultados adicional contiene las columnas SHOWPLAN_ALL de la consulta y estas columnas adicionales.  
  
|Nombre de columna|Description|  
|-----------------|-----------------|  
|**Filas**|Número real de filas que produce cada operador|  
|**Se ejecuta**|Número de veces que se ha ejecutado el operador|  
  
## <a name="permissions"></a>Permissions  
 Para utilizar SET STATISTICS PROFILE y ver el resultado, el usuario debe tener los permisos siguientes:  
  
-   Los permisos adecuados para ejecutar instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
-   El permiso SHOWPLAN para todas las bases de datos que contienen objetos a los que hacen referencia las instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 Para las instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] que no generan conjuntos de resultados de STATISTICS PROFILE, solo se necesitan los permisos adecuados para ejecutar las instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)]. Para las instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] que generan conjuntos de resultados de STATISTICS PROFILE, el permiso de ejecución de la instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] y el permiso SHOWPLAN deben ser correctos, o la ejecución de la instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] se anulará y no se generará información relativa al plan de presentación.  
  
## <a name="see-also"></a>Vea también  
 [Instrucciones SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET SHOWPLAN_ALL &#40; Transact-SQL &#41;](../../t-sql/statements/set-showplan-all-transact-sql.md)   
 [ESTABLECER STATISTICS TIME &#40; Transact-SQL &#41;](../../t-sql/statements/set-statistics-time-transact-sql.md)   
 [SET STATISTICS IO &#40; Transact-SQL &#41;](../../t-sql/statements/set-statistics-io-transact-sql.md)  
  
  

