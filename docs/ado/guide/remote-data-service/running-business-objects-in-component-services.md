---
title: Ejecutar objetos de negocio en servicios de componentes | Documentos de Microsoft
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
- component services in RDS [ADO]
ms.assetid: 3077d0b6-42d6-4f10-8e5d-42e6204f1109
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8a6682b87a72b5002cf20f20792315e287955c9c
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2018
---
# <a name="running-business-objects-in-component-services"></a>Ejecutar objetos de negocio en servicios de componentes
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar a [servicio de datos de WCF](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Objetos de negocio pueden ser archivos ejecutables (.exe) o bibliotecas de vínculos dinámicos (.dll). La configuración que se utiliza para ejecutar el objeto de negocio depende de si el objeto es un archivo .dll o .exe:  
  
-   Objetos de negocio creados como archivos .exe se pueden llamar a través de DCOM. Si estos objetos de negocios se usan a través de Internet Information Services (IIS), están sujetos a calcular las referencias adicionales de datos, lo que ralentizan el rendimiento del cliente.  
  
-   Objetos de negocio creados como archivos .dll se pueden usar a través de IIS y, por tanto, también por HTTP. También se utiliza con DCOM sólo a través de servicios de componentes, o a través de Microsoft Transaction Server, si está utilizando Windows NT. Archivos DLL de objetos de negocios deberá estar registrado en el equipo del servidor IIS para tener acceso a ellos a través de IIS. Para obtener información sobre cómo configurar un archivo DLL para que se ejecute en DCOM, consulte la sección [habilitar una biblioteca DLL para que funcione en DCOM](../../../ado/guide/remote-data-service/enabling-a-dll-to-run-on-dcom.md).  
  
> [!NOTE]
>  Cuando se implementan los objetos de negocios en el nivel intermedio como componentes de servicios de componentes mediante **GetObjectContext**, **SetComplete**, y **SetAbort**, la empresa pueden utilizar objetos de servicios de componentes (o MTS, si está utilizando Windows NT) objetos en el contexto para mantener su estado entre diferentes llamadas de cliente. Este escenario es posible con DCOM, que normalmente está implementado entre clientes de confianza y servidores en una intranet. En este caso, el [RDS. DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md) objeto y [CreateObject](../../../ado/reference/rds-api/createobject-method-rds.md) método en el lado del cliente se reemplazan por el objeto de contexto de transacción y **CreateInstance** método, que se proporcionan con el **ITransactionContext** interfaz e implementada por servicios de componentes.  
  
## <a name="see-also"></a>Vea también  
 [Aspectos básicos de RDS](../../../ado/guide/remote-data-service/rds-fundamentals.md)


