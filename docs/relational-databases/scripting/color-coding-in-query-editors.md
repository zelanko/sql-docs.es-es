---
title: Codificación de colores en el Editor de consultas | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssms-scripting
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Query Editor [SQL Server Management Studio], color coding
- color coding [Query Editor]
ms.assetid: 802882dc-c997-4e3f-8a01-994bb43169ae
caps.latest.revision: 33
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: b51afacfd047298f5f498bf956e9a70443ad71c7
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="color-coding-in-query-editors"></a>Codificación de colores en el Editor de consultas
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  El texto especificado en los editores de código se asigna a una categoría; cada categoría está identificada por un color. Los colores ayudan a encontrar texto rápidamente en el código. Por ejemplo, los comentarios se resaltan en verde oscuro. En la tabla siguiente se muestran los colores más comunes. Puede ver la lista completa de colores y sus categorías, así como configurar una combinación de colores personalizada, usando el menú **Herramientas**, **Opciones** . Para obtener más información sobre cómo cambiar los colores predeterminados, vea [Change Font Color, Size, and Style](../../relational-databases/scripting/change-font-color-size-and-style.md).  
  
## <a name="default-code-colors"></a>Colores predeterminados para el código  
  
|Color|Categoría|  
|-----------|--------------|  
|Rojo|Cadena de SQL|  
|Verde oscuro|Comentario|  
|Negro sobre fondo plateado|Comando SQLCMD|  
|Fucsia|Función del sistema|  
|Verde|Tabla, vista o función con valores de tabla del sistema. También, los esquemas del sistema sys e INFORMATION_SCHEMA.|  
|Azul|Palabra clave|  
|Verde azulado|Números de línea o parámetro de plantilla|  
|Rojo oscuro|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] procedimiento almacenado|  
|Gris oscuro|Operadores|  
  
## <a name="status-bar"></a>Barra de estado  
 Puede configurar que servidores registrados o servidores de [!INCLUDE[ssDE](../../includes/ssde-md.md)] en el Explorador de objetos tengan distintos colores en la barra de estado del editor de consultas de [!INCLUDE[ssDE](../../includes/ssde-md.md)] . Esto ayuda a identificar a qué servidor está conectada cada ventana del editor cuando se tienen muchas ventanas abiertas al mismo tiempo. Para obtener más información sobre cómo establecer colores de la barra de estado, vea [Barra de estado &#40;Editor de consultas del motor de base de datos&#41;](../../relational-databases/scripting/status-bar-database-engine-query-editor.md).  
  
 Algunos tipos de editores no muestran la barra de estado o no admiten varios colores.  
  
  
