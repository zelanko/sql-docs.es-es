---
title: Extensiones específicas en proceso SQL Server a ADO.NET | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: clr
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- data access [CLR integration]
- ADO.NET [CLR integration]
- common language runtime [SQL Server], ADO.NET
- database objects [CLR integration], in-process extensions
- in-process data access providers [CLR integration]
- extensions [CLR integration]
ms.assetid: 781b812e-eb14-472a-85fa-aa4cdb929bee
caps.latest.revision: 33
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 4d26ee079f507db9aebbf613e401726dbca2872b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sql-server-in-process-specific-extensions-to-adonet"></a>Extensiones específicas en proceso de SQL Server a ADO.NET
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Hay cuatro extensiones funcionales principales a ADO.NET que son específicamente para el uso en proceso. En los siguientes temas se tratan estas extensiones en detalle.  
  
## <a name="in-this-section"></a>En esta sección  
 [Objeto SqlContext](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqlcontext-object.md)  
 Esta clase proporciona acceso a las demás extensiones abstrayendo el contexto de llamador de una rutina de SQL Server que ejecuta el código administrado en proceso.  
  
 [Objeto SqlPipe](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqlpipe-object.md)  
 Esta clase contiene rutinas para enviar resultados tabulares y mensajes al cliente.  
  
 [Objeto SqlTriggerContext](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqltriggercontext-object.md)  
 Esta clase proporciona información sobre el contexto en el que se ejecuta un desencadenador.  
  
 [Objeto SqlDataRecord](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqldatarecord-object.md)  
 La clase SqlDataRecord representa una única fila de datos, junto con sus metadatos relacionados, y permite que los procedimientos almacenados devuelvan al cliente conjuntos de resultados personalizados.  
  
  
