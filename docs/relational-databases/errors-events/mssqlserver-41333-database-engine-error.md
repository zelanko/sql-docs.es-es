---
title: MSSQLSERVER_41333 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 41333 (Database Engine error)
ms.assetid: c3c3ae9a-1e4c-4de6-ba72-2f393375b053
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: a459a23e9f74f04baed73c24c25c1757fbcc047f
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85694134"
---
# <a name="mssqlserver_41333"></a>MSSQLSERVER_41333
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalles  
  
| Atributo | Value |  
| :-------- | :---- |  
|Nombre de producto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|Id. de evento|41333|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|CROSS_CONTAINER_ISOLATION_FAILURE|  
|Texto del mensaje|Las siguientes transacciones deben acceder a tablas optimizadas para memoria y a procedimientos almacenados compilados de forma nativa en el aislamiento de instantáneas: transacciones RepeatableRead, transacciones Serializable y transacciones que accedan a las tablas que no estén optimizadas para memoria en aislamiento RepeatableRead o Serializable.|  
  
## <a name="explanation"></a>Explicación  
Hay restricciones respecto al usuario de los niveles de aislamiento mayores entre las transacciones basadas en disco y las transacciones XTP.  
  
## <a name="user-action"></a>Acción del usuario  
No intente operaciones de aislamiento alto nivel de las tablas optimizadas en memoria (y procedimientos compilados de forma nativa) y las tablas basadas en disco.  
  
Para obtener más información, vea [OLTP en memoria &#40;optimización en memoria&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  
  
## <a name="see-also"></a>Consulte también  
[OLTP en memoria &#40;optimización en memoria&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
