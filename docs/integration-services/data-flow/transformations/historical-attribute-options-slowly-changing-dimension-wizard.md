---
title: Opciones de atributos históricos (Asistente para dimensiones de variación lenta) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.loaddimwizard.histattriboption.f1
ms.assetid: a176ec66-ec39-4c99-99d1-c1afa8450e1e
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 03d045cddeb2da31a3a9c3e4e3cef9f17d10d0f8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65726061"
---
# <a name="historical-attribute-options-slowly-changing-dimension-wizard"></a>Opciones de atributos históricos (Asistente para dimensiones variables)

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Utilice el cuadro de diálogo **Opciones de atributos históricos** para mostrar los atributos históricos por fechas de inicio y finalización, o bien para registrar atributos históricos en una columna creada especialmente con este fin.  
  
 Para obtener más información acerca de este asistente, vea [Slowly Changing Dimension Transformation](../../../integration-services/data-flow/transformations/slowly-changing-dimension-transformation.md).  
  
## <a name="options"></a>Opciones  
 **Utilice una única columna para mostrar los registros actual y expirado**  
 Si decide utilizar una sola columna para registrar el estado de los atributos históricos, dispone de las siguientes opciones:  
  
|Opción|Descripción|  
|------------|-----------------|  
|**Columna para indicar el registro actual**|Seleccione una columna donde se va a indicar el registro actual.|  
|**Valor actual**|Utilice **True** o **Current** para indicar si el registro es actual.|  
|**Valor de expiración**|Utilice **False** o **Expired** para indicar si el registro es un valor histórico.|  
  
 **Utilice las fechas inicial y final para identificar los registros actual y expirado**  
 La tabla de dimensiones de esta opción debe incluir una columna de fecha. Si decide mostrar los atributos históricos por fechas de inicio y finalización, dispone de las siguientes opciones:  
  
|Opción|Descripción|  
|------------|-----------------|  
|**Columna de fecha inicial**|Seleccione en la tabla de dimensiones la columna que contiene la fecha inicial.|  
|**Columna de fecha final**|Seleccione en la tabla de dimensiones la columna que contiene la fecha final.|  
|**Variable para establecer valores de fecha**|Seleccione una variable de fecha de la lista.|  
  
## <a name="see-also"></a>Consulte también  
 [Configurar salidas mediante el Asistente para dimensión de variación lenta](../../../integration-services/data-flow/transformations/configure-outputs-using-the-slowly-changing-dimension-wizard.md)  
  
  
