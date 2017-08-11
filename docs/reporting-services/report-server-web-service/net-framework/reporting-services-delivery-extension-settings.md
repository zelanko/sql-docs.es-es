---
title: "Configuración de la extensión de entrega de Reporting Services | Documentos de Microsoft"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- XML Web service [Reporting Services], delivery extension settings
- Report Server Web service, delivery extension settings
- delivery [Reporting Services]
- network share delivery [Reporting Services]
- file share delivery [Reporting Services]
- e-mail [Reporting Services]
- mailing reports [Reporting Services]
- sharing reports
- extensions [Reporting Services], delivery
- mail [Reporting Services]
- Web service [Reporting Services], delivery extension settings
ms.assetid: 68c31a85-261c-4ec4-b8df-1f9842b46f8a
caps.latest.revision: 36
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: bc52f95cdc038c0074feb10b05fffe916b3d3da1
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="reporting-services-delivery-extension-settings"></a>Configuración de la extensión de entrega de Reporting Services
  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]incluye una extensión de entrega de correo electrónico y una extensión de entrega del recurso compartido de archivos. La entrega por correo electrónico proporciona una manera de enviar un informe a usuarios individuales o grupos a través del correo electrónico. La entrega a recursos compartidos de archivos permite enviar los informes representados automáticamente a un recurso compartido de la red. Puede utilizar cualquiera de las dos extensiones de entrega admitidas con las suscripciones estándar o las suscripciones controladas por datos. La configuración de entrega específica del tipo de extensión de entrega se pasa siempre que se llama a los métodos <xref:ReportService2010.ReportingService2010.CreateSubscription%2A>,<xref:ReportService2010.ReportingService2010.CreateDataDrivenSubscription%2A>,<xref:ReportService2010.ReportingService2010.SetSubscriptionProperties%2A> y <xref:ReportService2010.ReportingService2010.SetDataDrivenSubscriptionProperties%2A>. Para recuperar mediante programación una lista de configuración de entrega, utilice el método <xref:ReportService2010.ReportingService2010.GetExtensionSettings%2A>.  
  
> [!NOTE]  
>  La configuración de la extensión de entrega distingue mayúsculas y minúsculas.  
  
## <a name="e-mail-delivery-settings"></a>Configuración de entrega por correo electrónico  
 En la tabla siguiente se enumeran las opciones de configuración de la entrega por correo electrónico para las suscripciones que utilizan el correo electrónico del servidor de informes.  
  
|Configuración|Value|  
|-------------|-----------|  
|**PARA**|La dirección de correo electrónico que aparece en el **a** línea de mensaje de correo electrónico. Varias direcciones de correo electrónico se separan mediante puntos y coma. Requerido.|  
|**CC**|La dirección de correo electrónico que aparece en el **Cc** línea de mensaje de correo electrónico. Varias direcciones de correo electrónico se separan mediante puntos y coma. Opcional.|  
|**CCO**|La dirección de correo electrónico que aparece en el **CCO** línea de mensaje de correo electrónico. Varias direcciones de correo electrónico se separan mediante puntos y coma. Opcional.|  
|**ReplyTo**|La dirección de correo electrónico que aparece en el **responder a** encabezado del mensaje de correo electrónico. El valor debe ser una dirección de correo electrónico única. Opcional.|  
|**Incluir informe**|Valor que indica si incluir el informe en la entrega por correo electrónico. Un valor de **true** indica que se entrega el informe en el cuerpo del mensaje de correo electrónico.|  
|**RenderFormat**|Nombre de la extensión de representación que se usa para generar el informe representado. El nombre debe corresponder a una de las extensiones de representación visibles instaladas en el servidor de informes. Este valor es necesario si la **incluir informe** valor está establecido en un valor de **true**.|  
|**Prioridad**|Prioridad con la que se envía el mensaje de correo electrónico. Los valores válidos son **bajo**, **NORMAL**, y **alta**. El valor predeterminado es **NORMAL**.|  
|**Asunto**|El texto de la línea de asunto del mensaje de correo electrónico.|  
|**Comentario**|Texto incluido en el cuerpo del mensaje de correo electrónico.|  
|**IncludeLink**|Valor que indica si incluir un vínculo al informe en el cuerpo del correo electrónico.|  
  
## <a name="file-share-delivery-settings"></a>Configuración de la entrega a recursos compartidos de archivos  
 En la tabla siguiente se enumeran las opciones de configuración de la entrega a recursos compartidos de archivos para las suscripciones.  
  
|Configuración|Value|  
|-------------|-----------|  
|**NOMBRE DE ARCHIVO**|Nombre del archivo que se va a guardar en disco.|  
|**FILEEXTN**|Indica si incluir una extensión de archivo para el informe representado. El valor es **true** o **false**.|  
|**RUTA DE ACCESO**|Ruta de acceso a la carpeta o al recurso compartido de archivos UNC donde guardar el informe.|  
|**RENDER_FORMAT**|Formato del informe que se guarda en el disco.|  
|**NOMBRE DE USUARIO**|Nombre de usuario necesario para tener acceso al recurso de la red o disco.|  
|**CONTRASEÑA**|Contraseña necesaria para tener acceso al recurso de la red o disco.|  
|**WRITEMODE**|Modo de escritura que utilizar al tener acceso al disco. Los valores válidos son **ninguno**, **sobrescribir**, y **AutoIncrement**.|  
  
## <a name="see-also"></a>Vea también  
 [Referencia técnica de &#40; SSRS &#41;](../../../reporting-services/technical-reference-ssrs.md)   
 [Creación de aplicaciones con el servicio Web y .NET Framework](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)  
  
  
