---
title: Propiedades de orígenes OData | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 4fde5bb0-6d78-4ec4-8f0b-67f91c53fe99
author: chugugrace
ms.author: chugu
ms.openlocfilehash: fe4a3c3d1375095a4766186e1b854ea038b54ac9
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/22/2020
ms.locfileid: "86920807"
---
# <a name="odata-source-properties"></a>Propiedades de orígenes OData

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


Al hacer clic con el botón derecho en **Origen OData** en el flujo de datos y hacer clic en **Propiedades**, verá las propiedades del componente de **Origen OData** en la ventana **Propiedades**.  

## <a name="properties"></a>Propiedades 

|Propiedad|Descripción|  
|-|-|  
|CollectionName|Nombre de la colección que se va a recuperar del servicio OData. La propiedad **CollectionName** se usa cuando **UseResourcePath** es False.<br /><br /> Esta propiedad se puede incluir en expresiones, lo que permite establecer el valor en tiempo de ejecución. Sin embargo, si los metadatos de la colección no coinciden con los metadatos que se usaron en tiempo de diseño, se producirá un error de validación, lo que producirá un error en la ejecución del flujo de datos.|  
|DefaultStringLength|Este valor especifica la longitud predeterminada de las columnas de cadena que no tienen ninguna longitud máxima.<br /><br /> **Valor predeterminado:** 4000|  
|Consultar|Parámetros de consulta OData. Esta propiedad se puede incluir en expresiones y establecer en tiempo de ejecución.|  
|ResourcePath|Use esta propiedad cuando necesite especificar una ruta de acceso completa a recursos, en lugar de seleccionar simplemente el nombre de una colección. Esta propiedad se usa cuando **UseResourcePath** es True.|  
|UseResourcePath|Cuando se establece en True, el valor **ResourcePath** se anexa a la dirección URL base para determinar la ubicación de la fuente OData. Cuando se establece en False, se usa el valor **CollectionName** .<br /><br /> **Valor predeterminado:** False|  
  
## <a name="see-also"></a>Consulte también
[Origen OData](odata-source.md)
