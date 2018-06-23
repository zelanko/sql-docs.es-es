---
title: MSSQLSERVER_15661 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 15661 (Database Engine error)
ms.assetid: 88b01bfb-74ce-4aa0-aec0-7885261c7ef3
caps.latest.revision: 12
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 7b407f652dc2ef9bcca807c359120166d5f31f89
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36103550"
---
# <a name="mssqlserver15661"></a>MSSQLSERVER_15661
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|15661|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|SQLErrorNum15661|  
|Texto del mensaje|El procedimiento almacenado sp_estimate_data_compression_savings no se puede utilizar para las tablas temporales.|  
  
## <a name="explanation"></a>Explicación  
 Se utilizó una tabla temporal como argumento para el procedimiento almacenado sp_estimate_data_compression_savings. Aunque se admite la compresión de tablas temporales, no se puede utilizar sp_estimate_data_compression_savings para estimar los ahorros obtenidos con la compresión.  
  
## <a name="user-action"></a>Acción del usuario  
 Quite la tabla temporal como argumento para sp_estimate_data_compression_savings.  
  
  