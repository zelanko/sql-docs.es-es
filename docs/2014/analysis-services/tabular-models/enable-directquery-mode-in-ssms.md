---
title: Configurar el acceso in-Memory o DirectQuery para una base de datos de modelo tabular | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: a5d439a9-5be1-4145-90e8-90777d80e98b
author: minewiskan
ms.author: owend
ms.openlocfilehash: 145d5a0d32384a0bcea1d60d00dcf3988642229c
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84938916"
---
# <a name="configure-in-memory-or-directquery-access-for-a-tabular-model-database"></a>Configurar el acceso In-Memory o DirectQuery para una base de datos modelo tabular
  En este tema se describe cómo cambiar las propiedades de conexión de un modelo tabular que ya se haya implementado, para habilitar el uso del modelo en el modo Direct Query.  
  
 Para obtener más información sobre estas propiedades y la configuración de los escenarios más comunes, vea [escenarios de implementación de DirectQuery &#40;&#41;tabular de SSAS ](../directquery-deployment-scenarios-ssas-tabular.md).  
  
## <a name="requirements"></a>Requisitos  
 Habilitar el uso del modo Direct Query en un modelo tabular es un proceso de varias fases. Debe:  
  
1.  Asegurarse de que el modelo no tiene características que podrían ocasionar errores de validación en el modo Direct Query.  
  
2.  Cambiar el modo de almacenamiento en el modelo para admitir Direct Query.  
  
3.  Implementar el modelo en un modo que admita consultas en el modo Direct Query híbrido o puro.  
  
4.  Modificar la cadena de conexión en la base de datos implementada para admitir el modo Direct Query.  
  
 En este tema se supone que ha creado y ha validado el modelo, y solo necesita habilitar el acceso Direct Query desde un cliente como [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)].  
  
## <a name="procedure"></a>Procedimiento  
  
#### <a name="change-the-connection-string-properties-of-the-model"></a>Cambiar las propiedades de una cadena de conexión del modelo  
  
1.  En SQL Server Management Studio, abra la instancia en la que se implementó el modelo.  
  
2.  En Explorador de objetos, haga clic con el botón secundario en el nombre de la base de datos modelo y seleccione **propiedades**.  
  
3.  Busque la propiedad **DirectQueryMode**. Para habilitar el uso del origen de datos relacional, esta propiedad se debe establecer en uno de estos valores:  
  
    -   **DirectQuery**  
  
    -   **InMemoryWithDirectQuery**  
  
    -   **DirectQueryWithInMemory**  
  
  
