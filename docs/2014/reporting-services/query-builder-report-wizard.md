---
title: (Asistente para informes) del generador de consultas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.dataview.vdtquerydesigner.f1
- sql12.rtp.rptwizard.querybuilder.f1
helpviewer_keywords:
- Query Builder [Reporting Services]
ms.assetid: 1b0904ea-28c1-448e-b56c-c0fdfbc8b222
caps.latest.revision: 21
author: maggiesmsft
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 8fef45f5ec6c4b9e0682ea625b2cc84bc8aaa089
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37253467"
---
# <a name="query-builder-report-wizard"></a>Generador de consultas (Asistente para informes)
  Utilice el Generador de consultas para especificar una consulta que recupera un conjunto de resultados para utilizarlo en un informe. Puede elegir entre dos generadores de consultas:  
  
-   El generador de consultas basado en texto (predeterminado) proporciona un área de trabajo sencilla para especificar una consulta y ver los resultados. Puede especificar varias sintaxis de consulta, comandos o instrucciones [!INCLUDE[tsql](../includes/tsql-md.md)] para extensiones de procesamiento de datos personalizadas, y consultas que se especifican como expresiones. Dado que el generador de consultas genérico no procesa previamente la consulta y puede dar cabida a todo tipo de sintaxis de consulta, es la herramienta de generación de consultas predeterminada para el Diseñador de informes.  
  
-   El generador de consultas gráfico proporciona una experiencia visual más rica. Se utiliza en [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] y en otras partes de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Puede utilizar el generador de consultas gráfico si no está creando expresiones o instrucciones SQL formadas por varias partes.  
  
     Para cambiar al generador de consultas gráfico, alterne la activación del botón **Editar como texto** en la esquina superior izquierda de la ventana.  
  
 También puede importar una consulta de otro informe.  
  
## <a name="query-builder-options"></a>Opciones del generador de consultas  
 **Editar como texto**  
 Alterna entre el diseñador de consultas basado en texto y el diseñador gráfico de consultas, si ambos van a funcionar para la consulta.  
  
 **Importar**  
 Abre el cuadro de diálogo **Importar consulta** y muestra los archivos .rdl y .sql de cualquier informe disponible. Puede utilizar la consulta importada tal cual o modificarla en el generador de consultas.  
  
 **! (Ejecutar)**  
 Ejecuta la consulta y devuelve un conjunto de resultados si la consulta es válida. Tenga en cuenta que no puede ejecutar la consulta si se trata de una expresión. Para comprobar una consulta basada en una expresión, debe generar una vista previa del informe.  
  
 **Tipo de comando**  
 Especifica texto, procedimiento almacenado o tabla directa. La disponibilidad de un tipo de comando depende de la extensión de procesamiento de datos especificada.  
  
 **Panel de consulta**  
 Escriba la consulta.  
  
 **Panel de resultados**  
 Muestra el conjunto de resultados que devuelve la consulta.  
  
## <a name="see-also"></a>Vea también  
 [Conjuntos de datos incrustados y compartidos de informe &#40;Generador de informes y SSRS&#41;](report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [Ayuda del Asistente para informes](../../2014/reporting-services/report-wizard-help.md)  
  
  
