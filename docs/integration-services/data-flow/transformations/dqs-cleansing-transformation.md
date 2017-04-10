---
title: "Transformaci&#243;n Limpieza de DQS | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "corrección de datos"
  - "corregir datos"
ms.assetid: d2ec1b1a-c745-4741-b57c-6fdb524a154c
caps.latest.revision: 35
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 35
---
# Transformaci&#243;n Limpieza de DQS
  La transformación Limpieza de DQS usa Data Quality Services (DQS) para corregir datos de un origen de datos conectado aplicando reglas aprobadas que se crearon para el origen de datos conectado o un origen de datos similar. Para obtener más información acerca de las reglas de corrección de datos, vea [DQS Knowledge Bases and Domains](../../../data-quality-services/dqs-knowledge-bases-and-domains.md). Para obtener más información acerca de DQS, vea [Data Quality Services Concepts](../../../data-quality-services/data-quality-services-concepts.md).  
  
 Para determinar si es necesario corregir los datos, la transformación Limpieza de DQS procesa los datos de una columna de entrada cuando se cumplen las condiciones siguientes:  
  
-   La columna está seleccionada para la corrección de datos.  
  
-   El tipo de datos de la columna se admite para la corrección de datos.  
  
-   La columna está asignada a un dominio que tiene un tipo de datos compatible.  
  
 La transformación también incluye una salida de error que puede configurar para controlar los errores de fila. Para configurar la salida de error, use el **Editor de transformación Limpieza de DQS**.  
  
 Puede incluir la [Fuzzy Grouping Transformation](../../../integration-services/data-flow/transformations/fuzzy-grouping-transformation.md) en el flujo de datos para identificar filas de datos que probablemente estén duplicadas.  
  
## Proyectos y valores de calidad de los datos  
 Al procesar datos con la transformación Limpieza de DQS, un proyecto de limpieza se crea en el servidor Data Quality Server. Utilice Data Quality Client para administrar el proyecto. Además, puede utilizar Data Quality Client para importar los valores del proyecto en un dominio de base de conocimiento de DQS. Puede importar los valores solo a un dominio (o dominio vinculado) que la transformación Limpieza de DQS se configurara para usar.  
  
## Tareas relacionadas  
  
-   [Abrir proyectos de Integration Services en Data Quality Client](../../../data-quality-services/open-integration-services-projects-in-data-quality-client.md)  
  
-   [Importar valores de un proyecto de limpieza en un dominio](../../../data-quality-services/import-cleansing-project-values-into-a-domain.md)  
  
-   [Aplicar reglas de calidad de los datos al origen de datos](../../../integration-services/data-flow/transformations/apply-data-quality-rules-to-data-source.md)  
  
## Contenido relacionado  
  
-   [Abrir, desbloquear, cambiar nombre y eliminar un proyecto de calidad de los datos](https://msdn.microsoft.com/library/hh510417.aspx)  
  
-   Artículo sobre la [limpieza de datos complejos con dominios compuestos](http://social.technet.microsoft.com/wiki/contents/articles/13324.using-dqs-cleansing-complex-data-using-composite-domains.aspx), en social.technet.microsoft.com.  
  
  