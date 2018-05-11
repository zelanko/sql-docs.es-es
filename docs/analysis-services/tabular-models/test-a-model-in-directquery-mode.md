---
title: Probar un modelo en el modo DirectQuery | Documentos de Microsoft
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: tabular-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 1b632cebe8df962c3d66ec0c40d4939a408cd70c
ms.sourcegitcommit: 1aedef909f91dc88dc741748f36eabce3a04b2b1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/08/2018
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
  
  
