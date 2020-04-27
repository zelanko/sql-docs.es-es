---
title: Propiedades del informe (cuadro de diálogo), referencias (Generador de informes) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10082"
ms.assetid: 3414c857-8ea6-4fc4-a6d5-b4883c039efa
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 99fe80a22f380bbe1406d357846c4103eeb0083e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66104392"
---
# <a name="report-properties-dialog-box-references-report-builder"></a>Propiedades del informe (cuadro de diálogo), Referencias (Generador de informes)
  Seleccione **Referencias** en el cuadro de diálogo **Propiedades del informe** para agregar o quitar referencias a ensamblados personalizados u otros ensamblados externos, así como instancias de clases personalizadas que las expresiones usarán en la definición de informe. Los ensamblados personalizados no se admiten en el modo local en el Generador de informes. Para crear informes que usen ensamblados personalizados, use Diseñador de informes [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]en.  
  
## <a name="options"></a>Opciones  
 **Agregar o quitar ensamblados**  
 Muestra los ensamblados a los que el informe hace referencia. El ensamblado debe estar disponible en el equipo donde está instalada la herramienta que está usando para diseñar el informe y en el servidor de informes. El nombre de la referencia debe coincidir exactamente con el contenido de las etiquetas de ** \<CodeModule>** del archivo de lenguaje de definición de informes (. rdl).  
  
 **Add (Agregar)**  
 Haga clic en esta opción para agregar un ensamblado. Haga clic en el botón de puntos suspensivos (...) para abrir el cuadro de diálogo **abrir** y seleccionar los ensamblados necesarios para completar el procesamiento del informe y la evaluación de la expresión.  
  
 **Remove**  
 Para quitar una referencia de ensamblado de la lista, seleccione el nombre del ensamblado y haga clic en el botón **Quitar** .  
  
 **Agregar o quitar clases**  
 Muestra las instancias de clases que se utilizan en el informe. Solo los miembros basados en instancias, no los miembros estáticos, utilizan la lista de clases.  
  
 **Add (Agregar)**  
 Haga clic en esta opción para agregar una referencia de clase. Haga clic en el botón de puntos suspensivos (...) para abrir el cuadro de diálogo **abrir** y seleccionar las clases necesarias para completar el procesamiento del informe y la evaluación de la expresión.  
  
 **Remove**  
 Para eliminar la instancia de clase, selecciónela y haga clic en el botón **Quitar** .  
  
 **Arriba**  
 Para las clases que tienen dependencias, puede mover esta referencia hacia arriba en la lista.  
  
 **Bajar**  
 Para las clases que tienen dependencias, puede mover esta referencia hacia abajo en la lista.  
  
## <a name="see-also"></a>Consulte también  
 [Generador de informes ayuda para cuadros de diálogo, paneles y asistentes](../../2014/reporting-services/report-builder-help-for-dialog-boxes-panes-and-wizards.md)   
 [Expresiones &#40;Generador de informes y SSRS&#41;](report-design/expressions-report-builder-and-ssrs.md)  
  
  
