---
title: MSSQLSERVER_11409 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 11409 (Database Engine error)
ms.assetid: 99b71a1c-a72d-4ca9-9d00-4230c9042ba5
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: e8df350d50971d239dd166456b547e8e0f1af537
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85781250"
---
# <a name="mssqlserver_11409"></a>MSSQLSERVER_11409
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalles  
  
| Atributo | Value |  
| :-------- | :---- |  
|Nombre de producto|SQL Server|  
|Id. de evento|11409|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|ALTERCOL_COLSET_DROP|  
|Texto del mensaje|No se puede quitar el conjunto de columnas '%.*ls' de la tabla '%.\*ls' porque la tabla contiene más de 1025 columnas.|  
  
## <a name="explanation"></a>Explicación  
Las tablas pueden contener 1024 columnas, como máximo, que no estén designadas como dispersas o calculadas. Cuando las columnas dispersas hacen que la tabla supere el número de 1024 columnas, se debe definir un conjunto de columnas para la tabla. La tabla a la que se hace referencia tiene más de 1024 columnas y se ha intentado quitar el conjunto de columnas.  
  
## <a name="user-action"></a>Acción del usuario  
Con las columnas actuales en la tabla, debe conservar el conjunto de columnas.  
  
Para quitar el conjunto de columnas, primero debe quitar columnas de la tabla, hasta que haya menos de 1024. A continuación, puede quitar el conjunto de columnas.  
  
