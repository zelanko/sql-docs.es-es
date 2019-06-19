---
title: MSSQLSERVER_21889 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 21889 (Database Engine error)
ms.assetid: ae199540-7986-4cc2-b782-cd22793236d3
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 635205cbc92121034cd8c949382c4910c794b55e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63045843"
---
# <a name="mssqlserver21889"></a>MSSQLSERVER_21889
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|21889|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|SQLErrorNum21889|  
|Texto del mensaje|La instancia de SQL Server "%s" no es un publicador de replicación. Ejecute **sp_adddistributor** en la instancia de SQL Server "%s" con el distribuidor "%s" a fin de habilitar la instancia para hospedar la base de datos de publicación "%s". Asegúrese de especificar el mismo inicio de sesión y contraseña que se usarán para el publicador original.|  
  
## <a name="explanation"></a>Explicación  
Para hospedar la base de datos del publicador, la instancia de SQL Server debe ser un publicador de replicación. **sp_validate_redirected_publisher** llama a **sp_helpdistributor** en el servidor remoto para determinar si el servidor es un publicador de replicación. Este error indica que la instancia de destino de SQL Server no es un publicador de replicación.  
  
## <a name="user-action"></a>Acción del usuario  
Ejecute **sp_adddistributor** en la instancia de SQL Server que hospeda la base de datos del publicador. Al ejecutar **sp_adddistributor**, especifique el distribuidor correcto. Use el mismo valor para el parámetro *@password* que se usó cuando se ejecutó **sp_adddistributor** inicialmente en el distribuidor.  
  
