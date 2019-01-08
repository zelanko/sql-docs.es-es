---
title: Propiedades de orígenes OData | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 4fde5bb0-6d78-4ec4-8f0b-67f91c53fe99
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 46c44d1274271dfc826db44513b64b96f8ff9e57
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52766957"
---
# <a name="odata-source-properties"></a>Propiedades de orígenes OData
  Al hacer clic con el botón derecho en **Origen OData** en el flujo de datos y hacer clic en **Propiedades**, verá las propiedades del componente de **Origen OData** en la ventana **Propiedades**.  
  
|||  
|-|-|  
|Property|Descripción|  
|CollectionName|Nombre de la colección que desea recuperar del servicio OData. La propiedad **CollectionName** se usa cuando **UseResourcePath** es False.<br /><br /> Esta propiedad se puede incluir en expresiones, lo que permite establecer el valor en tiempo de ejecución. Sin embargo, si los metadatos de la colección no coinciden con los metadatos que se usaron en tiempo de diseño, se producirá un error de validación, lo que producirá un error en la ejecución del flujo de datos.|  
|DefaultStringLength|Este valor especifica la longitud predeterminada de las columnas de cadena que no tienen ninguna longitud máxima.<br /><br /> **Valor predeterminado:** 4000|  
|Consulta|Parámetros de consulta OData. Esta propiedad se puede incluir en expresiones y establecer en tiempo de ejecución.|  
|ResourcePath|Use esta propiedad cuando necesite especificar una ruta de acceso completa a recursos, en lugar de seleccionar simplemente el nombre de una colección. Esta propiedad se usa cuando **UseResourcePath** es True.|  
|UseResourcePath|Cuando se establece en True, el valor **ResourcePath** se anexa a la dirección URL base para determinar la ubicación de la fuente OData. Cuando se establece en False, se usa el valor **CollectionName** .<br /><br /> **Valor predeterminado:** False|  
  
  
