---
title: MSSQLSERVER_8689 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 8689 (Database Engine error)
ms.assetid: 99467a32-6576-4272-a076-b16c06933f2a
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 18c8e591f255b57f8cbb935075695fca7bcc3960
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85637057"
---
# <a name="mssqlserver_8689"></a>MSSQLSERVER_8689
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalles  
  
| Atributo | Value |  
| :-------- | :---- |  
|Nombre de producto|SQL Server|  
|Id. de evento|8689|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|USEPLAN_ERR_NO_DB|  
|Texto del mensaje|La base de datos '%.*ls' especificada en la sugerencia USE PLAN no existe. Especifique una base de datos existente.|  
  
## <a name="explanation"></a>Explicación  
Una de las bases de datos que se especifican en la sugerencia USE PLAN no existe.  
  
## <a name="user-action"></a>Acción del usuario  
Asegúrese de que todas las bases de datos que se especifican en la sugerencia USE PLAN existen.  
  
## <a name="see-also"></a>Consulte también  
[Sugerencias de consulta &#40;Transact-SQL&#41;](~/t-sql/queries/hints-transact-sql-query.md)  
[Guías de plan](~/relational-databases/performance/plan-guides.md)  
  
