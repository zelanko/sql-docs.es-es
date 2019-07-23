---
title: Referencia de errores y eventos (Integration Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services packages, events
- events [Integration Services]
- errors [Integration Services]
- Integration Services, errors
ms.assetid: cf4f0f14-8087-42d7-9b67-e4929228abd6
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 00c1fed0bf79774a9e3f52d00f69be5c6222deae
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68057681"
---
# <a name="errors-and-events-reference-integration-services"></a>Referencia de errores y eventos (Integration Services)

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Esta sección de la documentación contiene información sobre varios errores y eventos relacionados con [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. Se incluye información sobre las causas y la forma de resolver los mensajes de error.  
  
 Para más información sobre los mensajes de error de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , incluida una lista de la mayoría de los errores de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] y sus descripciones, vea [Referencia de errores y mensajes de Integration Services](../integration-services/integration-services-error-and-message-reference.md). Sin embargo, la lista no incluye actualmente información sobre solución de problemas.  
  
> [!IMPORTANT]  
>  Muchos de los mensajes de error que puede llegar a ver cuando trabaje con [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] provienen de otros componentes. Éstos pueden incluir proveedores de OLE DB, otros componentes de bases de datos como [!INCLUDE[ssDE](../includes/ssde-md.md)] y [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , u otros servicios o componentes como el sistema de archivos, el servidor SMTP o Microsoft Message Queueing. Para encontrar información acerca de estos mensajes de error externos, vea la documentación específica del componente.  
  
## <a name="error-messages"></a>mensajes de error  
  
|Nombre simbólico de error|Descripción|  
|----------------------------|-----------------|  
|DTS_E_CACHELOADEDFROMFILE|Indica que el paquete no se puede ejecutar porque se está intentando escribir una transformación de caché en caché en memoria. Sin embargo, un administrador de conexiones de caché ya ha cargado un archivo caché en la memoria caché en memoria.|  
|DTS_E_CANNOTACQUIRECONNECTIONFROMCONNECTIONMANAGER|Indica que el paquete no se puede ejecutar porque se produjo un error en una conexión especificada.|  
|DTS_E_CANNOTCONVERTBETWEENUNICODEANDNONUNICODESTRINGCOLUMN|Indica que un componente de flujo de datos está intentando pasar datos de cadena Unicode a otro componente que espera datos de cadena no Unicode en la correspondiente columna o viceversa.|  
|DTS_E_CANNOTCONVERTBETWEENUNICODEANDNONUNICODESTRINGCOLUMNS|Indica que un componente de flujo de datos está intentando pasar datos de cadena Unicode a otro componente que espera datos de cadena no Unicode en la correspondiente columna o viceversa.|  
|DTS_E_CANTINSERTCOLUMNTYPE|Indica que la columna no se puede agregar a la tabla de base de datos porque no se admite la conversión entre el tipo de datos de columna de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] y el tipo de datos de columna de base de datos.|  
|DTS_E_CONNECTIONNOTFOUND|Indica que el paquete no se puede ejecutar porque no se puede encontrar el administrador de conexiones especificado.|  
|DTS_E_CONNECTIONREQUIREDFORMETADATA|Indica que el Diseñador de [!INCLUDE[ssIS](../includes/ssis-md.md)] debe conectarse a un origen de datos para recuperar metadatos nuevos o actualizados para un origen o un destino, y que no se puede conectar al origen de datos.|  
|DTS_E_MULTIPLECACHEWRITES|Indica que el paquete no se puede ejecutar porque se está intentando escribir una transformación de caché en caché en memoria. Sin embargo, otra transformación de caché ya ha escrito en la memoria caché en memoria.|  
|DTS_E_PRODUCTLEVELTOLOW|Indica que el paquete no puede ejecutarse porque no está instalada la versión adecuada de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .|  
|DTS_E_READNOTFILLEDCACHE|Indica que una transformación de búsqueda está intentando leer datos de caché en memoria al mismo tiempo que una transformación de caché está escribiendo datos en la memoria caché.|  
|DTS_E_UNPROTECTXMLFAILED|Indica que el sistema no ha descifrado un nodo XML protegido.|  
|DTS_E_WRITEWHILECACHEINUSE|Indica que una transformación de caché está intentando escribir datos en caché en memoria al mismo tiempo que una transformación de búsqueda está leyendo datos en caché en memoria.|  
|DTS_W_EXTERNALMETADATACOLUMNSOUTOFSYNC|Indica que los metadatos de columna en el origen de datos no coinciden con los metadatos de columna en el componente de origen o de destino que está conectado al origen de datos.|  
  
## <a name="events-sqlispackage"></a>Eventos (SQLISPackage)  
 Para más información, vea [Eventos registrados por un paquete de Integration Services](../integration-services/performance/events-logged-by-an-integration-services-package.md).  
  
|Evento|Descripción|  
|-----------|-----------------|  
|SQLISPackage_12288|Indica que se inició un paquete.|  
|SQLISPackage_12289|Indica que un paquete ha terminado de ejecutarse correctamente.|  
|SQLISPACKAGE_12291|Indica que un paquete no pudo terminar de ejecutarse y se detuvo.|  
|SQLISPackage_12546|Indica que una tarea u otra aplicación ejecutable en un paquete ha finalizado su trabajo.|  
|SQLISPackage_12549|Indica que se generó un mensaje de advertencia en un paquete.|  
|SQLISPackage_12550|Indica que se generó un mensaje de error en un paquete.|  
|SQLISPackage_12551|Indica que una tarea en un paquete  no finalizó su trabajo y se detuvo.|  
|SQLISPackage_12557|Indica que un paquete ha terminado de ejecutarse.|  
  
## <a name="events-sqlisservice"></a>Eventos (SQLISService)  
 Para más información, vea [Eventos registrados por el servicio Integration Services](../integration-services/service/events-logged-by-the-integration-services-service.md).  
  
|Evento|Descripción|  
|-----------|-----------------|  
|SQLISService_256|Indica que el servicio está a punto de iniciarse.|  
|SQLISService_257|Indica que el servicio se ha iniciado.|  
|SQLISService_258|Indica que el servicio está a punto de detenerse.|  
|SQLISService_259|Indica que el servicio se ha detenido.|  
|SQLISService_260|Indica que el servicio intentó iniciarse, pero no pudo.|  
|SQLISService_272|Indica que el archivo de configuración no existe en la ubicación especificada.|  
|SQLISService_273|Indica que el archivo de configuración no se puede leer o no es válido.|  
|SQLISService_274|Indica que la entrada del Registro que contiene la ubicación del archivo de configuración no existe o esta vacía.|  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de errores y mensajes de Integration Services](../integration-services/integration-services-error-and-message-reference.md)  
  
  
