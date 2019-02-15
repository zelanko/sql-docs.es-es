---
title: Configurar DQS para usar datos de referencia | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql13.dqs.administration.rdsconfiguration.f1
- sql13.dqs.administration.configuration.createDirectRDS.f1
- sql13.dqs.admin.config.rds.f1
ms.assetid: fae745e7-57a7-4cbc-8979-56ea8e392e4e
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: b0246f3aa83dace474b482d2998206b8418738a0
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/11/2019
ms.locfileid: "56030786"
---
# <a name="configure-dqs-to-use-reference-data"></a>Configurar DQS para utilizar datos de referencia

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  En este tema se describe cómo configurar [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) con el fin de utilizar datos de referencia para limpiar los datos. Puede utilizar datos de referencia tanto de Windows Azure Marketplace como de proveedores directos de datos de referencia de terceros en línea.  

> [!IMPORTANT]
> En este artículo se mencionan algunos servicios de datos de referencia de terceros que anteriormente no estaban disponibles desde Azure DataMarket. DataMarket y Data Services (incluidos los datos de dirección de Melissa, por ejemplo), se suspendieron después del 31/12/2016. Como resultado, ya no se pueden ejecutar los ejemplos de este artículo con los servicios especificados de DataMarket. Sin embargo, se pueden usar los servicios de datos de referencia que están disponibles directamente en línea de los proveedores de datos de referencia de terceros.

## <a name="before-you-begin"></a>Antes de empezar  
  
###  <a name="Prerequisites"></a> Requisitos previos  
 Para utilizar datos de referencia de Marketplace, es necesario tener una clave de cuenta de Marketplace válida. Para obtener información detallada sobre cómo crear una clave de cuenta de Marketplace, vea [Crear su cuenta](https://go.microsoft.com/fwlink/?LinkId=212936) (https://go.microsoft.com/fwlink/?LinkId=212936). También es posible crear una clave de cuenta de Marketplace desde [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] ; para ello, haga clic en **Configuración** en el área **Administración** de la página de inicio de [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] y, a continuación, haga clic en **Crear un id. de cuenta de DataMarket** en la pestaña **Datos de referencia** .  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permissions  
 Para configurar servicios de datos de referencia en DQS, debe disponer del rol dqs_administrator en la base de datos DQS_MAIN.  
  
##  <a name="Marketplace"></a> Configurar DQS para utilizar datos de referencia de Marketplace  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Ejecute la aplicación Data Quality Client](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  En la página de inicio de [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , en **Administración**, haga clic en **Configuración**.  
  
3.  En la pestaña **Datos de referencia** , en el área **Configuración de red** , escriba los valores apropiados en los cuadros **Servidor proxy** y **Puerto** si utiliza un servidor proxy para conectarse a Internet.  
  
4.  Especifique la clave de cuenta de Marketplace en el cuadro **Id. de cuenta de DataMarket** y haga clic en el icono **Validar el id. de cuenta de DataMarket** para validarla. Aparecerá un mensaje que indicará si la clave de cuenta de Marketplace especificada es válida.  
  
 Ahora ya está preparado para utilizar en DQS los servicios de datos de referencia de Marketplace a los que está suscrita la clave de cuenta de Marketplace especificada.  
  
##  <a name="ThirdParty"></a> Configurar DQS para utilizar datos de referencia de proveedores directos de datos de referencia de terceros en línea  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Ejecute la aplicación Data Quality Client](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  En la página de inicio de [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , en **Administración**, haga clic en **Configuración**.  
  
3.  En la pestaña **Datos de referencia** , en el área **Configuración de red** , escriba los valores apropiados en los cuadros **Servidor proxy** y **Puerto** si utiliza un servidor proxy para conectarse a Internet.  
  
4.  En el área **Configuración del servicio directo de datos de referencia de terceros en línea** , haga clic en el icono **Agregar un nuevo proveedor de servicios de datos de referencia** .  
  
5.  En el cuadro de diálogo **Crear un nuevo proveedor de servicios directos de datos de referencia de terceros en línea** , especifique los detalles siguientes:  
  
    1.  En el cuadro **Nombre** , escriba el nombre del nuevo proveedor de servicios directos de datos de referencia.  
  
    2.  (Opcional) en el cuadro **Descripción** , escriba una descripción para el nuevo proveedor de servicios directos de datos de referencia.  
  
    3.  En el cuadro **Categoría** , escriba la categoría de los datos proporcionados por el nuevo proveedor de servicios directos de datos de referencia.  
  
    4.  En el cuadro Esquema, especifique el esquema que define la cadena de los campos (nombres de columna) que se van a utilizar del proveedor de servicios directos de datos de referencia. Los nombres de campo no pueden incluir espacios, y los campos deben ir separados con comas. Por ejemplo: `FirstName, LastName, City, State`.  
  
    5.  En el cuadro **URI** , escriba el URI del proveedor de servicios directos de datos de referencia. Solo se permiten URI seguros (aquellos cuya dirección empieza por "https://") en DQS.  
  
    6.  En el cuadro **Tamaño máximo de lote** , escriba el número máximo de registros por lote que se enviarán al proveedor de servicios de datos de referencia para la limpieza. Se puede especificar un máximo de 100 registros por lote para la actividad de limpieza.  
  
    7.  En el cuadro **Id. de cuenta** , escriba el identificador de cuenta del suscriptor al proveedor de servicios de datos de referencia.  
  
6.  Haga clic en **Aceptar** para guardar los datos y cerrar el cuadro de diálogo **Crear un nuevo proveedor de servicios directos de datos de referencia de terceros en línea** . El proveedor directo de datos de referencia de terceros en línea recién agregado estará disponible en la cuadrícula **Proveedores de servicios directos de datos de referencia** en DQS.  
  
 Ahora ya puede utilizar los servicios de datos de referencia del proveedor de servicios directos de datos de referencia de terceros en línea que se acaba de configurar en DQS.  
  
##  <a name="FollowUp"></a> Seguimiento: después de configurar DQS para usar datos de referencia  
 A continuación, debe asignar los dominios de la base de conocimiento necesarios a los datos de referencia disponibles en los proveedores de datos que acaba de configurar. Para ello, vea [Adjuntar un dominio o un dominio compuesto a datos de referencia](../data-quality-services/attach-domain-or-composite-domain-to-reference-data.md).  
  
  
