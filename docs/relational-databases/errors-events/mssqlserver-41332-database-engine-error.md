---
title: MSSQLSERVER_41332 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 41332 (Database Engine error)
ms.assetid: d3403c3e-d178-4006-b6c9-c18609562db5
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 6a0ae51ca0aea57f454446301f0e624298f146e5
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85694279"
---
# <a name="mssqlserver_41332"></a>MSSQLSERVER_41332
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalles  
  
| Atributo | Value |  
| :-------- | :---- |  
|Nombre de producto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|Id. de evento|41332|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|SQL_SNAPSHOT_NOT_SUPPORTED|  
|Texto del mensaje|No se puede tener acceso ni crear tablas optimizadas en memoria ni procedimientos almacenados compilados de forma nativa cuando la configuración de TRANSACTION ISOLATION LEVEL para la sesión se ha establecido en SNAPSHOT.|  
  
## <a name="explanation"></a>Explicación  
La transacción se inició con el nivel de aislamiento de instantánea y luego se intentó utilizar una función incompatible.  
  
## <a name="user-action"></a>Acción del usuario  
Inicie la transacción con otro nivel de aislamiento. Para obtener más información, vea [OLTP en memoria &#40;optimización en memoria&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  
  
## <a name="see-also"></a>Consulte también  
[OLTP en memoria &#40;optimización en memoria&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
