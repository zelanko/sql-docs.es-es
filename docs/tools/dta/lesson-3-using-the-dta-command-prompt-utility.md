---
title: 'Lección 3: Usar la utilidad del símbolo del sistema dta | Documentos de Microsoft'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: dta
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-query-tuning
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- Database Engine [SQL Server], tutorials
ms.assetid: 30f27f4d-8852-4b12-ba62-57f63e496f1d
caps.latest.revision: 26
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b333aee9876af4bd3432184cdf6e5061ab0ddec7
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MTE
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="lesson-3-using-the-dta-command-prompt-utility"></a>Lección 3: Usar la utilidad del símbolo del sistema dta
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
La utilidad del símbolo del sistema **dta** ofrece funcionalidad adicional a la del Asistente para la optimización de motor de base de datos.  
  
Puede utilizar las herramientas XML que desee para crear archivos de entrada para la utilidad mediante el esquema XML del Asistente para la optimización de motor de base de datos. Este esquema se instala al instalar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y se encuentra en: C:\Archivos de programa (x86)\Microsoft SQL Server\110\Tools\Binn\schemas\sqlserver\2004\07\dta\dtaschema.xsd.  
  
El esquema XML del Asistente para la optimización de motor de base de datos también se encuentra disponible en línea en el [sitio web de Microsoft](http://go.microsoft.com/fwlink/?linkid=43100&clcid=0x409).  
  
Este esquema ofrece una mayor flexibilidad a la hora de configurar opciones de optimización. Por ejemplo, le permite realizar análisis de escenarios condicionales. El análisis de escenarios condicionales conlleva especificar un conjunto de estructuras de diseño físico hipotético ya existente para la base de datos que desea optimizar y, a continuación, analizarla con el Asistente para la optimización de motor de base de datos para determinar si este diseño físico hipotético mejorará el rendimiento del procesamiento de consultas. Este tipo de análisis tiene la ventaja de evaluar la nueva configuración sin incurrir en la sobrecarga que supone implementarla realmente. Si el diseño físico hipotético no proporciona las mejoras de rendimiento que desea, es fácil modificarlo y volver a analizarlo hasta que logre la configuración que se ajuste a sus necesidades.  
  
Además, al usar el esquema XML del Asistente para la optimización de motor de base de datos y la utilidad del símbolo del sistema **dta** , puede incorporar la funcionalidad del asistente a los scripts y usarla con otras herramientas de diseño de bases de datos.  
  
Esta lección no cubre el uso de la funcionalidad de entrada XML del Asistente para la optimización de motor de base de datos.  
  
Esta lección ofrece una introducción a la sintaxis básica de la utilidad del símbolo del sistema **dta** , muestra cómo obtener acceso a la Ayuda y practicar la optimización de cargas de trabajo sencillas.  
  
Incluye el tema siguiente:  
  
-   Iniciar la utilidad del símbolo del sistema **dta** y optimizar una carga de trabajo  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
[Iniciar la utilidad del símbolo del sistema dta y optimizar una carga de trabajo](../../tools/dta/lesson-3-1-starting-the-dta-command-prompt-utility-and-tuning-a-workload.md)  
  
  
  
