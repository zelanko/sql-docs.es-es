---
title: Análisis rápido | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- fast parse [Integration Services]
ms.assetid: 6688707d-3c5b-404e-aa2f-e13092ac8d95
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 41e7848dff95d531db44bef2b45b11d7c3c5f85a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48054295"
---
# <a name="fast-parse"></a>Fast Parse
  El análisis rápido ofrece un conjunto rápido y simple de rutinas para analizar datos. Estas rutinas no son dependientes de la configuración regional y solo admiten un subconjunto de formatos de fecha, hora y número entero.  
  
## <a name="requirements-and-limitations"></a>Requisitos y limitaciones  
 Al implementar el análisis rápido, un paquete arriesga su capacidad de interpretar los datos numéricos y de fecha y hora en formatos específicos de configuración regional, así como varios formatos ISO 8601 básicos y extendidos utilizados con frecuencia, pero el paquete mejora su rendimiento. Por ejemplo, el análisis rápido admite únicamente las representaciones de formato de fecha usadas con más frecuencia, como DDMMYYYY y DD-MM-YYYY, no realiza ningún análisis específico de una configuración regional, no reconoce caracteres especiales en los datos de moneda y no puede convertir una representación hexadecimal o científica de números enteros.  
  
 El análisis rápido solamente está disponible cuando se utiliza el origen de archivo plano o la transformación Conversión de datos. El aumento del rendimiento puede ser considerable, por lo que debería tener en cuenta la posibilidad de utilizar el análisis rápido en estos componentes de flujo de datos, si es posible.  
  
 Si el flujo de datos en el paquete exige un análisis sensible a la configuración regional, se recomienda el análisis estándar en lugar del rápido. Por ejemplo el análisis rápido no reconoce los datos relacionados con la configuración regional que incluyen símbolos decimales como la coma, formatos de fecha que no sean los formatos año-mes-fecha y símbolos de moneda.  
  
 Las representaciones truncadas que implican una o más partes de una fecha, como el siglo, año o mes, no son reconocidas por el análisis rápido. Por ejemplo, el análisis rápido no reconoce el formato "**-YYMM**", que especifica un año y mes en un siglo específico, ni "**--MM**", que especifica un mes en un año implícito. Sin embargo, se reconocen algunas representaciones con precisión reducida. Por ejemplo, el análisis rápido reconoce el formato 'hhmm;', que indica solamente horas y minutos, y '**YYYY**', que indica el año solamente.  
  
 El análisis rápido se especifica en el nivel de columna. En el origen de archivo plano y en la transformación Conversión de datos, puede especificarse el análisis rápido en las columnas de salida. Las entradas y salidas pueden incluir columnas sensibles y no sensibles a la configuración regional.  
  
 Para obtener más información sobre los formatos de datos que admiten el análisis rápido, vea [Numeric Data Formats](../../2014/integration-services/numeric-data-formats.md) y [Date and Time Formats](../../2014/integration-services/date-and-time-formats.md).  
  
## <a name="related-tasks"></a>Related Tasks  
 [Configurar el análisis rápido](../../2014/integration-services/set-fast-parse.md)  
  
  
