---
title: Marcar objetos de negocios como seguros para Scripting | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- business objects in RDS [ADO]
ms.assetid: 0be98d1a-ab3d-4dce-a166-dacda10d154a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0a8c6e3b1d74cb122a94cc643a9eb94d5dbb6c5c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47772724"
---
# <a name="marking-business-objects-as-safe-for-scripting"></a>Marcado de objetos de negocios como seguros para scripting
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo de Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Deben migrar las aplicaciones que usan RDS a [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Para ayudar a garantizar un entorno seguro de Internet, debe marcar los objetos de negocios crea una instancia con el [RDS. DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md) del objeto [CreateObject](../../../ado/reference/rds-api/createobject-method-rds.md) método como "seguros para scripting." Deberá asegurarse de que se marcan como tal en el área de licencia del registro del sistema antes de que pueden utilizarse en DCOM.  
  
> [!NOTE]
>  Marcados como "seguros para scripting" o seguro para la inicialización de objetos de negocios se pueden crear instancias de e inicializados por cualquier persona a través de la red. Marcar un objeto de negocios "seguros para scripting" no estén seguros. Es sumamente importante para asegurarse de que se codifican los objetos de negocios con la máxima seguridad para asegurarse de que estos objetos no presentan un punto de acceso sin protección para datos confidenciales.  
  
 Para marcar el objeto de negocios como seguros para scripting, cree un archivo de texto con la extensión .reg que contenga el texto siguiente. En este ejemplo, \< *MyActiveXGUID*> es el número GUID hexadecimal de un objeto comercial. Los siguientes dos números habilitan la característica de seguridad para el scripting:  
  
```  
[HKEY_CLASSES_ROOT\CLSID\<MyActiveXGUID>\Implemented   
Categories\{7DD95801-9882-11CF-9FA9-00AA006C42C4}]  
[HKEY_CLASSES_ROOT\CLSID\<MyActiveXGUID>\Implemented   
Categories\{7DD95802-9882-11CF-9FA9-00AA006C42C4}]  
```  
  
 Guarde el archivo y combinarlo con el registro mediante el Editor del registro o hacer doble clic en el archivo .reg en el Explorador de Windows.  
  
 Objetos de negocio creados en Microsoft Visual Basic se pueden marcar automáticamente como "seguros para scripting" en el paquete y el Asistente para la implementación. Cuando el asistente le pide que especifique la configuración de seguridad, seleccione **seguras para inicialización** y **seguros para scripting**.  
  
 En el último paso, el Asistente para instalación de aplicaciones crea un .htm y un archivo .cab. A continuación, puede copiar estos dos archivos en el equipo de destino y haga doble clic en el archivo .htm para cargar la página y registrar correctamente el servidor.  
  
 Dado que el objeto de negocios se instalará en el directorio Windows\System32\Occache de forma predeterminada, muévalo al directorio Windows\System32 y cambie la **HKEY_CLASSES_ROOT\CLSID\\**  \< *MyActiveXGUID*>\\**InprocServer32** clave del registro para que coincida con la ruta de acceso correcta.


