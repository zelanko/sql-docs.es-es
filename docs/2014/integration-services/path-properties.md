---
title: Propiedades de ruta de acceso | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- paths [Integration Services], properties
ms.assetid: 89b1e347-9579-4f6b-af74-c6519ea08eea
caps.latest.revision: 25
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 9d5917edcf5038028075d0f71b70a8e90acc53d7
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37285431"
---
# <a name="path-properties"></a>Propiedades de la ruta de acceso
  Los objetos de flujo de datos del modelo de objetos de [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] tienen propiedades comunes y propiedades personalizadas en el nivel del componente, de las entradas y salidas, y de las columnas de entrada y de salida. Muchas propiedades tienen valores de solo lectura que son asignados en tiempo de ejecución por el motor de flujo de datos.  
  
 En este tema se enumeran y describen las propiedades personalizadas de las rutas de acceso que conectan los objetos del flujo de datos.  
  
## <a name="path-properties"></a>Propiedades de la ruta de acceso  
 En el modelo de objetos de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], una ruta de acceso que conecta componentes en el flujo de datos implementa la interfaz <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSPath100>.  
  
 La tabla siguiente describe las propiedades configurables de las rutas de acceso en un flujo de datos. El motor de flujo de datos también asigna valores a propiedades de solo lectura adicionales no enumeradas aquí.  
  
|Nombre de propiedad|Tipo de datos|Descripción|  
|-------------------|---------------|-----------------|  
|PathAnnotation|Integer (enumeración)|Un valor que indica si una anotación se debería mostrar con la ruta de acceso en el área del diseñador. Los valores posibles son `AsNeeded`, `SourceName`, `PathName`, y `Never`. El valor predeterminado es `AsNeeded`.|  
|DestinationName|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSInput100>|La entrada asociada a la ruta de acceso.|  
|SourceName|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutput100>|La salida asociada a la ruta de acceso.|  
  
## <a name="see-also"></a>Vea también  
 [Rutas de Integration Services](data-flow/integration-services-paths.md)   
 [Propiedades comunes](../../2014/integration-services/common-properties.md)   
 [Propiedades personalizadas de transformación](data-flow/transformations/transformation-custom-properties.md)   
 [Propiedades de flujo de datos que se pueden establecer utilizando expresiones](../../2014/integration-services/data-flow-properties-that-can-be-set-by-using-expressions.md)  
  
  
