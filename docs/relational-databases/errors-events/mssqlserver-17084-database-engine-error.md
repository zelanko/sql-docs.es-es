---
description: MSSQLSERVER_17084
title: MSSQLSERVER_17084 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 17084 (Database Engine error)
ms.assetid: e579d104-3307-4edd-8587-b14ecbc02ed9
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: bf44aa95cca35e56f836306f7870bd2c2de9be7a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471117"
---
# <a name="mssqlserver_17084"></a>MSSQLSERVER_17084
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalles  
  
| Atributo | Value |  
| :-------- | :---- |  
|Nombre de producto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|Id. de evento|17084|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|P3_ATOMIC_WITH_MISSING_OPTION|  
|Texto del mensaje|La cláusula WITH de la instrucción BEGIN ATOMIC debe especificar un valor para la opción '%ls'.|  
  
## <a name="explanation"></a>Explicación  
La cláusula WITH de la instrucción BEGIN ATOMIC no especificó un valor para una opción.  
  
## <a name="user-action"></a>Acción del usuario  
Los bloques **ATOMIC** requieren valores para las opciones **WITH** **TRANSACTION ISOLATION LEVEL** y **LANGUAGE**. Por ejemplo:  
  
```  
BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE= N'us_english')  
```  
  
Para obtener más información, vea [OLTP en memoria &#40;optimización en memoria&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  
  
## <a name="see-also"></a>Consulte también  
[OLTP en memoria &#40;optimización en memoria&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
