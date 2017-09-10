---
title: Importar datos de un origen de datos multidimensionales (SSAS Tabular) | Documentos de Microsoft
ms.custom: 
ms.date: 05/22/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 7f0793ea-a4c7-42e9-b722-2164a454ebca
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4aaa43e745c86cd493279fe8bd875d376f8185c0
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="import-data---multidimensional-data-source"></a>Importar datos - origen de datos Multidimensional
  Puede usar una base de datos de cubo de Analysis Services como origen de datos para un modelo tabular. Para importar datos de un cubo de Analysis Services, debe definir una consulta MDX para seleccionar los datos que desea importar.  
  
 Cualquier dato contenido en una base de datos de SQL Server Analysis Services se puede importar en un modelo. Puede extraer todo el contenido o parte de una dimensión, u obtener segmentos y agregados del cubo, como la suma de ventas, mes a mes, durante el año actual, etc. No obstante, debería tener presente que todos los datos que se importan de un cubo pierden la información de estructura jerárquica. Por consiguiente, si define una consulta que recupera medidas a lo largo de varias dimensiones, los datos se importarán con cada dimensión en una columna independiente.  
  
 Los cubos de Analysis Services deben ser de la versión SQL Server 2005, SQL Server 2008, SQL Server 2008 R2, [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]o [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)].  
  
### <a name="to-import-data-from-an-analysis-services-cube"></a>Para importar datos de un cubo de Analysis Services  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], haga clic en el menú **Modelo** y, a continuación, haga clic en **Importar desde el origen de datos**.  
  
2.  En la página **Conectarse a un origen de datos** , seleccione **Microsoft Analysis Services**y, a continuación, haga clic en **Siguiente**.  
  
3.  Siga los pasos en el Asistente para la importación de tablas. Podrá especificar una consulta MDX en la página de **Especificar una consulta MDX** . Para usar el Diseñador de consultas MDX, haga clic en **Diseño**en la página Especificar una consulta MDX.  
  
## <a name="see-also"></a>Vea también  
 [Importar datos &#40;SSAS tabular&#41;](http://msdn.microsoft.com/library/6617b2a2-9f69-433e-89e0-4c5dc92982cf)   
 [Orígenes de datos compatibles &#40;SSAS tabular&#41;](../../analysis-services/tabular-models/data-sources-supported-ssas-tabular.md)  
  
  
