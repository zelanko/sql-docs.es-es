---
title: 'Paso 3: Modificar el valor de configuración de la propiedad Directory | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: tutorial
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: ba2a091f-361c-4331-afe2-53b465164c36
caps.latest.revision: 29
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 0489101f98bcb4815e0c42e61763c894e61aeb00
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="lesson-5-3---modifying-the-directory-property-configuration-value"></a>Lección 5-3: Modificar el valor de configuración de la propiedad Directory
En esta tarea, modificará el parámetro de configuración, almacenado en el archivo SSISTutorial.dtsConfig, para la propiedad Value de la variable de nivel de paquete `User::varFolderName`. Esta variable actualiza la propiedad Directory del contenedor de bucles Foreach. El valor modificado hará referencia a la carpeta **New Sample Data** que ha creado en la tarea anterior. Una vez que haya modificado el parámetro de configuración y que haya ejecutado el paquete, la variable actualizará la propiedad Directory, mediante el valor rellenado desde el archivo de configuración, en lugar del valor del directorio configurado originalmente en el paquete.  
  
### <a name="to-modify-the-configuration-setting-of-the-directory-property"></a>Para modificar el parámetro de configuración de la propiedad Directory  
  
1.  En el Bloc de notas o en cualquier editor de texto, busque y abra el archivo de configuración SSISTutorial.dtsConfig que ha creado utilizando el Asistente para la configuración de paquetes en la tarea anterior.  
  
2.  Cambie el valor del elemento **ConfiguredValue** para que coincida con la ruta de acceso de la carpeta **New Sample Data** que ha creado en la tarea anterior. No especifique la ruta de acceso entre comillas. Si la carpeta **New Sample Data** está en el nivel de raíz de su unidad (por ejemplo, C:\\), el XML actualizado debería ser similar al siguiente ejemplo:  
  
    `<?xml version="1.0"?><DTSConfiguration><DTSConfigurationHeading><DTSConfigurationFileInfo GeneratedBy="DOMAIN\UserName" GeneratedFromPackageName="Lesson 5" GeneratedFromPackageID="{F4475E73-59E3-478F-8EB2-B10AFA61D3FA}" GeneratedDate="6/10/2012 8:16:50 AM"/></DTSConfigurationHeading><Configuration ConfiguredType="Property" Path="\Package.Variables[User::varFolderName].Properties[Value]" ValueType="String"><ConfiguredValue></ConfiguredValue></Configuration></DTSConfiguration>`  
  
    La información de encabezado, **GeneratedBy**, **GeneratedFromPackageID**y **GeneratedDate** será diferente en su archivo, por supuesto. El elemento que debe observar es **Configuration** . La propiedad **Value** de la variable `User::varFolderName`ahora contiene C:\New Sample Data.  
  
3.  Guarde el cambio y cierre el editor de texto.  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
[Paso 4: Probar el paquete del tutorial de la lección 5](../integration-services/lesson-5-4-testing-the-lesson-5-tutorial-package.md)  
  
  
  
