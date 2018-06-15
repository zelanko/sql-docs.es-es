---
title: Los modelos tabulares | Documentos de Microsoft
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8e85a618379b5b3c6da010c8b25782ed6836edb4
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
ms.locfileid: "34040351"
---
# <a name="tabular-models"></a>Modelos tabulares
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Los modelos tabulares son bases de datos de Analysis Services que se ejecutan en memoria o en el modo DirectQuery, de tal forma que se accede a los datos directamente desde los orígenes de datos relacionales de back-end. Mediante el uso de algoritmos de compresión de última generación y el procesador de consultas multiproceso, el motor de análisis ofrece un acceso rápido a datos y objetos del modelo tabular mediante la notificación de las aplicaciones cliente como Power BI y Excel.  
  
 Aunque los modelos en memoria son el valor predeterminado, DirectQuery es un modo de consulta alternativo para los modelos que son demasiado grandes para caber en memoria, o cuando la volatilidad de los datos impide una estrategia de procesamiento razonable. DirectQuery logra paridad con modelos en memoria mediante la compatibilidad con una amplia gama de orígenes de datos, capacidad para manejar tablas calculadas y columnas en un modelo de DirectQuery, seguridad de nivel de fila a través de expresiones de DAX que llegue a la base de datos back-end y las consultas optimizaciones que dan como resultado un rendimiento más rápido.
  
 Los modelos tabulares se crean en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] mediante la plantilla de proyecto de modelo Tabular que proporciona una superficie de diseño para crear un modelo, tablas, relaciones y expresiones DAX. Puede importar datos de varios orígenes y luego enriquecer el modelo agregando relaciones, columnas y tablas calculadas, medidas, KPI, jerarquías y traducciones.  
  
 Los modelos se pueden implementar en los servicios de análisis de Azure o una instancia de SQL Server Analysis Services configurado para el modo de servidor Tabular. Los modelos tabulares implementados se pueden administrar en SQL Server Management Studio. Medida que crecen los modelos, puede particiones para optimizar el procesamiento y protegerlos en el nivel de fila mediante la seguridad basada en roles.  

  
  
