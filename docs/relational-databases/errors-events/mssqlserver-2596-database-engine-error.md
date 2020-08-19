---
description: MSSQLSERVER_2596
title: MSSQLSERVER_2596 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 2596 (Database Engine error)
ms.assetid: 49ab892f-8ba3-4ba1-b562-ddf205019802
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: ce3ed3f225671a762ba6e39f958c6347f813076f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88410861"
---
# <a name="mssqlserver_2596"></a>MSSQLSERVER_2596
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalles  
  
| Atributo | Value |  
| :-------- | :---- |  
|Nombre de producto|SQL Server|  
|Id. de evento|2596|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|DBCC_DATABASE_IN_READ_ONLY_MODE|  
|Texto del mensaje|Instrucción de reparación no procesada. La base de datos no puede estar en modo de solo lectura.|  
  
## <a name="explanation"></a>Explicación  
Este mensaje indica que la base de datos está en modo de solo lectura. No es posible llevar a cabo reparaciones cuando una base de datos está en modo de solo lectura.  
  
## <a name="user-action"></a>Acción del usuario  
Establezca la base de datos en modo de lectura y escritura mediante el uso de ALTER DATABASE y después vuelva a ejecutar el comando DBCC.  
  
## <a name="see-also"></a>Consulte también  
[ALTER DATABASE &#40;Transact-SQL&#41;](~/t-sql/statements/alter-database-transact-sql-set-options.md)  
  
