---
title: MSSQLSERVER_7916 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 7916 (Database Engine error)
ms.assetid: 9bac3536-de14-4e98-84c2-bde9a59ba0d1
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: eadb07e1f7add72d181546a3c1a74c9bbf6ca406
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85693966"
---
# <a name="mssqlserver_7916"></a>MSSQLSERVER_7916
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalles  
  
| Atributo | Value |  
| :-------- | :---- |  
|Nombre de producto|SQL Server|  
|Id. de evento|7916|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|DBCC2_REPAIR_RECORD|  
|Texto del mensaje|Reparación: se ha eliminado el registro para el id. de objeto O_ID, id. de índice I_ID, id. de partición PN_ID, id. de unidad de asignación A_ID (tipo TYPE), en la página P_ID, ranura S_ID. Se volverán a generar los índices.|  
  
## <a name="explanation"></a>Explicación  
Este es un mensaje informativo de REPAIR que indica que el registro especificado se eliminó de la página.  
  
## <a name="user-action"></a>Acción del usuario  
None  
  
