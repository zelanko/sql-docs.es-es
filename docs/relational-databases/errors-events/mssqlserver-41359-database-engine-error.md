---
title: MSSQLSERVER_41359 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 41359 (Database Engine error)
ms.assetid: 02b717c7-9170-4676-b0f6-4dec9eb5b5d4
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: b5372ffbeed279bf8c2c2f3adc8ad00dd8436fe3
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85765323"
---
# <a name="mssqlserver_41359"></a>MSSQLSERVER_41359
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalles  
  
| Atributo | Value |  
| :-------- | :---- |  
|Nombre de producto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|Id. de evento|41359|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|SQL_READ_COMMITTED_SNAPSHOT_NOT_SUPPORTED|  
|Texto del mensaje|Una consulta que tiene acceso a las tablas optimizadas en memoria con el nivel de aislamiento READ COMMITTED no puede tener acceso a las tablas basadas en disco cuando la opción de base de datos READ_COMMITTED_SNAPSHOT está establecida en ON. Proporciona un nivel de aislamiento admitido para la tabla optimizada en memoria mediante una sugerencia de tabla, como WITH (SNAPSHOT).|  
  
## <a name="explanation"></a>Explicación  
La base de datos con READ_COMMITTED_SNAPSHOT=ON no admite las transacciones que tienen acceso a las tablas optimizadas en memoria a las y tablas basadas en disco.  
  
## <a name="user-action"></a>Acción del usuario  
Establezca READ_COMMITTED_SNAPSHOT en OFF o proporcione un nivel de aislamiento admitido para la tabla optimizada en memoria mediante una sugerencia de nivela de tabla, como WITH (SNAPSHOT). Para obtener más información, vea [OLTP en memoria &#40;optimización en memoria&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  
  
## <a name="see-also"></a>Consulte también  
[OLTP en memoria &#40;optimización en memoria&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
