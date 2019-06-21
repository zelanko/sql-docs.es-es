---
title: Crear un informe vinculado | Microsoft Docs
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
ms.openlocfilehash: 77590da41aa09f66d7549a0d7ff615cdb3f63af3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66506641"
---
# <a name="create-a-linked-report"></a>Crear un informe vinculado
  Un informe vinculado es un elemento del servidor de informes que proporciona un punto de acceso a un informe existente. Conceptualmente, es similar a los accesos directos a programa que se usan para ejecutar un programa o abrir un archivo.  
  
 Un informe vinculado se deriva de otro informe existente y conserva la definición de informe original. El informe vinculado siempre hereda el diseño de informe y las propiedades del origen de datos del informe original. El resto de propiedades y parámetros pueden ser distintos de los del informe original, incluyendo la seguridad, los parámetros, la ubicación, las suscripciones y las programaciones.  
  
 Se puede crear un informe vinculado cuando se desean crear versiones adicionales de un informe existente. Por ejemplo, se podría usar un único informe de ventas regional para crear informes específicos de regiones para todos los territorios de ventas.  
  
 Si bien los informes vinculados se basan normalmente en informes con parámetros, no es necesario disponer de este tipo de informe. Puede crear informes vinculados siempre que desee implementar un informe existente con diferentes parámetros.  
  
## <a name="to-create-a-linked-report"></a>Crear un informe vinculado  
  
1. En el portal web, desplácese hasta el informe que desee, haga doble clic en él y seleccione **administrar** desde el menú desplegable.

2. En el **administrar <reportname>**  página, seleccione **crear informe vinculado**.  
  
3. Escriba un nombre para el nuevo informe vinculado. Opcionalmente, escriba una descripción.  
  
4. Para seleccionar una carpeta diferente para el informe, seleccione el botón de puntos suspensivos (...) a la derecha del ***ubicación***.  Vaya a la nueva carpeta para el informe y seleccione **seleccione**. Si no selecciona una carpeta diferente, el informe vinculado se crea en la carpeta actual.  
  
5. Seleccione **Crear**. Se crea el informe vinculado.  

6. En **avanzadas**, seleccionar otro **tiempo de espera de informe** valor si lo desea y seleccione **aplicar** para guardar los cambios.
  
     El icono de un informe vinculado es distinto de otros elementos administrados por un servidor de informes. El siguiente icono distingue los informes vinculados:  
  
     ![Icono de informe vinculado](../../reporting-services/report-server/media/hlp-16linked.gif "Icono de informe vinculado")  
  
## <a name="see-also"></a>Vea también  
 [Abrir y cerrar un informe &#40;portal web&#41;](../../reporting-services/reports/open-and-close-a-report-report-manager.md)  
 [Conceptos de Reporting Services &#40;SSRS&#41;](../../reporting-services/reporting-services-concepts-ssrs.md)  
 [El portal web de un servidor de informes (modo nativo de SSRS)](../../reporting-services/web-portal-ssrs-native-mode.md)
  
