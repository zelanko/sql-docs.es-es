---
title: Agregar una tabla | Documentos de Microsoft
ms.custom: ''
ms.date: 02/21/2018
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: d713c432-db99-4983-acc1-52b0fdd58bd6
caps.latest.revision: 5
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 266a0a8c236d3b765f98e68805f73ce6a12270df
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="add-a-table"></a>Agregar una tabla
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  En este artículo se describe cómo agregar una tabla de un origen de datos desde el que ha importado datos previamente en el modelo. Para agregar una tabla del mismo origen de datos, puede usar la conexión de origen de datos existente. Se recomienda usar siempre una conexión única al importar cualquier número de tablas de un origen de datos único.  
  
### <a name="to-add-a-table-from-an-existing-data-source"></a>Para agregar una tabla de un origen de datos existente  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], haga clic en el menú **Modelo** y, a continuación, en **Conexiones existentes**.  
  
2.  En la página **Conexiones existentes** , seleccione la conexión al origen de datos que tiene la tabla que desea agregar y haga clic en **Abrir**.  
  
3.  En la página **Seleccionar tablas y vistas** , seleccione la tabla del origen de datos que desea agregar al modelo.  
  
    > [!NOTE]  
    >  En la página **Seleccionar tablas y vistas** no se mostrarán las tablas que se importaron previamente como activadas.  Si selecciona una tabla que se importó previamente con esta conexión y no proporcionó a la tabla un nombre descriptivo diferente, se agrega un 1 al nombre descriptivo. No tiene que volver a seleccionar las tablas que se importaron previamente con esta conexión.  
  
4.  En caso necesario, use **Vista previa y filtro** para seleccionar solo algunas columnas o para aplicar filtros a los datos que se van a importar.  
  
5.  Haga clic en **Finalizar** para importar la nueva tabla.  
  
> [!NOTE]  
>  Cuando se importan varias tablas al mismo tiempo desde un único origen de datos, las relaciones entre dichas tablas en el origen se crean automáticamente en el modelo. Sin embargo, cuando posteriormente agregue una tabla, es posible que tenga que crear las relaciones manualmente en el modelo entre las tablas recién agregadas y las tablas que se importaron previamente.  
  
## <a name="see-also"></a>Vea también  
 [Importar datos](http://msdn.microsoft.com/library/6617b2a2-9f69-433e-89e0-4c5dc92982cf)   
 [Eliminar una tabla](../../analysis-services/tabular-models/delete-a-table-ssas-tabular.md)  
  
  
