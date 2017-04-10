---
title: "Establecer las propiedades del procesamiento de informes | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "informes a petición"
  - "procesamiento de informes [Reporting Services], propiedades de ejecución"
  - "instantáneas [Reporting Services], ejecutar informes a partir de"
  - "informes almacenados en caché [Reporting Services]"
  - "instantáneas de informe [Reporting Services], ejecutar informes a partir de"
  - "instantáneas de ejecución de informes [Reporting Services]"
ms.assetid: b5cbc453-5986-423e-af44-1f243ef3edb1
caps.latest.revision: 43
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 43
---
# Establecer las propiedades del procesamiento de informes
  Las propiedades de ejecución del informe controlan el modo en que se procesa un informe. Estas propiedades deben establecerse de forma individual para cada uno de los informes.  
  
 Para establecer las propiedades de ejecución, abra el informe en el Administrador de informes y navegue a la página de propiedades Ejecución. Para obtener más información, vea [Página de propiedades Opciones de procesamiento &#40;Administrador de informes&#41;](../Topic/Processing%20Options%20Properties%20Page%20\(Report%20Manager\).md). También puede establecer propiedades mediante [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]; vea [Página de propiedades Opciones de procesamiento &#40;Administrador de informes&#41;](../Topic/Processing%20Options%20Properties%20Page%20\(Report%20Manager\).md).  
  
## Modos de ejecución del informe  
 Los informes pueden ejecutarse a petición o como una instantánea. La siguiente sección describe cada una de estas opciones.  
  
### Ejecutar informes a petición  
 Puede especificar que un informe consulte un origen de datos cada vez que un usuario ejecute el informe, lo cual da lugar a informes a petición que contienen los datos más actualizados. Por cada usuario que abre o solicita el informe se crea una instancia del informe; cada nueva instancia contiene los resultados de una nueva consulta. Cuando se usa esta opción, si diez usuarios abren el informe a la vez, se enviarán diez consultas para procesar al origen de datos.  
  
### Ejecutar informes a petición desde la caché  
 Para mejorar el rendimiento puede especificar que un informe (y sus datos) se almacene temporalmente en caché mientras un usuario lo esté ejecutando. La copia en caché estará disponible posteriormente para otros usuarios que tengan acceso al mismo informe. Con esta opción, si diez usuarios abren el informe, solamente la primera solicitud dará lugar al procesamiento del informe. El informe se almacena posteriormente en caché y los nueve usuarios restantes ven el informe almacenado en caché.  
  
 Los informes en caché se eliminan a intervalos definidos por el usuario. Estos intervalos pueden especificarse en minutos o se puede programar una fecha y hora específicas para vaciar la caché. Para obtener más información, vea [Informes almacenados en caché &#40;SSRS&#41;](../../reporting-services/report-server/caching-reports-ssrs.md).  
  
### Ejecutar informes desde instantáneas  
 Una instantánea de informe es un informe que contiene información de diseño y datos que se recuperan en un momento concreto. Los informes pueden ejecutarse como una instantánea de informe si se desea evitar que el informe se ejecute de forma arbitraria (durante una copia de seguridad programada, por ejemplo). Una instantánea de informe suele crearse y actualizarse posteriormente según una programación, lo que permite controlar con exactitud el momento en que se producirá el procesamiento del informe y los datos. Si un informe se basa en consultas que tardan demasiado en ejecutarse o en consultas que usan datos desde un origen de datos al que prefiere que nadie tenga acceso durante determinadas horas, debe ejecutar el informe como instantánea.  
  
 Las instantáneas de informe se almacenan en una base de datos del servidor de informes, de donde se recuperan posteriormente cada vez que un usuario o un proceso (como una suscripción) solicita el informe. Las instantáneas de informe se sobrescriben con una nueva instancia cada vez que se actualizan. El servidor de informes no guarda las versiones anteriores de una instantánea de informe salvo que se establezcan específicamente opciones para agregarla al historial del informe. Para obtener más información, vea [Crear, modificar y eliminar instantáneas del historial de informes](../../reporting-services/report-server/create-modify-and-delete-snapshots-in-report-history.md).  
  
 No todos los informes pueden configurarse para ejecutarse como una instantánea. No puede crear una instantánea para un informe que solicita credenciales a los usuarios o usa seguridad integrada de Windows para obtener datos para el informe. Si desea ejecutar un informe con parámetros como instantánea, debe especificar un parámetro predeterminado que se use al crear la instantánea. A diferencia de los informes que se ejecutan a petición, no es posible especificar un valor de parámetro diferente para una instantánea de informe cuando se abre el informe. La elección de un valor de parámetro diferente dará como resultado una nueva solicitud de procesamiento de informe, lo cual no está permitido.  
  
 En algunos casos, la configuración de un informe a petición para ejecutar una instantánea puede desactivar suscripciones. La siguiente condición hará que un servidor de informes desactive suscripciones existentes que se definieron cuando se configuró el informe para que se ejecute a petición:  
  
-   El informe usa parámetros de consulta y se selecciona un valor específico como parámetro predeterminado a fin de cumplir con los requisitos para ejecutar el informe como instantánea.  
  
-   Las suscripciones existentes se configuran para usar valores de parámetro distintos del valor de parámetro predeterminado que se especificó para la instantánea.  
  
 Cuando se cumpla esta condición, el servidor de informes deshabilitará la suscripción la próxima vez que esté programada su ejecución. Para volver a activarla, abra y guarde la suscripción. Al abrir la suscripción, el servidor de informes actualiza los valores de parámetro de la suscripción con los valores especificados para la instantánea. Para obtener más información sobre las suscripciones, vea [Suscripciones y entrega &#40;Reporting Services&#41;](../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md).  
  
## Vea también  
 [Establecer opciones de procesamiento &#40;Reporting Services en el modo integrado de SharePoint&#41;](../../reporting-services/report-server-sharepoint/set-processing-options-reporting-services-in-sharepoint-integrated-mode.md)   
 [Configurar las propiedades de ejecución de un informe &#40;Administrador de informes&#41;](../../reporting-services/reports/configure-execution-properties-for-a-report-report-manager.md)   
 [Conceptos de Reporting Services &#40;SSRS&#41;](../../reporting-services/reporting-services-concepts-ssrs.md)   
 [Cómo agregar una instantánea al historial de informes](../../reporting-services/report-server/add-a-snapshot-to-report-history-report-manager.md)   
 [Especificar información de credenciales y conexión para los orígenes de datos de informes](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md)  
  
  