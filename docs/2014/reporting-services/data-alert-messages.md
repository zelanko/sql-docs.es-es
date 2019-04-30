---
title: Mensajes de alertas de datos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 6819720c-d848-4b90-9b51-89501b4f4645
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 809f893a38af6f269899e8e9d5913116b32864cc
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63164803"
---
# <a name="data-alert-messages"></a>Mensajes de alertas de datos
  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] alertas de datos envían a dos tipos de datos de mensajes de alerta por correo electrónico: Mensajes con resultados de alertas de datos y los mensajes con descripciones de errores. Los mensajes con resultados informan a todos los destinatarios de los cambios realizados en los datos del informe que sean de interés común e importantes para las decisiones empresariales. Si por alguna razón se produce un error y los resultados no están disponibles, se envía en su lugar el mensaje de error.  
  
 El propietario de la definición de la alerta de datos también puede ver la información sobre la instancia de la alerta de datos en el Administrador de alertas de datos. Para más información, consulte [Data Alert Manager for SharePoint Users](../../2014/reporting-services/data-alert-manager-for-sharepoint-users.md).  
  
##  <a name="DataAlertMessages"></a> Mensajes de alertas de datos  
 En las imágenes siguientes se muestra un mensaje de alerta de datos con resultados y un mensaje de alerta con una descripción de error.  
  
 **Mensaje de resultados**  
  
 ![Mensaje de correo electrónico de alerta de datos con los resultados](media/rs-alertmessageresults.gif "Mensaje de correo electrónico de alerta de datos con los resultados")  
  
 **Mensaje de error**  
  
 ![Mensaje de alerta de datos con mensaje de error](media/rs-alertmessageerrror.gif "Mensaje de alerta de datos con mensaje de error")  
  
 Los mensajes incluyen los mismos tipos de información.  
  
1.  **En nombre de** contiene el nombre de la persona que creó la definición de alerta de datos.  
  
2.  Si proporcionó una descripción en la definición de la alerta, esta se muestra bajo **en nombre de**.  
  
3.  En**Resultados de alertas** se muestran la filas de la fuente de distribución de datos del informe que satisfacen las reglas especificadas en la definición de la alerta en formato tabular o se muestra la descripción de un error. No hay límite en el número de filas que se pueden mostrar.  
  
4.  **Ir a informe** es un vínculo al informe en el que se basa la definición de alerta. Si el vínculo no es válido porque se ha movido o eliminado el informe, se muestra un mensaje de error.  
  
5.  En**Reglas** se muestran las reglas y las cláusulas de la definición de alerta. Esta información le ayuda a comprobar y entender los resultados de la alerta, así como a identificar reglas en la definición de alerta de datos que tal vez desee cambia para restringir o ampliar los resultados.  
  
6.  En**Parámetros de informe** se muestran los parámetros y los valores de parámetro que se usaron cuando se ejecutó el informe. Los parámetros y los valores de parámetro le ayudan a entender los resultados de las alertas.  
  
7.  En**Valores contextuales** se muestran los nombres y valores de los elementos del informe que están fuera de las regiones de datos del informe. Los elementos suelen ser cuadros de texto. Por ejemplo, un cuadro de texto con un valor constante como un asunto o una descripción de un informe.  
  
 La única diferencia entre los dos tipos de mensajes es el elemento 5, **Resultados de alertas**. Si ocurre un error cuando se crea una instancia de alerta de datos o un mensaje de alerta de datos, **Resultados de alertas** muestra un mensaje de error que describe el problema. El mensaje de error, enviado a todos los destinatarios, permite saber que los resultados de alertas esperados para la toma de decisiones empresariales no están disponibles.  
  
 
  
##  <a name="HowTo"></a> Tareas relacionadas  
 En esta sección se muestran los procedimientos para crear y editar las definiciones de alertas de datos que proporcionan la mayor parte de la información que se muestra en los mensajes de alertas de datos.  
  
-   [Creación de una alerta de datos en el Diseñador de alertas de datos](create-a-data-alert-in-data-alert-designer.md)  
  
-   [Modificación de una alerta de datos en el Diseñador de alertas](edit-a-data-alert-in-alert-designer.md)  
  

  
## <a name="see-also"></a>Vea también  
 [Diseñador de alertas de datos](../../2014/reporting-services/data-alert-designer.md)   
 [Alertas de datos de Reporting Services](../ssms/agent/alerts.md)  
  
  
