---
title: Propiedades del informe (cuadro de diálogo), referencias | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10530"
- sql12.rtp.rptdesigner.reportproperties.references.f1
ms.assetid: 4639d368-9918-4bb1-9953-7a724ca78dea
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: e57e0eb15c8c0ae7e326927ab14493f21c52cc14
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66104296"
---
# <a name="report-properties-dialog-box-references"></a>Propiedades del informe (cuadro de diálogo), Referencias
  Seleccione **Referencias** en el cuadro de diálogo **Propiedades del informe** para agregar o quitar referencias a ensamblados personalizados u otros ensamblados externos, así como instancias de clases personalizadas que las expresiones usarán en la definición de informe.  
  
## <a name="options"></a>Opciones  
 **Agregar o quitar ensamblados**  
 Muestra los ensamblados a los que el informe hace referencia. El ensamblado debe estar disponible en el equipo donde está instalada la herramienta que está usando para diseñar el informe y en el servidor de informes. El nombre de la referencia debe coincidir exactamente con el contenido de las etiquetas de ** \<CodeModule>** del archivo de lenguaje de definición de informes (. rdl).  
  
 **Add (Agregar)**  
 Haga clic en esta opción para agregar un ensamblado. Haga clic en el botón de puntos suspensivos (...) para abrir el cuadro de diálogo **abrir** y seleccionar los ensamblados necesarios para completar el procesamiento del informe y la evaluación de la expresión.  
  
 **Eliminar**  
 Para quitar una referencia de ensamblado de la lista, seleccione el nombre del ensamblado y haga clic en el botón **Quitar** .  
  
 **Agregar o quitar clases**  
 Muestra las instancias de clases que se utilizan en el informe. Solo los miembros basados en instancias, no los miembros estáticos, utilizan la lista de clases.  
  
 **Add (Agregar)**  
 Haga clic en esta opción para agregar una referencia de clase. Haga clic en el botón de puntos suspensivos (...) para abrir el cuadro de diálogo **abrir** y seleccionar las clases necesarias para completar el procesamiento del informe y la evaluación de la expresión.  
  
 **Eliminar**  
 Para eliminar la instancia de clase, selecciónela y haga clic en el botón **Quitar** .  
  
 **Up** (Arriba)  
 Para las clases que tienen dependencias, puede mover esta referencia hacia arriba en la lista.  
  
 **Vertical**  
 Para las clases que tienen dependencias, puede mover esta referencia hacia abajo en la lista.  
  
## <a name="see-also"></a>Consulte también  
 [Referencias a ensamblados y código personalizado en expresiones en Diseñador de informes &#40;SSRS&#41;](report-design/custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md)   
 [Referencias a las colecciones de variables de informe y de grupo &#40;Generador de informes y SSRS&#41;](report-design/built-in-collections-report-and-group-variables-references-report-builder.md)   
 [Ejemplos de expresiones &#40;Generador de informes y SSRS&#41;](report-design/expression-examples-report-builder-and-ssrs.md)  
  
  
