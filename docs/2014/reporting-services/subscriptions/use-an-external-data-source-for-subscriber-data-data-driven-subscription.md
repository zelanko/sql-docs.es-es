---
title: Usar un origen de datos externo para obtener información de los suscriptores (suscripción controlada por datos) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- subscriber data sources [Reporting Services]
- subscriptions [Reporting Services], external data sources
- query-based subscriptions [Reporting Services]
- external data sources [Reporting Services]
- data-driven subscriptions
- data sources [Reporting Services], subscriptions
ms.assetid: 1cade8ec-729c-4df8-a428-e75c9ad86369
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 8314a1d0bdf16a7a320c8a5a7e06558a2bec62c4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62631848"
---
# <a name="use-an-external-data-source-for-subscriber-data-data-driven-subscription"></a>Usar un origen de datos externo para obtener información de los suscriptores (suscripción controlada por datos)
  En una suscripción controlada por datos, los datos de suscripción dinámica se proporcionan mediante una consulta o un comando que recupera los datos desde un origen de datos externo. Los datos de suscripción se pueden recuperar desde cualquier origen de datos compatible que satisfaga los requisitos del procesamiento de suscripciones controladas por datos. La sintaxis de la consulta o el comando debe ser válida para una extensión de procesamiento de datos instalada en el servidor de informes.  
  
## <a name="data-processing-requirements"></a>Requisitos del procesamiento de datos  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] usa extensiones de procesamiento de datos para recuperar datos de suscripción. Entre los tipos de orígenes de datos recomendados, se incluyen los siguientes:  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bases de datos relacionales  
  
-   bases de datos Oracle  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] orígenes de datos multidimensionales y de minería de datos  
  
-   Orígenes de datos XML  
  
     Cuando se utilice la extensión de procesamiento de datos XML para datos de suscriptor, asegúrese de aumentar el valor del tiempo de espera de consulta en la suscripción. La extensión de procesamiento de datos XML utiliza milisegundos en lugar de segundos para los valores de tiempo de espera de consulta. Si no se aumenta el valor de tiempo de espera, es posible que se produzca un error en la suscripción debido a que el tiempo de procesamiento no es suficiente.  
  
     Evite utilizar la opción **No se necesitan credenciales** al configurar la conexión al origen de datos de suscriptor. Se recomienda el uso de credenciales almacenadas cuando se utilice la extensión de procesamiento de datos XML para recuperar datos de suscripción en tiempo de ejecución.  
  
 Quizás se puedan utilizar otros tipos de origen de datos admitidos, pero no se garantiza que todos ellos funcionen. Por ejemplo, los tipos de origen de datos siguientes no se pueden utilizar para datos de suscriptor:  
  
-   Bases de datos SAP Netweaver BI  
  
-   Modelos de informe  
  
 Si tiene una extensión de procesamiento de datos personalizada que quiere usar en las suscripciones controladas por datos, es necesario que implemente las interfaces <xref:Microsoft.ReportingServices.DataProcessing.IDbCommand> y <xref:Microsoft.ReportingServices.DataProcessing.IDataReader> . La extensión de procesamiento de datos debe admitir la ejecución de una consulta solo de esquema. Esta consulta se utiliza para recuperar metadatos de columna en tiempo de diseño, de manera que los usuarios puedan asignar columnas a opciones de entrega y parámetros de informe en la definición de la suscripción. La ejecución de la consulta solo de esquema se produce en una etapa inicial, cuando el usuario define la suscripción.  
  
## <a name="query-requirements"></a>Requisitos de consulta  
 Cuando se crea una consulta que recupera datos de suscripción, deben tenerse en cuenta los puntos siguientes:  
  
-   Solo se puede crear una consulta para la suscripción.  
  
-   La consulta debe devolver todos los valores que se desea utilizar para las opciones de entrega y para especificar parámetros de informe.  
  
-   El servidor de informes creará una entrega de informe para cada fila del conjunto de resultados. Si el conjunto de resultados está formado por trescientas filas, el servidor de informes intentará entregar trescientos informes.  
  
## <a name="setting-delivery-options-using-variable-data-from-a-subscriber-database"></a>Configurar las opciones de entrega con datos variables procedentes de una base de datos de suscriptor  
 Se pueden utilizar los datos de la base de datos de suscriptor para personalizar las opciones de entrega de cada destinatario. La clase de extensión de entrega que se utilice determina las opciones disponibles. Si utiliza la extensión de entrega por correo electrónico del servidor de informes, la consulta debería contener un alias de correo electrónico para cada suscriptor. Si se está usando la entrega a recursos compartidos de archivos, los datos de suscriptor deberán incluir valores que puedan utilizarse para crear archivos de informe específicos del suscriptor o para proporcionar un destino para la entrega. Para obtener más información, consulte [File Share Delivery in Reporting Services](file-share-delivery-in-reporting-services.md) y [entrega por correo electrónico en Reporting Services](e-mail-delivery-in-reporting-services.md).  
  
## <a name="passing-parameter-values-from-the-subscriber-database-to-the-report"></a>Pasar valores de parámetro desde la base de datos de suscriptores al informe  
 Si se va a crear una suscripción controlada por datos para un informe con parámetros, se pueden utilizar valores de parámetro variables para personalizar los resultados de cada informe. Por ejemplo, la base de datos de suscriptores puede contener información sobre los números de identificación de los empleados, las fechas de contratación, los puestos de trabajo y la ubicación en la oficina que puede utilizarse para filtrar datos del informe. Si el informe acepta parámetros basados en estos u otros datos de columnas disponibles, puede asignar el parámetro a la columna adecuada.  
  
 Cuando asigne campos de suscriptor a parámetros de informe, asegúrese de que los tipos de datos sean compatibles con la longitud de las columnas. Si hay discrepancias, se producirán errores al procesar las suscripciones. Para más información sobre cómo usar los datos de suscriptor en un informe con parámetros, vea [Crear una suscripción controlada por datos &#40;Tutorial de SSRS&#41;](../create-a-data-driven-subscription-ssrs-tutorial.md).  
  
## <a name="modifying-the-subscriber-data-source"></a>Modificar el origen de datos de suscriptores  
 Las siguientes modificaciones en el origen de datos de suscriptores pueden impedir que se ejecute la suscripción:  
  
-   Quitar columnas a las que se hace referencia en la suscripción.  
  
-   Modificar la estructura de tabla del origen de datos.  
  
-   Cambiar el tipo de datos y otras propiedades de columna.  
  
 Si realiza cualquiera de estos cambios, deberá actualizar la suscripción.  
  
## <a name="see-also"></a>Vea también  
 [Crear, modificar y eliminar una suscripción controlada por datos](data-driven-subscriptions.md)   
 [Data-Driven Subscriptions](data-driven-subscriptions.md)   
 [Suscripciones y entrega &#40;Reporting Services&#41;](subscriptions-and-delivery-reporting-services.md)  
  
  
