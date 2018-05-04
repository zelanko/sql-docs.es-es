---
title: Probar un modelo en el modo DirectQuery | Documentos de Microsoft
ms.custom: ''
ms.date: 07/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 11260792-ff8b-4d0e-b845-ca210dd3fced
caps.latest.revision: 11
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 7c57766209690f9509f4fd9c321358faa534cd96
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="test-a-model-in-directquery-mode"></a>Probar un modelo en el modo DirectQuery
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Revise las opciones para probar un modelo tabular en el modo DirectQuery en cada fase de desarrollo, empezando por el diseño.  
  
## <a name="test-in-excel"></a>Prueba en Excel 
  
 Al diseñar el modelo en SSDT, puede usar la característica **Analizar en Excel** para probar las decisiones de modelado frente a un conjunto de datos de ejemplo en memoria, o bien con la base de datos relacional.  Al hacer clic en Analizar en Excel, se abre un cuadro de diálogo donde puede especificar diferentes opciones.
 
 ![Opciones de DirectQuery de Analizar en Excel](../../analysis-services/tabular-models/media/analyze-in-excel-directquery-options.png)
 
 Si el modo DirectQuery del modelo está activado, puede especificar el modo de conexión DirectQuery, donde tendrá dos opciones:
 - **Vista de datos de ejemplo** : con esta opción, todas las consultas de Excel se dirigen a particiones de ejemplo que contienen un conjunto de datos de ejemplo en memoria. Esta opción es útil si quiere asegurarse de que las fórmulas DAX que tenga en medidas, columnas calculadas o seguridad de nivel de fila se ejecuten correctamente.
 
 - **Vista de datos completa** : con esta opción, todas las consultas de Excel se envían a Analysis Services y, después, a la base de datos relacional. Esta opción es, de hecho, un modo DirectQuery que funciona correctamente.
 
 ### <a name="other-clients"></a>Otros clientes
 Al usar Analizar en Excel, se crea un archivo de conexión .odc. Puede usar la información de la cadena de conexión de este archivo para conectarse al modelo desde otras aplicaciones cliente. Se agrega otro parámetro (DataView=Sample) para especificar que el cliente tiene que conectarse a particiones de datos de ejemplo.  
  
## <a name="monitor-query-execution-on-backend-systems-using-xevents-or-sql-profiler"></a>Supervisar la ejecución de consultas en sistemas back-end con xEvents o SQL Profiler 
 Inicie un seguimiento de sesión conectado a la base de datos relacional de SQL Server para supervisar las conexiones que proceden del modelo tabular:  
  
-   [Supervisar Analysis Services con SQL Server Extended Events](../../analysis-services/instances/monitor-analysis-services-with-sql-server-extended-events.md)  
  
-   [Usar a SQL Server Profiler para supervisar Analysis Services](../../analysis-services/instances/use-sql-server-profiler-to-monitor-analysis-services.md)  
  
 Si usa Oracle o Teradata, use las herramientas de supervisión de seguimiento disponibles para esos sistemas.  
  
  
