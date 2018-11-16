---
title: Ejecutar objetos de negocio en servicios de componentes | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- component services in RDS [ADO]
ms.assetid: 3077d0b6-42d6-4f10-8e5d-42e6204f1109
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4ddf5fff0974c9a7ae92b5d44372f0d71fecf712
ms.sourcegitcommit: 1a5448747ccb2e13e8f3d9f04012ba5ae04bb0a3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/12/2018
ms.locfileid: "51558522"
---
# <a name="running-business-objects-in-component-services"></a>Ejecución de objetos de negocios en servicios de componentes
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo de Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Deben migrar las aplicaciones que usan RDS a [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Objetos de negocio pueden ser archivos ejecutables (.exe) o bibliotecas de vínculos dinámicos (.dll). La configuración que se utiliza para ejecutar el objeto de negocios depende de si el objeto es un archivo .dll o .exe:  
  
-   Objetos de negocio creados como archivos .exe se pueden llamar a través de DCOM. Si estos objetos de negocios se usan a través de Internet Information Services (IIS), están sujetos a referencias adicionales de datos, lo que ralentizan el rendimiento del cliente.  
  
-   Objetos de negocio creados como archivos .dll que se pueden usar a través de IIS y por lo tanto, también por HTTP. También se utiliza con DCOM únicamente a través de servicios de componentes o a través de Microsoft Transaction Server, si está utilizando Windows NT. Los archivos DLL del objeto de negocios debe estar registrado en el equipo del servidor IIS para tener acceso a ellos a través de IIS. Para obtener información sobre cómo configurar un archivo DLL para ejecutarlo en DCOM, vea la sección [habilitación de un archivo DLL y ejecutarlo en DCOM](../../../ado/guide/remote-data-service/enabling-a-dll-to-run-on-dcom.md).  
  
> [!NOTE]
>  Cuando los objetos de negocios en el nivel intermedio se implementan como componentes de servicios de componentes mediante **GetObjectContext**, **SetComplete**, y **SetAbort**, la empresa pueden utilizar objetos de servicios de componentes (o MTS, si está utilizando Windows NT) objetos de contexto para mantener su estado entre varias llamadas de cliente. Este escenario es posible con DCOM, que se suele implementar entre clientes de confianza y servidores en una intranet. En este caso, el [RDS. DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md) objeto y [CreateObject](../../../ado/reference/rds-api/createobject-method-rds.md) método en el lado del cliente se reemplazan por el objeto de contexto de transacción y **CreateInstance** método, que proporciona el **ITransactionContext** interfaz e implementada por los servicios de componentes.  
  
## <a name="see-also"></a>Vea también  
 [Aspectos básicos de RDS](../../../ado/guide/remote-data-service/rds-fundamentals.md)


