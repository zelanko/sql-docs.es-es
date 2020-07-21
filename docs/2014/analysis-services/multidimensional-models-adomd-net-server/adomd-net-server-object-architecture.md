---
title: Arquitectura de objetos de servidor ADOMD.NET | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- ADOMD.NET, object model
- object model [ADOMD.NET]
ms.assetid: bdc81de9-b390-4654-b62a-cd6c0c9ca10d
author: minewiskan
ms.author: owend
ms.openlocfilehash: 33a8f420f985c9e62c7d7f275e7de370a6988e8d
ms.sourcegitcommit: 04ba0ed3d860db038078609d6e348b0650739f55
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/27/2020
ms.locfileid: "85469060"
---
# <a name="adomdnet-server-object-architecture"></a>Arquitectura de objetos de servidor ADOMD.NET
  Los objetos de servidor ADOMD.NET son objetos auxiliares que se pueden usar para crear funciones definidas por el usuario (UDF) o procedimientos almacenados en [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
> [!NOTE]  
>  Para utilizar el espacio de nombres `Microsoft.AnalysisServices.AdomdServer` (y estos objetos), debe agregarse una referencia a msmgdsrv.dll en el proyecto de UDF o procedimiento almacenado.  
  
 ![Muestra las relaciones de objetos en el servidor ADOMD.NET](../../analysis-services/dev-guide/media/adomdnetserverobjectmodel.gif "Muestra las relaciones de objetos en el servidor ADOMD.NET")  
Modelo de objetos ADOMD.NET  
  
 La interacción con la jerarquía de objetos ADOMD.NET suele comenzar con uno o más de los objetos del nivel superior, como se describe en la tabla siguiente.  
  
|A|Utilice este objeto|  
|--------|---------------------|  
|Evaluar expresiones MDX (Expresiones multidimensionales)|[Microsoft. AnalysisServices. AdomdServer. Expression](/previous-versions/sql/sql-server-2014/ms143609(v=sql.120))<br /> El objeto [Microsoft. AnalysisServices. AdomdServer. Expression](/previous-versions/sql/sql-server-2014/ms143609(v=sql.120)) proporciona una manera de ejecutar una expresión MDX y evaluar esa expresión en una tupla especificada.|  
|Proporcionar compatibilidad para la ejecución de funciones MDX sin construir la instrucción MDX completa|[Microsoft. AnalysisServices. AdomdServer. MDX](/previous-versions/sql/sql-server-2014/ms143616(v=sql.120))<br /> El objeto [Microsoft. AnalysisServices. AdomdServer. MDX](/previous-versions/sql/sql-server-2014/ms143616(v=sql.120)) es práctico para llamar a funciones MDX predefinidas sin usar el objeto [Microsoft. AnalysisServices. AdomdServer. Expression](/previous-versions/sql/sql-server-2014/ms143609(v=sql.120)) . Las funciones adicionales para el objeto [Microsoft. AnalysisServices. AdomdServer. MDX](/previous-versions/sql/sql-server-2014/ms143616(v=sql.120)) deben estar disponibles en futuras versiones.|  
|Representar el contexto de ejecución actual de la UDF|[Microsoft. AnalysisServices. AdomdServer. Context](/previous-versions/sql/sql-server-2014/ms143353(v=sql.120))<br /> El objeto [Microsoft. AnalysisServices. AdomdServer. Context](/previous-versions/sql/sql-server-2014/ms143353(v=sql.120)) expone información como el cubo o el modelo de minería de datos actual y diversas colecciones de metadatos. Un uso clave del objeto [Microsoft. AnalysisServices. AdomdServer. Context](/previous-versions/sql/sql-server-2014/ms143353(v=sql.120)) es la propiedad [Microsoft. AnalysisServices. AdomdServer. hierarchy. CurrentMember *](/previous-versions/sql/sql-server-2014/ms137044(v=sql.120)) del objeto [Microsoft. AnalysisServices. AdomdServer. Hierarchy](/previous-versions/sql/sql-server-2014/ms143578(v=sql.120)) . Este uso clave permite que el autor de la UDF o el procedimiento almacenado tome decisiones en función del miembro de cierta dimensión sobre el que se realiza la consulta.|  
|Crear conjuntos y tuplas|[Microsoft. AnalysisServices. AdomdServer. SetBuilder](/previous-versions/sql/sql-server-2014/ms144510(v=sql.120)), [Microsoft. AnalysisServices. AdomdServer. TupleBuilder](/previous-versions/sql/sql-server-2014/ms145407(v=sql.120))<br /> [Microsoft. AnalysisServices. AdomdServer. SetBuilder](/previous-versions/sql/sql-server-2014/ms144510(v=sql.120)) proporciona una manera de crear conjuntos inmutables, mientras que [Microsoft. AnalysisServices. AdomdServer. TupleBuilder](/previous-versions/sql/sql-server-2014/ms145407(v=sql.120)) proporciona una manera de crear tuplas inmutables.|  
|Admitir la conversión implícita entre los seis tipos básicos del lenguaje MDX|[Microsoft. AnalysisServices. AdomdServer. MDXValue](/previous-versions/sql/sql-server-2014/ms143573(v=sql.120))<br /> El objeto [Microsoft. AnalysisServices. AdomdServer. MDXValue](/previous-versions/sql/sql-server-2014/ms143573(v=sql.120)) proporciona conversión y conversión implícita entre los tipos siguientes:<br /><br /> -   [Microsoft. AnalysisServices. AdomdServer. hierarchy](/previous-versions/sql/sql-server-2014/ms143578(v=sql.120))<br />-   [Microsoft. AnalysisServices. AdomdServer. LEVEL](/previous-versions/sql/sql-server-2014/ms143581(v=sql.120))<br />-   [Microsoft. AnalysisServices. AdomdServer. Member](/previous-versions/sql/sql-server-2014/ms143820(v=sql.120))<br />-   [Microsoft. AnalysisServices. AdomdServer. Tuple](/previous-versions/sql/sql-server-2014/ms145330(v=sql.120))<br />-   [Microsoft. AnalysisServices. AdomdServer. Set](/previous-versions/sql/sql-server-2014/ms144530(v=sql.120))<br />-Tipos de valor escalar o|  
  
## <a name="see-also"></a>Consulte también  
 [Programación del servidor ADOMD.NET](https://docs.microsoft.com/bi-reference/adomd/multidimensional-models-adomd-net-server/adomd-net-server-programming)  
  
  
