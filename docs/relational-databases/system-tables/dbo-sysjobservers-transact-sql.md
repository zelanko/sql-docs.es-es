---
title: dbo.sysjobservers (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/26/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysjobservers
- sysjobservers_TSQL
- dbo.sysjobservers
- dbo.sysjobservers_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysjobservers system table
ms.assetid: 9abcc20f-a421-4591-affb-62674d04575e
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 3b02aa88951f7dd4e82ab26fcd54d715027b1ab7
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2020
ms.locfileid: "85890450"
---
# <a name="dbosysjobservers-transact-sql"></a>dbo.sysjobservers (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Almacena la asociación o relación de un trabajo determinado con uno o más servidores de destino. Esta tabla se almacena en la base de datos msdb.
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|job_id|**uniqueidentifier**|Número de identificación del trabajo.|  
|server_id|**int**|Número de identificación del servidor.|  
|last_run_outcome|**tinyint**|Resultado de la última ejecución del trabajo:<br /><br /> **0** = error<br /><br /> **1** = correcto<br /><br /> **2** = reintento<br /><br /> **3** = cancelar<br /><br /> **4** = en curso<br /><br /> **5** = desconocido (consulte la sección Comentarios siguiente) |  
|last_outcome_ message|**nvarchar(1024)**|Mensaje asociado, si existe, a la columna last_run_outcome.|  
|last_run_date|**int**|Fecha en que se ejecutó el trabajo por última vez.|  
|last_run_time|**int**|Hora a la que se ejecutó el trabajo por última vez.|  
|last_run_duration|**int**|Duración de la ejecución del trabajo, en horas, minutos y segundos. Se calcula mediante la fórmula: (*horas* \* 10000) + (*minutos* \* 100) + *segundos*.|  


## <a name="remarks"></a>Comentarios

Un valor superior A *4* significa que el Agente SQL no conoce el estado de ese trabajo. El *last_run_outcome* se establece inicialmente en *5* cuando se crea un trabajo.


## <a name="see-also"></a>Consulte también

[Tablas de Agente SQL Server &#40;&#41;de Transact-SQL](../../relational-databases/system-tables/sql-server-agent-tables-transact-sql.md)  
