---
title: Conjuntos de datos incrustados y compartidos (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: adc95cc0-d15a-413d-bc5a-302eab37a069
caps.latest.revision: 6
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 35e8f59dca243b48eeffb471166d47f98d8a024b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36199860"
---
# <a name="embedded-and-shared-datasets-report-builder-and-ssrs"></a>Conjuntos de datos incrustados y compartidos (Generador de informes y SSRS)
  En un informe, un conjunto de datos representa los datos del informe que se devuelven como resultado de ejecutar una consulta en un origen de datos externo. El conjunto de datos depende de la conexión de datos que contiene información sobre el origen de datos externo. Los datos en sí no se incluyen en la definición de informe. El conjunto de datos contiene un comando de consulta, una colección de campos, parámetros, filtros y opciones de datos que incluyen la distinción entre mayúsculas y minúsculas y la intercalación. Hay dos tipos de conjuntos de datos:  
  
-   **Conjuntos de datos compartidos.** Un conjunto de datos compartido se publica en un servidor de informes y se puede usar en varios informes. Un conjunto de datos compartido debe basarse en un origen de datos compartido. Un conjunto de datos compartido puede estar almacenado en memoria caché y programarse creando un plan de actualización de la memoria caché.  
  
-   **Conjuntos de datos insertados.** Los conjuntos de datos incrustados se definen en un único informe y se usan en él.  
  
 La diferencia entre ambos enfoques es la manera en que se crean, almacenan y administran.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="shared-datasets"></a>Conjuntos de datos compartidos  
 Use un conjunto de datos compartido para proporcionar una consulta que pueda ser usada por más de un informe. Los conjuntos de datos compartidos se almacenan en el servidor de informes y se pueden administrar de forma independiente de los informes u orígenes de datos compartidos. Por ejemplo, un administrador del servidor de informes podría actualizar la consulta para aprovechar la indización mejorada u otra optimización del rendimiento de las consultas.  
  
 Se recomienda usar conjuntos de datos compartidos siempre que sea posible. Puede optimizar una consulta o almacenar en caché los resultados de la consulta para mejorar el rendimiento del informe. Los conjuntos de datos compartidos facilitan el acceso a los datos, y ayudan a mantener una mayor seguridad y rendimiento en el acceso a los informes y los conjuntos de datos.  
  
 En el Diseñador de informes, puede crear conjuntos de datos compartidos como parte de un proyecto de informe y controlar si se han de implementar en un servidor de informes. No puede desplazarse a un servidor de informes y seleccionar un conjunto de datos compartido para agregarlo a su informe.  
  
 En el Generador de informes se puede realizar lo siguiente:  
  
1.  Para crear un conjunto de datos compartido, utilice la vista de diseño de conjunto de datos compartido. Puede guardarlo en un servidor de informes o un sitio de SharePoint para compartirlo con otros informes. También puede desplazarse al servidor de informes y editar un conjunto de datos existente. En esta vista, puede generar una consulta y establecer todas las opciones de conjunto de datos. Para más información, vea [Vista de diseño de conjunto de datos compartidos &#40;Generador de informes&#41;](../report-builder/shared-dataset-design-view-report-builder.md).  
  
2.  Para agregar un conjunto de datos compartido a un informe, abra el Generador de informes en la vista de diseño de informe. Desde un asistente o en el panel Datos de informe, vaya al servidor de informes y seleccione el conjunto de datos compartido que desea agregar al informe. En esta vista, no puede cambiar la consulta excepto para agregar los campos. Puede invalidar otras opciones de datos y agregar filtros. No puede quitar los filtros.  
  
3.  En la tabla siguiente se comparan las propiedades que se pueden configurar para la definición del conjunto de datos compartido en el servidor de informes y la instancia del conjunto de datos compartido en la definición de informe.  
  
    |Property|Notas de configuración para la definición|Notas de configuración para la instancia|  
    |--------------|--------------------------------------------|------------------------------------------|  
    |Texto de consulta|Configure la consulta y defínala como expresión.|No puede cambiar la consulta.|  
    |Parámetros de consulta|No puede hacer referencia a los parámetros de informe<br /><br /> Incluye los valores predeterminados<br /><br /> Incluye una marca de solo lectura|Configure los parámetros que no están marcados como de solo lectura en la definición|  
    |Filtros|Definir filtros|No se pueden ver ni cambiar los filtros de conjunto de datos que forman parte de la definición<br /><br /> Puede crear filtros adicionales|  
    |Origen de datos|Debe ser un origen de datos compartido|No se puede cambiar el origen de datos|  
    |Campos|Campos en el comando de consulta<br /><br /> Los campos calculados no forman parte de la definición del conjunto de datos|Se ven los campos, pero no se pueden cambiar<br /><br /> La colección de campos es estática y está basada en la consulta en el momento que agregó el conjunto de datos compartido al informe. Para actualizar, haga clic en **Actualizar campos** en el cuadro de diálogo **Propiedades del conjunto de datos** . La colección de campos actual es cualquier la consulta actual que la definición devuelve.<br /><br /> Agregar campos calculados|  
    |Dataset|Opciones de datos como la distinción entre mayúsculas y minúsculas|Invalidar las opciones de datos en la instancia|  
  
## <a name="embedded-datasets"></a>Conjuntos de datos insertados  
 Use un conjunto de datos incrustado cuando desee recibir los datos desde un origen de datos externo que solo se va a usar en un informe. Los conjuntos de datos incrustados son útiles si se desea crear una consulta que no tenga ninguna otra dependencia y que no sea necesario usar para varios informes.  
  
 Para crear o editar un conjunto de datos incrustado, use el panel Datos de informe. Después de crear un conjunto de datos, puede configurar las propiedades en el cuadro de diálogo **Propiedades del conjunto de datos** .  
  
## <a name="see-also"></a>Vea también  
 [Incrustados y compartidos conexiones de datos u orígenes de datos &#40;el generador de informes SSRS&#41;](../embedded-and-shared-data-connections-or-data-sources-report-builder-and-ssrs.md)   
 [Crear un conjunto de datos compartido o un conjunto de datos incrustado &#40;Generador de informes y SSRS&#41;](create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)   
 [Agregar datos a un informe &#40;el generador de informes SSRS&#41;](report-datasets-ssrs.md)   
 [Colección Campos del conjunto de datos &#40;Generador de informes y SSRS&#41;](dataset-fields-collection-report-builder-and-ssrs.md)   
 [Conexiones de datos, orígenes de datos y cadenas de conexión en el generador de informes](../data-connections-data-sources-and-connection-strings-in-report-builder.md)   
 [Conexiones de datos, orígenes de datos y cadenas de conexión en Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)  
  
  