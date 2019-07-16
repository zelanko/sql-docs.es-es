---
title: Mediante el SDK de Microsoft para Java | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Java (Microsoft SDK for)
- Microsoft SDK for Java [ADO]
ms.assetid: 2d7cb5b5-8307-49dd-b07e-c07069bb1626
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b0e6c5f2eb5ad792141e77122ff9e132d97f62ae
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67926465"
---
# <a name="using-the-microsoft-sdk-for-java"></a>Mediante el SDK de Microsoft para Java

> [!IMPORTANT]
> Microsoft no incluye soporte técnico de Visual J ++ en enero de 2004.

Microsoft SDK para Java es el kit de desarrollo para el entorno de Microsoft Internet Explorer. Herramientas, información y ejemplos se proporcionan para ayudarle a desarrollar programas Java y subprogramas según JDK 1.1 y la máquina virtual de Microsoft Win32 (VM de Microsoft). Microsoft SDK para Java no está asociado a Microsoft Visual J ++. Para descargar este SDK, haga clic aquí.  
  
 La utilidad Jactivex.exe genera clases a partir de una biblioteca de tipos, pero solo se puede invocar en la línea de comandos. Esta característica no está integrada con el entorno de desarrollo de Visual J ++. A diferencia de las clases generadas por el Asistente para la biblioteca de tipos de Java, puede entrar en los contenedores de clase creados por el SDK. Esto es útil para depurar cómo el código usa las clases contenedoras de ADO.  
  
 Este mecanismo lee la biblioteca de tipos de ADO y genera clases que se pueden crear instancias dentro de la aplicación. Genera las clases en la siguiente ubicación: \\< directorio de windows\>\Java\trustlib\msado15.  
  
 Creación de una aplicación ADO en Java mediante el SDK de Microsoft para Java es básicamente idéntico, desde la perspectiva del código fuente, al usar al Asistente para la biblioteca de tipos de Java. Código de ejemplo vea [contenedores de clase Java de ADO](../../../ado/guide/appendixes/ado-java-class-wrappers.md). La única diferencia está en cómo se generan las clases contenedoras en primer lugar, como se muestra en los pasos siguientes.  
  
### <a name="to-create-an-ado-project-with-the-microsoft-sdk-for-java"></a>Para crear un proyecto de ADO con Microsoft SDK para Java  
  
1.  Ejecute lo siguiente en un símbolo del sistema. Debe establecer la ruta de acceso para incluir el SDK de Microsoft para el directorio Bin de Java, o ejecute el comando desde esa ubicación. Normalmente, el Microsoft SDK para Java se instala en la misma ubicación que Visual Studio. Se trata de una instrucción de comando único.  
  
    ```java
    \<path to DevStudio>\<path to Java SDK>\bin\JactiveX.exe /javatlb "C:\program files\common files\system\ado\msado15.dll"  
    ```  
  
2.  Ejecute el siguiente comando para compilar las clases generadas. El modificador/g: t activa la generación de símbolos de depuración para que puede realizar el seguimiento de la. Símbolos de Java. Quítelo para las compilaciones de versión.  
  
    ```java
    jvc /g:t c:\<windows>\Java\trustlib\msado15\*.Java  
    ```  
  
3.  Para usar estos archivos, abra el proyecto en Visual J ++. Desde el **proyecto** menú, elija **agregar al proyecto**. Seleccione **archivos**y agregue todas las. Archivos de JAVA que se genera en el directorio trustlib\msado15 al proyecto.  
  
## <a name="see-also"></a>Vea también  
 [Contenedores de clase Java de ADO](../../../ado/guide/appendixes/ado-java-class-wrappers.md)   
