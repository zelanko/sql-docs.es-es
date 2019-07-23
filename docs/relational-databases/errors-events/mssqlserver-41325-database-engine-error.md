---
title: MSSQLSERVER_41325 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 41325 (Database Engine error)
ms.assetid: 97c6a8bb-139a-44f3-9ed5-f46d047e8ed3
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: fadfc5afc9e45b8c09591e2c133343146a5fbe99
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68123362"
---
# <a name="mssqlserver41325"></a>MSSQLSERVER_41325
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|Identificador del evento|41325|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|HK_TX_COMMIT_SR_VALIDATION|  
|Texto del mensaje|La transacción actual no pudo confirmarse debido a un error serializable de validación.|  
  
## <a name="explanation"></a>Explicación  
La transacción encontró un error de validación y ahora está condenada.  
  
## <a name="user-action"></a>Acción del usuario  
Vuelva a intentar la transacción con error. Para obtener más información, vea [OLTP en memoria &#40;optimización en memoria&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  
  
## <a name="see-also"></a>Consulte también  
[OLTP en memoria &#40;optimización en memoria&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
