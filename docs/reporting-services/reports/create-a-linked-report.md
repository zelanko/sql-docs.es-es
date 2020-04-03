---
title: Crear un informe vinculado | Microsoft Docs
description: Obtenga información sobre cómo crear un informe vinculado para crear versiones adicionales de un informe existente.
ms.date: 05/30/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reports
ms.topic: conceptual
helpviewer_keywords:
- linked reports [Reporting Services], creating
ms.assetid: 12be8341-cb57-45e8-a421-2bf66b50234d
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: cb362f699e8bf87e0f386c3ec726869f67aec934
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "79510166"
---
# <a name="create-a-linked-report"></a>Crear un informe vinculado
  Un informe vinculado es un elemento del servidor de informes que proporciona un punto de acceso a un informe existente. Conceptualmente, es similar a los accesos directos a programa que se usan para ejecutar un programa o abrir un archivo.  
  
 Un informe vinculado se deriva de otro informe existente y conserva la definición de informe original. El informe vinculado siempre hereda el diseño de informe y las propiedades del origen de datos del informe original. El resto de propiedades y parámetros pueden ser distintos de los del informe original, incluyendo la seguridad, los parámetros, la ubicación, las suscripciones y las programaciones.  
  
 Se puede crear un informe vinculado cuando se desean crear versiones adicionales de un informe existente. Por ejemplo, se podría usar un único informe de ventas regional para crear informes específicos de regiones para todos los territorios de ventas.  
  
 Si bien los informes vinculados se basan normalmente en informes con parámetros, no es necesario disponer de este tipo de informe. Puede crear informes vinculados siempre que desee implementar un informe existente con diferentes parámetros.  
  
## <a name="to-create-a-linked-report"></a>Crear un informe vinculado  
  
1. En el portal web, vaya al informe que desee, haga clic con el botón derecho en él y seleccione **Administrar** en el menú desplegable.

2. En la página **Administrar<reportname>** , seleccione **Crear informe vinculado**.  
  
3. Escriba un nombre para el nuevo informe vinculado. Si lo desea, escriba una descripción.  
  
4. Para seleccionar una carpeta diferente para el informe, seleccione el botón de puntos suspensivos (...) a la derecha de ***Ubicación***.  Vaya a la nueva carpeta del informe y elija **Seleccionar**. Si no selecciona una carpeta distinta, el informe vinculado se creará en la carpeta actual.  
  
5. Seleccione **Crear**. Se crea el informe vinculado.  

6. En **Avanzado**, seleccione un valor diferente para **Tiempo de espera de informe** si lo desea, y seleccione **Aplicar** para guardar los cambios.
  
     El icono de un informe vinculado es distinto de otros elementos administrados por un servidor de informes. El siguiente icono distingue los informes vinculados:  
  
     ![Icono de informe vinculado](../../reporting-services/report-server/media/hlp-16linked.gif "Icono de informe vinculado")  
  
## <a name="see-also"></a>Consulte también  

 [Conceptos de Reporting Services &#40;SSRS&#41;](../../reporting-services/reporting-services-concepts-ssrs.md)  
 [El portal web de un servidor de informes (modo nativo de SSRS)](../../reporting-services/web-portal-ssrs-native-mode.md)
  
