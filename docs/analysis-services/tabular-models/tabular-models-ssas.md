---
title: Los modelos tabulares | Microsoft Docs
ms.date: 09/17/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 1f894ad30f6344eb832cb9549a60c7f60071188c
ms.sourcegitcommit: e34e9cd1b1ec02393dc88b1f0471023a7f7f278b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/21/2018
ms.locfileid: "46506139"
---
# <a name="tabular-models"></a>Modelos tabulares
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]

  Los modelos tabulares en Analysis Services son las bases de datos que se ejecutan en memoria o en el modo DirectQuery, conectarse a los datos directamente desde los datos relacionales de back-end orígenes. Mediante el uso de algoritmos de compresión de última generación y el procesador de consultas multiproceso, el motor de análisis de Vertipaq de Analysis Services ofrece un acceso rápido a datos y objetos de modelo tabular mediante la notificación de las aplicaciones cliente como Power BI y Excel.  
  
 Aunque los modelos en memoria son el valor predeterminado, DirectQuery es un modo de consulta alternativo para los modelos que son demasiado grandes para caber en memoria, o cuando la volatilidad de los datos impide una estrategia de procesamiento razonable. DirectQuery logra la paridad con modelos en memoria mediante la compatibilidad con una amplia gama de orígenes de datos, capacidad para manejar tablas calculadas y columnas en un modelo DirectQuery, seguridad de nivel de fila a través de expresiones de DAX que llegue a la base de datos back-end y realizar consultas optimizaciones que producen un rendimiento más rápido.
  
 Los modelos tabulares se crean en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] mediante la plantilla de proyecto de modelo Tabular. La plantilla de proyecto proporciona una superficie de diseño para crear objetos como tablas, particiones, relaciones, jerarquías, medidas y KPI del modelo semántico. 
  
 Los modelos tabulares se pueden implementar en Azure Analysis Services o una instancia de SQL Server Analysis Services configurado para el modo de servidor Tabular. Los modelos tabulares implementados se pueden administrar en SQL Server Management Studio. 

Documentación de modelado tabular que se incluyen aquí se aplica en la mayoría de los casos, SQL Server Analysis Services y Azure Analysis Services. Se publican artículos específicos para Azure Analysis Services junto con otra documentación de Azure. Para obtener más información, consulte [documentación de Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/).
  
