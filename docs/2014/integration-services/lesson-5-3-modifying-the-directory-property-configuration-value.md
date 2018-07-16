---
title: 'Paso 3: Modificar el valor de configuración de la propiedad Directory | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: ba2a091f-361c-4331-afe2-53b465164c36
caps.latest.revision: 29
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 8675de132f15b723b6d7d2a651d31ef7b3e85063
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37304275"
---
# <a name="step-3-modifying-the-directory-property-configuration-value"></a>Paso 3: Modificar el valor de configuración de la propiedad Directory
  En esta tarea, modificará el parámetro de configuración, almacenado en el archivo SSISTutorial.dtsConfig, para la propiedad Value de la variable de nivel de paquete `User::varFolderName`. Esta variable actualiza la propiedad Directory del contenedor de bucles Foreach. El valor modificado hará referencia a la `New Sample Data` carpeta que ha creado en la tarea anterior. Una vez que haya modificado el parámetro de configuración y que haya ejecutado el paquete, la variable actualizará la propiedad Directory, mediante el valor rellenado desde el archivo de configuración, en lugar del valor del directorio configurado originalmente en el paquete.  
  
### <a name="to-modify-the-configuration-setting-of-the-directory-property"></a>Para modificar el parámetro de configuración de la propiedad Directory  
  
1.  En el Bloc de notas o en cualquier editor de texto, busque y abra el archivo de configuración SSISTutorial.dtsConfig que ha creado utilizando el Asistente para la configuración de paquetes en la tarea anterior.  
  
2.  Cambie el valor de la **ConfiguredValue** elemento para que coincida con la ruta de acceso de la `New Sample Data` carpeta que ha creado en la tarea anterior. No especifique la ruta de acceso entre comillas. Si el `New Sample Data` carpeta está en el nivel raíz de la unidad (por ejemplo, C:\\), el XML actualizado debería ser similar al ejemplo siguiente:  
  
     `<?xml version="1.0"?><DTSConfiguration><DTSConfigurationHeading><DTSConfigurationFileInfo GeneratedBy="DOMAIN\UserName" GeneratedFromPackageName="Lesson 5" GeneratedFromPackageID="{F4475E73-59E3-478F-8EB2-B10AFA61D3FA}" GeneratedDate="6/10/2012 8:16:50 AM"/></DTSConfigurationHeading><Configuration ConfiguredType="Property" Path="\Package.Variables[User::varFolderName].Properties[Value]" ValueType="String"><ConfiguredValue></ConfiguredValue></Configuration></DTSConfiguration>`  
  
     La información de encabezado, `GeneratedBy`, `GeneratedFromPackageID`, y **GeneratedDate** será diferente en el archivo, por supuesto. El elemento que debe observar es `Configuration`. La propiedad `Value` de la variable `User::varFolderName` ahora contiene C:\New Sample Data.  
  
3.  Guarde el cambio y cierre el editor de texto.  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Paso 4: Probar el paquete del tutorial de la lección 5](../integration-services/lesson-5-4-testing-the-lesson-5-tutorial-package.md)  
  
  
