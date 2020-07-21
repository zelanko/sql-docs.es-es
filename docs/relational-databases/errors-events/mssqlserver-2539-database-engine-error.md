---
title: MSSQLSERVER_2539 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 2539 (Database Engine error)
ms.assetid: e638efcc-56f4-40f9-9740-17ef67b47d79
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: d270c016d60be484e6dbd81127006e56572a3cb6
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85780293"
---
# <a name="mssqlserver_2539"></a>MSSQLSERVER_2539
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalles  
  
| Atributo | Value |  
| :-------- | :---- |  
|Nombre de producto|SQL Server|  
|Id. de evento|2539|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|DBCC_ALLOCATION_SUMMARY_FOR_DATABASE|  
|Texto del mensaje|El número total de extensiones = EXTENTS, páginas usadas = USED_PAGES y páginas reservadas = RESERVED_PAGES de esta base de datos.|  
  
## <a name="explanation"></a>Explicación  
Esta información forma parte de la salida del comando DBCC CHECKALLOC. Esta información es el resumen de las extensiones asignadas, las páginas usadas y las páginas reservadas de la base de datos especificada.  
  
## <a name="user-action"></a>Acción del usuario  
None  
  
