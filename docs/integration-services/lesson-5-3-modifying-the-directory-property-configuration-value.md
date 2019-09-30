---
title: 'Paso 3: Modificar el valor de configuración de la propiedad Directory | Microsoft Docs'
ms.custom: ''
ms.date: 01/08/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: ba2a091f-361c-4331-afe2-53b465164c36
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 0f83ecbec76bfb142da55aa659ce3ef1cc95dad1
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/26/2019
ms.locfileid: "71295898"
---
# <a name="lesson-5-3-modify-the-directory-property-configuration-value"></a>Lección 5-3: Modificar el valor de configuración de la propiedad Directory

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



En esta tarea se modifica el parámetro de configuración almacenado en el archivo **SSISTutorial.dtsConfig** para establecer la propiedad **Value** de la variable de nivel de paquete `User::varFolderName`. La variable actualiza la propiedad **Directory** del contenedor de bucles Foreach. El valor modificado apunta a la carpeta **Nuevos datos de ejemplo** creada en la tarea anterior. Después de modificar el parámetro de configuración y ejecutar el paquete, la propiedad **Directory** se actualiza a partir de la variable del archivo de configuración. Anteriormente, el valor de la propiedad **Directory** formaba parte del paquete.  
  
## <a name="modify-the-configuration-setting-of-the-directory-property"></a>Modificar el parámetro de configuración de la propiedad Directory  
  
1.  En el Bloc de notas o cualquier otro editor de texto, busque y abra el archivo de configuración **SSISTutorial.dtsConfig** creado mediante el Asistente para configuración de paquetes en la tarea anterior.  
  
2.  Cambie el valor del elemento **ConfiguredValue** para que coincida con la ruta de acceso de la carpeta **New Sample Data** que ha creado en la tarea anterior. No especifique la ruta de acceso entre comillas. Si la carpeta **Nuevos datos de ejemplo** está en el nivel raíz de la unidad (por ejemplo, **C:\\** ), el XML actualizado debería ser similar al siguiente ejemplo:  
  
    ```
    <?xml version="1.0"?>
    <DTSConfiguration>
      <DTSConfigurationHeading>
        <DTSConfigurationFileInfo GeneratedBy="DOMAIN\UserName" GeneratedFromPackageName="Lesson 5" GeneratedFromPackageID="{F4475E73-59E3-478F-8EB2-B10AFEE1D3FA}" GeneratedDate="6/10/2018 8:16:50 AM"/>
      </DTSConfigurationHeading>
      <Configuration ConfiguredType="Property" 
          Path="\Package.Variables[User::varFolderName].Properties[Value]" ValueType="String">
        <ConfiguredValue>C:\New Sample Data</ConfiguredValue>
      </Configuration>
    </DTSConfiguration>  
    ```

    La información de encabezado **GeneratedBy**, **GeneratedFromPackageID** y **GeneratedDate** es diferente en el archivo. El elemento que debe observar es **Configuration** . La propiedad **Value** de la variable, `User::varFolderName`, ahora contiene **C:\Nuevos datos de ejemplo**.  
  
3.  Guarde el cambio y cierre el editor de texto.  
  
## <a name="go-to-next-task"></a>Ir a la tarea siguiente  
[Paso 4: Probar el paquete de la lección 5](../integration-services/lesson-5-4-testing-the-lesson-5-tutorial-package.md)  
  
  
  
