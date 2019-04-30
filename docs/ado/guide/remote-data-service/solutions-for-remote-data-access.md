---
title: Soluciones para el acceso a datos remotos | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS [ADO]
ms.assetid: d311cc67-7db7-4c43-9590-d465564695e4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a761267c3d25619b58f23e2e7b6396f0e9b43958
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63204598"
---
# <a name="solutions-for-remote-data-access"></a>Soluciones de acceso a datos remotos
## <a name="the-issue"></a>El problema  
 ADO permite que la aplicación obtener acceso a directamente y modificar orígenes de datos (también conocidos como un sistema de dos niveles). Por ejemplo, si la conexión es el origen de datos que contiene los datos, es una conexión directa en un sistema de dos niveles.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo de Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Deben migrar las aplicaciones que usan RDS a [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Sin embargo, desea tener acceso a orígenes de datos indirectamente a través de un intermediario, como Microsoft® Internet Information Services (IIS). Esta disposición se denomina a veces un sistema de tres niveles. IIS es un sistema cliente/servidor que proporciona una manera eficaz para una aplicación local o de cliente invocar un programa de servidor, o remoto a través de Internet o una intranet. El programa de servidor obtiene acceso al origen de datos y, opcionalmente, procesa los datos obtenidos.  
  
 Por ejemplo, la página Web de intranet contiene una aplicación creada en Microsoft® Visual Basic Scripting Edition (VBScript), que se conecta a IIS. IIS a su vez se conecta al origen de datos real, recupera los datos, lo procesa de alguna manera y, a continuación, devuelve la información procesada para la aplicación.  
  
 En este ejemplo, la aplicación nunca conectado directamente al origen de datos; IIS se ha hecho. Y IIS tiene acceso a los datos por medio de ADO.  
  
> [!NOTE]
>  La aplicación cliente/servidor no tiene que estar basado en Internet o una intranet (es decir, basada en Web): puede constar únicamente de programas compilados en una red de área local. Sin embargo, el caso típico es una aplicación basada en Web.  
  
 Dado que algunos controles visuales, como una cuadrícula, la casilla de verificación o la lista, pueden usar la información devuelta, debe usarse fácilmente la información devuelta por un control visual.  
  
 Desea una interfaz de programación de aplicaciones sencilla y eficaz que es compatible con sistemas de tres niveles y devuelve la información como fácilmente como si se recuperó en un sistema de dos niveles. Servicio de datos remoto (RDS) es esta interfaz.  
  
## <a name="the-solution"></a>Solución  
 RDS define un modelo de programación: la secuencia de actividades necesarias para tener acceso a y actualizar un origen de datos: para tener acceso a datos a través de un intermediario, como Internet Information Services (IIS). El modelo de programación Resume toda la funcionalidad de RDS.  
  
## <a name="see-also"></a>Vea también  
 [Modelo de programación de RDS básica](../../../ado/guide/remote-data-service/basic-rds-programming-model.md)   
 [Escenario RDS](../../../ado/guide/remote-data-service/rds-scenario.md)   
 [Tutorial de RDS](../../../ado/guide/remote-data-service/rds-tutorial.md)   
 [Seguridad y uso de RDS](../../../ado/guide/remote-data-service/rds-usage-and-security.md)


