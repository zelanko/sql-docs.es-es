---
title: Soluciones de acceso a datos remotos | Documentos de Microsoft
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS [ADO]
ms.assetid: d311cc67-7db7-4c43-9590-d465564695e4
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 84030d05131d8a410690a6896b5173da356240c3
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2018
---
# <a name="solutions-for-remote-data-access"></a>Soluciones de acceso a datos remotos
## <a name="the-issue"></a>El problema  
 ADO permite que la aplicación obtener acceso a directamente y modificar orígenes de datos (también conocidos como un sistema de dos niveles). Por ejemplo, si la conexión es el origen de datos que contiene los datos, es una conexión directa en un sistema de dos niveles.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar a [servicio de datos de WCF](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Sin embargo, puede que desee tener acceso a orígenes de datos de forma indirecta a través de un intermediario, como Microsoft® Internet Information Services (IIS). Esta disposición se denomina a veces un sistema de tres niveles. IIS es un sistema de cliente/servidor que proporciona una manera eficaz de una aplicación local o cliente invocar un programa remoto o de servidor, a través de Internet o una intranet. El programa de servidor obtiene acceso al origen de datos y, opcionalmente, procesa los datos adquiridos.  
  
 Por ejemplo, la página Web de intranet contiene una aplicación escrita en Microsoft® Visual Basic Scripting Edition (VBScript), que se conecta a IIS. IIS a su vez se conecta al origen de datos real, recupera los datos, lo procesa de alguna manera y, a continuación, devuelve la información procesada a la aplicación.  
  
 En este ejemplo, la aplicación nunca directamente conectado al origen de datos; IIS ha. Y IIS tiene acceso a los datos por medio de ADO.  
  
> [!NOTE]
>  La aplicación de cliente/servidor no tiene que estar basado en Internet o una intranet (es decir, basada en Web), puede constar únicamente de programas compilados en una red de área local. Sin embargo, el caso típico es una aplicación basada en Web.  
  
 Dado que algunos controles visuales, como una cuadrícula, una casilla o una lista, pueden utilizar la información devuelta, debe utilizarse fácilmente la información devuelta por un control visual.  
  
 Desea una interfaz de programación de aplicaciones simple y eficaz que es compatible con sistemas de tres niveles y devuelve la información como fácilmente como si se hubiera ha recuperado en un sistema de dos niveles. Servicio de datos remoto (RDS) es esta interfaz.  
  
## <a name="the-solution"></a>Solución  
 RDS define un modelo de programación, la secuencia de actividades necesarias para obtener acceso y actualizar un origen de datos: para obtener acceso a datos a través de un intermediario, como Internet Information Services (IIS). El modelo de programación Resume toda la funcionalidad de RDS.  
  
## <a name="see-also"></a>Vea también  
 [Modelo de programación de RDS básica](../../../ado/guide/remote-data-service/basic-rds-programming-model.md)   
 [Escenario RDS](../../../ado/guide/remote-data-service/rds-scenario.md)   
 [Tutorial RDS](../../../ado/guide/remote-data-service/rds-tutorial.md)   
 [Seguridad y uso de RDS](../../../ado/guide/remote-data-service/rds-usage-and-security.md)


