---
title: Opciones de esquema de base de datos (Asistente para generación de esquema) de área de asunto (Analysis Services - datos multidimensionales) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.schemagenwizard.subjectareaschemaopts.f1
ms.assetid: 4c109bb8-e19d-412b-908f-bfdd7f872439
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e608f6ca210f1d86a58b469145a9840f7c25ba2b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62758494"
---
# <a name="subject-area-database-schema-options-schema-generation-wizard-analysis-services---multidimensional-data"></a>Opciones de esquema de la base de datos del área de asunto (Asistente para generar esquemas) (Analysis Services - Datos multidimensionales)
  Use la página **Opciones de esquema de la base de datos del área de asunto** para controlar cómo se genera el esquema y definir cómo se mantienen los datos.  
  
## <a name="options"></a>Opciones  
 **Esquema de propiedad**  
 Especifica el nombre del esquema dentro de la nueva base de datos de área de asunto.  
  
 **Crear claves principales en tablas de dimensiones**  
 Crea claves principales en las tablas de dimensiones en el esquema generado. Si no selecciona esta opción, no se genera ningún índice.  
  
> [!NOTE]  
>  Si no selecciona esta opción, se exige integridad referencial.  
  
 **Crear índices**  
 Crea índices en columnas de clave externa en el esquema generado.  
  
 **Exigir integridad referencial**  
 Exige integridad referencial en el esquema generado. Si no selecciona esta opción, las relaciones se crean, pero no se exigen.  
  
 **Conservar los datos al volver a generar**  
 Mantiene la base de datos del área de asunto cuando el asistente termina. Si no selecciona esta opción, todos los datos de la base de datos del área de asunto se pueden eliminar sin previo aviso.  
  
 **Rellenar tablas de tiempos**  
 Especifica cómo rellena el asistente las tablas de tiempos. En la siguiente tabla se describen los posibles valores para esta opción.  
  
> [!NOTE]  
>  Esta opción solo está habilitada si se realiza una llamada al Asistente para generar esquemas desde un proyecto de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , con [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] en modo de proyecto.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|Llenar|Las tablas de tiempos del área de asunto se llenan.|  
|No llenar|Las tablas de tiempos del área de asunto no se llenan.|  
|Llenar solamente si está vacía|Las tablas de tiempos del área de asunto se llenan solo si están vacías.|  
  
## <a name="see-also"></a>Vea también  
 [Ayuda F1 de Asistente para generación de esquema &#40;Analysis Services - datos multidimensionales&#41;](schema-generation-wizard-f1-help-analysis-services-multidimensional-data.md)  
  
  
