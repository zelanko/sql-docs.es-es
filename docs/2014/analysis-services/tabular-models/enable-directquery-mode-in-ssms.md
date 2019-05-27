---
title: Configurar el acceso de DirectQuery para una base de datos de modelo Tabular o en memoria | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: a5d439a9-5be1-4145-90e8-90777d80e98b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 55a1a296e6a7b2a2155dea590be9321b22e73451
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66067193"
---
# <a name="configure-in-memory-or-directquery-access-for-a-tabular-model-database"></a>Configurar el acceso In-Memory o DirectQuery para una base de datos modelo tabular
  En este tema se describe cómo cambiar las propiedades de conexión de un modelo tabular que ya se haya implementado, para habilitar el uso del modelo en el modo Direct Query.  
  
 Para obtener más información acerca de estas propiedades y configuración para los escenarios más comunes, consulte [escenarios de implementación de DirectQuery &#40;Tabular de SSAS&#41;](../directquery-deployment-scenarios-ssas-tabular.md).  
  
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
  
2.  En el Explorador de objetos, haga clic en el nombre de la base de datos modelo y seleccione **propiedades**.  
  
3.  Busque la propiedad **DirectQueryMode**. Para habilitar el uso del origen de datos relacional, esta propiedad se debe establecer en uno de estos valores:  
  
    -   **DirectQuery**  
  
    -   **InMemoryWithDirectQuery**  
  
    -   **DirectQueryWithInMemory**  
  
  
