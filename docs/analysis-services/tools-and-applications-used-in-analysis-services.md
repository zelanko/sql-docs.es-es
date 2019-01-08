---
title: Herramientas y aplicaciones utilizadas en Analysis Services | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8d3ecb5de4c70c09bc367b9008f5d62c6a23faef
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/11/2018
ms.locfileid: "53210081"
---
# <a name="tools-and-applications-used-in-analysis-services"></a>Herramientas y aplicaciones utilizadas en Analysis Services
[!INCLUDE[ssas-appliesto-sqlas-aas](../includes/ssas-appliesto-sqlas-aas.md)]

  Encuentre las herramientas y las aplicaciones que necesitará para la creación de modelos de Analysis Services y administración de bases de datos implementadas.  
  
## <a name="analysis-services-model-designers"></a>Diseñadores de modelo de Analysis Services  
 Los modelos se crean mediante el uso de plantillas de proyecto en SQL Server Data Tools (SSDT), un shell de Visual Studio. Plantillas de proyecto proporcionan los diseñadores de modelos para crear los objetos de modelo de datos que componen una solución de Analysis Services. SSDT es una descarga web gratuita que se actualiza mensualmente.

 **[Descargar SQL Server Data Tools (SSDT)](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt)** 
  
 Los modelos tienen una configuración de nivel de compatibilidad que determina qué características va a haber disponibles y qué versión de Analysis Services ejecuta el modelo.  Si puede especificar que un nivel de compatibilidad determinado determina en parte por el Diseñador de modelos.  
  
 Modelos tabulares mediante la funcionalidad más reciente, como los archivos BIM en formato JSON tabular y bidireccional entre el filtrado, deben crear o actualizar en el nivel de compatibilidad 1200 o superior.  
  
 Si necesita un nivel de compatibilidad inferior, quizás porque desea implementar un modelo en una versión anterior de Analysis Services, puede seguir usará el Diseñador de modelos en SSDT. Las versiones más recientes de la herramienta admiten la creación de cualquier tipo de modelo (tabular o multidimensional), en cualquier nivel de compatibilidad.   

## <a name="administrative-tools"></a>Herramientas administrativas  
  
 SQL Server Management Studio (SSMS) es la herramienta de administración principal para todas las características de SQL Server, incluido Analysis Services. SSMS es una descarga web gratuita que se actualiza mensualmente. 
  
**[Descargar SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md)** 
  
 SSMS incluye eventos extendidos (xEvents), que proporciona una alternativa ligera a los seguimientos de SQL Server Profiler usa para supervisar la actividad y diagnosticar problemas en servidores de Azure Analysis Services y SQL Server 2016. Para obtener más información, consulte [Monitor Analysis Services with SQL Server Extended Events](../analysis-services/instances/monitor-analysis-services-with-sql-server-extended-events.md) .  
  
### <a name="sql-server-profiler"></a>SQL Server Profiler  
 Aunque esté oficialmente en desuso por la aparición de los xEvents, SQL Server Profiler ofrece un método conocido para controlar las conexiones, ejecutar consultas MDX y otras operaciones del servidor. SQL Server Profiler está instalado de forma predeterminada. Puede encontrarlo con aplicaciones de SQL Server en las aplicaciones en Windows.  
  
### <a name="powershell"></a>PowerShell  
 Puede utilizar comandos de PowerShell para realizar muchas tareas administrativas. Consulte [referencia de PowerShell](../analysis-services/powershell/analysis-services-powershell-reference.md) para obtener más información.  
  
### <a name="community-and-third-party-tools"></a>Herramientas de la comunidad y de terceros  
 Consulte la [página de codeplex Analysis Services](http://sqlsrvanalysissrvcs.codeplex.com/) para obtener ejemplos de código de la comunidad. Los[foros](http://social.msdn.microsoft.com/Forums/sqlserver/home?forum=sqlanalysisservices) pueden ser útiles para buscar recomendaciones de herramientas de terceros compatibles con Analysis Services.  
  
## <a name="see-also"></a>Vea también  
 [Nivel de compatibilidad de una base de datos Multidimensional](../analysis-services/multidimensional-models/compatibility-level-of-a-multidimensional-database-analysis-services.md)   
 [Nivel de compatibilidad para modelos tabulares](../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)  
  
  
