---
title: MSSQLSERVER_2538 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 2538 (Database Engine error)
ms.assetid: 0a0f7d79-f1ba-4749-8804-fb660cca3492
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 16a79a049ea1b1beaba79ec94c980c73e9614a00
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85780308"
---
# <a name="mssqlserver_2538"></a>MSSQLSERVER_2538
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalles  
  
| Atributo | Value |  
| :-------- | :---- |  
|Nombre de producto|SQL Server|  
|Id. de evento|2538|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|DBCC_ALLOCATION_SUMMARY_PER_FILE|  
|Texto del mensaje|Archivo FILE. Número de extensiones = EXTENTS, páginas usadas = USED_PAGES, páginas reservadas = RESERVED_PAGES.|  
  
## <a name="explanation"></a>Explicación  
Esta información forma parte de la salida del comando DBCC CHECKALLOC. Esta información es el resumen por archivo de las extensiones asignadas, las páginas utilizadas y las páginas reservadas de la base de datos especificada.  
  
## <a name="user-action"></a>Acción del usuario  
None  
  
