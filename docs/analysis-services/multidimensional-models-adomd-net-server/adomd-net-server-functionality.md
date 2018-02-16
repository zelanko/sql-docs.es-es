---
title: Funcionalidad de servidor ADOMD.NET | Documentos de Microsoft
ms.custom: 
ms.date: 02/14/2018
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- functionality [ADOMD.NET]
- ADOMD.NET, functionality
ms.assetid: b74c6957-3f64-4e09-aa09-d06ee93f82fa
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 4eda9ee6f9bed6af7990e001b12844c55d419358
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/15/2018
---
# <a name="adomdnet-server-functionality"></a>Funcionalidad del servidor de ADOMD.NET
  Todos los objetos de servidor de ADOMD.NET proporcionan acceso de solo lectura a los datos y metadatos del servidor. Para recuperar datos y metadatos, utilice el modelo de objetos del servidor ADOMD.NET, ya que el modelo de objetos de servidor no admite conjuntos de filas de esquema.  
  
 Con objetos de servidor ADOMD.NET, puede crear una función definida por el usuario (UDF) o un procedimiento almacenado para [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Para llamar a estos métodos incrustados se utilizan instrucciones de consulta creadas en lenguajes como MDX (Expresiones multidimensionales), DMX (Extensiones de minería de datos) o SQL. Estos métodos incrustados también proporcionan otras funciones sin las latencias asociadas a las comunicaciones de red.  
  
> [!NOTE]  
>  El objeto <xref:Microsoft.AnalysisServices.AdomdServer.AdomdCommand> solamente admite DMX.  
  
## <a name="what-is-a-udf"></a>¿Qué es una UDF?  
 A *UDF* es un método que tiene las siguientes características:  
  
-   Puede llamar a la UDF en el contexto de una consulta.  
  
-   La UDF puede aceptar un número cualquiera de parámetros.  
  
-   La UDF puede devolver varios tipos de datos.  
  
 En el ejemplo siguiente se utiliza una UDF ficticia, `FinalSalesNumber`:  
  
```  
SELECT SalesPerson.Name ON ROWS,  
       FinalSalesNumber() ON COLUMNS  
FROM SalesModel  
```  
  
## <a name="what-is-a-stored-procedure"></a>¿Qué es un procedimiento almacenado?  
 A *procedimiento almacenado* es un método que tiene las siguientes características:  
  
-   Se llama a un procedimiento almacenado en su propio con el MDX [llamar](../../mdx/mdx-data-manipulation-call.md) instrucción.  
  
-   Un procedimiento almacenado puede aceptar un número cualquiera de parámetros.  
  
-   Un procedimiento almacenado puede devolver un conjunto de datos, un **IDataReader**, o un resultado vacío.  
  
 En el ejemplo siguiente se utiliza un procedimiento almacenado ficticio, `FinalSalesNumbers`:  
  
```  
CALL FinalSalesNumbers()  
```  
  
## <a name="see-also"></a>Vea también  
 [Programación del servidor ADOMD.NET](../../analysis-services/multidimensional-models-adomd-net-server/adomd-net-server-programming.md)  
  
  
