---
title: MSSQLSERVER_945 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 945 (Database Engine error)
ms.assetid: ee501d13-0bd9-4627-896c-ed5b1bdb88b3
caps.latest.revision: 20
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: f06aed5f498ed67b7d9335cb37b62b1edb25327e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36107458"
---
# <a name="mssqlserver945"></a>MSSQLSERVER_945
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|945|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|DB_IS_SHUTDOWN|  
|Texto del mensaje|No se puede abrir la base de datos '%.*ls', porque no es posible tener acceso a archivos, o la memoria o el espacio en disco son insuficientes.  Compruebe el registro de errores de SQL Server para obtener más información.|  
  
## <a name="explanation"></a>Explicación  
 No se pudo obtener acceso a la base de datos porque faltan archivos u otros recursos.  
  
## <a name="user-action"></a>Acción del usuario  
 Compruebe el registro de errores para obtener información adicional acerca del error de memoria, espacio en disco o permiso. Confirme la ubicación de los archivos .mdf y .ndf de la base de datos afectada y confirme que la cuenta usada por [!INCLUDE[ssDE](../../includes/ssde-md.md)] tiene permiso de acceso a esos archivos. Después de corregir el problema, reinicie la base de datos usando ALTER DATABASE para establecerla en ONLINE.  
  
  