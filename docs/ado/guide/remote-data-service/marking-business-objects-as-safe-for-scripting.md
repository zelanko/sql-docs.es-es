---
title: Marcar objetos de negocio como seguros para Scripting | Documentos de Microsoft
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- business objects in RDS [ADO]
ms.assetid: 0be98d1a-ab3d-4dce-a166-dacda10d154a
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 05a2131b594d20c4215a2c52422d930c0ac2edfb
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="marking-business-objects-as-safe-for-scripting"></a>Marcar objetos de negocio como seguros para Scripting
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar a [servicio de datos de WCF](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Para ayudar a garantizar un entorno seguro de Internet, debe marcar los objetos de negocios crea una instancia con el [RDS. DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md) del objeto [CreateObject](../../../ado/reference/rds-api/createobject-method-rds.md) método como "seguros para scripts". Debe asegurarse de que se marcan como tal en el área de licencia del registro del sistema antes de que se puedan utilizar en DCOM.  
  
> [!NOTE]
>  Objetos de negocio marcados como seguros para inicialización o "seguros para scripts" se pueden crear una instancia e inicializar por cualquiera a través de la red. Marcar un objeto comercial "seguros para scripts" no hace que sea seguro. Es sumamente importante para asegurarse de que los objetos comerciales están codificados con la máxima seguridad para asegurarse de que estos objetos no presentan un punto de acceso sin protección para datos confidenciales.  
  
 Para marcar el objeto comercial como seguros para scripting, cree un archivo de texto con una extensión .reg que contiene el texto siguiente. En este ejemplo, \< *MyActiveXGUID*> es el número hexadecimal de GUID de su objeto de negocios. Los siguientes dos números habilitan la característica de seguridad para scripting:  
  
```  
[HKEY_CLASSES_ROOT\CLSID\<MyActiveXGUID>\Implemented   
Categories\{7DD95801-9882-11CF-9FA9-00AA006C42C4}]  
[HKEY_CLASSES_ROOT\CLSID\<MyActiveXGUID>\Implemented   
Categories\{7DD95802-9882-11CF-9FA9-00AA006C42C4}]  
```  
  
 Guarde el archivo e insértelo en el registro mediante el Editor del registro o haciendo doble clic en el archivo .reg en el Explorador de Windows.  
  
 Objetos de negocio creados en Microsoft Visual Basic se pueden marcar automáticamente como "seguros para scripting" en el paquete y el Asistente para la implementación. Cuando el asistente le pide que especifique la configuración de seguridad, seleccione **seguras para inicialización** y **seguros para scripting**.  
  
 En el último paso, el Asistente para instalación de aplicaciones crea un .htm y un archivo .cab. A continuación, puede copiar estos dos archivos en el equipo de destino y haga doble clic en el archivo .htm para cargar la página y registrar correctamente el servidor.  
  
 Dado que el objeto de negocios se instalarán en el directorio Windows\System32\Occache de forma predeterminada, muévalo al directorio Windows\System32 y cambie la **HKEY_CLASSES_ROOT\CLSID\\ ** \< *MyActiveXGUID*>\\**InprocServer32** clave del registro para que coincida con la ruta de acceso correcta.



