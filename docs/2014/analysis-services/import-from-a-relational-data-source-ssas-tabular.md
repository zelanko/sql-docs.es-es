---
title: Importar desde un origen de datos relacionales (SSAS Tabular) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 043201cc-fbef-4ed0-bde8-dc5e3a3e8bea
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 61fb30ea21ea810eab8d30a3a040fac4a1bd2128
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66080532"
---
# <a name="import-from-a-relational-data-source-ssas-tabular"></a>Importar datos de un origen de datos relacionales (SSAS tabular)
  Con el Asistente para la importación de tablas, puede importar datos desde una variedad de bases de datos relacionales. El asistente está disponible en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], en el menú **Modelo** . Para conectarse a un origen de datos, debe tener instalado en el equipo el proveedor adecuado. Para más información sobre los proveedores y los orígenes de datos admitidos, vea [Data Sources Supported &#40;SSAS Tabular&#41;](tabular-models/data-sources-supported-ssas-tabular.md).  
  
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
  
 El Asistente para la importación de tablas no permite importar datos de un libro de [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] como origen de datos.  
  
### <a name="to-import-data-from-a-database"></a>Para importar datos de una base de datos  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], haga clic en el menú **Modelo** y, a continuación, haga clic en **Importar desde el origen de datos**.  
  
2.  En la página **Conectarse a un origen de datos** , seleccione el tipo de base de datos con el que desea conectar y, a continuación, haga clic en **Siguiente**.  
  
3.  Siga los pasos en el Asistente para la importación de tablas. En las páginas siguientes, podrá seleccionar tablas y vistas específicas o aplicar filtros mediante la página **Seleccionar tablas y vistas** o mediante la creación de una consulta SQL en la página **Especificar una consulta SQL** .  
  
## <a name="see-also"></a>Vea también  
 [Importar datos &#40;SSAS tabular&#41;](import-data-ssas-tabular.md)   
 [Orígenes de datos compatibles &#40;SSAS tabular&#41;](tabular-models/data-sources-supported-ssas-tabular.md)  
  
  
