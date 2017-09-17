---
title: Importar datos de un origen de datos relacionales (SSAS Tabular) | Documentos de Microsoft
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
ms.assetid: 043201cc-fbef-4ed0-bde8-dc5e3a3e8bea
caps.latest.revision: 15
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1db6dd24d059f8c478967bc3c69652aaec0aeb51
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="import-data---relational-data-source"></a>Importar datos - origen de datos relacional
  Con el Asistente para la importación de tablas, puede importar datos desde una variedad de bases de datos relacionales. El asistente está disponible en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], en el menú **Modelo** . Para conectarse a un origen de datos, debe tener instalado en el equipo el proveedor adecuado. Para más información sobre los proveedores y los orígenes de datos admitidos, vea [Orígenes de datos compatibles &#40;SSAS tabular&#41;](../../analysis-services/tabular-models/data-sources-supported-ssas-tabular.md).  
  
 El Asistente para la importación de tablas permite importar datos de los orígenes de datos siguientes:  
  
 **Bases de datos relacionales**  
  
-   Base de datos de Microsoft SQL Server  
  
-   Microsoft SQL Azure  
  
-   Base de datos de Microsoft Access  
  
-   Almacenamiento de datos paralelo de Microsoft SQL Server  
  
-   Oracle  
  
-   Teradata  
  
-   Sybase  
  
-   Informix  
  
-   IBM DB2  
  
-   OLE DB/ODBC  
  
 **Orígenes multidimensionales**  
  
-   Cubo de Microsoft SQL Server Analysis Services  
  
 El Asistente para la importación de tablas no permite importar datos de un libro de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] como origen de datos.  
  
### <a name="to-import-data-from-a-database"></a>Para importar datos de una base de datos  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], haga clic en el menú **Modelo** y, a continuación, haga clic en **Importar desde el origen de datos**.  
  
2.  En la página **Conectarse a un origen de datos** , seleccione el tipo de base de datos con el que desea conectar y, a continuación, haga clic en **Siguiente**.  
  
3.  Siga los pasos en el Asistente para la importación de tablas. En las páginas siguientes, podrá seleccionar tablas y vistas específicas o aplicar filtros mediante la página **Seleccionar tablas y vistas** o mediante la creación de una consulta SQL en la página **Especificar una consulta SQL** .  
  
## <a name="see-also"></a>Vea también  
 [Importar datos &#40;SSAS tabular&#41;](http://msdn.microsoft.com/library/6617b2a2-9f69-433e-89e0-4c5dc92982cf)   
 [Orígenes de datos compatibles &#40;SSAS tabular&#41;](../../analysis-services/tabular-models/data-sources-supported-ssas-tabular.md)  
  
  
