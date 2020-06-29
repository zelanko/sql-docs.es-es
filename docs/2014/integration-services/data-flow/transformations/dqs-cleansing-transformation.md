---
title: Transformación Limpieza de DQS | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- data correction
- correct data
ms.assetid: d2ec1b1a-c745-4741-b57c-6fdb524a154c
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 6df48dd9d90802b5694dcc6b7f73a65aee46b5e9
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/26/2020
ms.locfileid: "85430692"
---
# <a name="dqs-cleansing-transformation"></a>Transformación Limpieza de DQS
  La transformación Limpieza de DQS usa Data Quality Services (DQS) para corregir datos de un origen de datos conectado aplicando reglas aprobadas que se crearon para el origen de datos conectado o un origen de datos similar. Para obtener más información acerca de las reglas de corrección de datos, vea [DQS Knowledge Bases and Domains](../../../data-quality-services/dqs-knowledge-bases-and-domains.md). Para obtener más información acerca de DQS, vea [Data Quality Services Concepts](../../../data-quality-services/data-quality-services-concepts.md).  
  
 Para determinar si es necesario corregir los datos, la transformación Limpieza de DQS procesa los datos de una columna de entrada cuando se cumplen las condiciones siguientes:  
  
-   La columna está seleccionada para la corrección de datos.  
  
-   El tipo de datos de la columna se admite para la corrección de datos.  
  
-   La columna está asignada a un dominio que tiene un tipo de datos compatible.  
  
 La transformación también incluye una salida de error que puede configurar para controlar los errores de fila. Para configurar la salida de error, use el **Editor de transformación Limpieza de DQS**.  
  
 Puede incluir la [Fuzzy Grouping Transformation](fuzzy-grouping-transformation.md) en el flujo de datos para identificar filas de datos que probablemente estén duplicadas.  
  
## <a name="data-quality-projects-and-values"></a>Proyectos y valores de calidad de los datos  
 Al procesar datos con la transformación Limpieza de DQS, un proyecto de limpieza se crea en el servidor Data Quality Server. Utilice Data Quality Client para administrar el proyecto. Además, puede utilizar Data Quality Client para importar los valores del proyecto en un dominio de base de conocimiento de DQS. Puede importar los valores solo a un dominio (o dominio vinculado) que la transformación Limpieza de DQS se configurara para usar.  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [Abrir proyectos de Integration Services en Data Quality Client](../../../data-quality-services/open-integration-services-projects-in-data-quality-client.md)  
  
-   [Importar valores de un proyecto de limpieza en un dominio](../../../data-quality-services/import-cleansing-project-values-into-a-domain.md)  
  
-   [Aplicación de reglas de calidad de los datos al origen de datos](apply-data-quality-rules-to-data-source.md)  
  
## <a name="related-content"></a>Contenido relacionado  
  
-   [Administrar &#40;abrir, desbloquear, cambiar el nombre y eliminar&#41; un proyecto de calidad de datos](../../../data-quality-services/manage-open-unlock-rename-and-delete-a-data-quality-project.md)  
  
-   Artículo sobre la [limpieza de datos complejos con dominios compuestos](https://social.technet.microsoft.com/wiki/contents/articles/13324.using-dqs-cleansing-complex-data-using-composite-domains.aspx), en social.technet.microsoft.com.  
  
  
