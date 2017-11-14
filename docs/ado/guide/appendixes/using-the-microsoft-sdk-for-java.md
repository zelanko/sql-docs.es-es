---
title: Mediante el SDK de Microsoft para Java | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology:
- drivers
ms.custom: 
ms.date: 02/15/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Java (Microsoft SDK for)
- Microsoft SDK for Java [ADO]
ms.assetid: 2d7cb5b5-8307-49dd-b07e-c07069bb1626
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b7473f3a8772c53834c964071c2385736ff45cbf
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="using-the-microsoft-sdk-for-java"></a>Mediante el SDK de Microsoft para Java

> [!IMPORTANT]
> Microsoft no incluye compatibilidad de Visual J ++ en enero de 2004.

El SDK de Microsoft para Java es el kit de desarrollo para el entorno de Microsoft Internet Explorer. Herramientas, información y ejemplos se proporcionan para ayudarle a desarrollar programas Java y applets en función de JDK 1.1 y la máquina virtual de Microsoft Win32 (VM de Microsoft). El SDK de Microsoft para Java no está vinculado a Microsoft Visual J ++. Para descargar este SDK, haga clic aquí.  
  
 La utilidad Jactivex.exe genera clases a partir de una biblioteca de tipos, pero solo se puede invocar en la línea de comandos. Esta característica no está integrada con el entorno de desarrollo de Visual J ++. A diferencia de las clases generadas por el Asistente para la biblioteca de tipos de Java, puede ir a los contenedores de clase creados por el SDK. Esto es útil para depurar cómo el código utiliza las clases contenedoras de ADO.  
  
 Este mecanismo lee la biblioteca de tipos de ADO y genera las clases que se pueden crear instancias en la aplicación. Genera las clases en la siguiente ubicación: \\< directorio de windows\>\Java\trustlib\msado15.  
  
 Crear una aplicación ADO en Java mediante el SDK de Microsoft para Java es fundamentalmente idéntica, desde la perspectiva del código fuente, al usar al Asistente para la biblioteca de tipos de Java. Para obtener código de ejemplo, vea [contenedores de clase Java de ADO](../../../ado/guide/appendixes/ado-java-class-wrappers.md). La única diferencia está en cómo se generan las clases contenedoras en primer lugar, como se muestra en los pasos siguientes.  
  
### <a name="to-create-an-ado-project-with-the-microsoft-sdk-for-java"></a>Para crear un proyecto de ADO con Microsoft SDK para Java  
  
1.  Ejecute lo siguiente en un símbolo del sistema. Debe establecer la ruta de acceso para incluir el SDK de Microsoft para el directorio Bin de Java o ejecute el comando desde esa ubicación. Normalmente, el SDK de Microsoft para Java se instala en la misma ubicación que Visual Studio. Se trata de una instrucción de comando único.  
  
    ```  
    \<path to DevStudio>\<path to Java SDK>\bin\JactiveX.exe /javatlb "C:\program files\common files\system\ado\msado15.dll"  
    ```  
  
2.  Ejecute el siguiente comando para compilar las clases generadas. El modificador/g: t activa la generación de símbolos de depuración para que puede realizar un seguimiento en el. Símbolos de Java. Quitarlo para versiones de lanzamiento.  
  
    ```  
    jvc /g:t c:\<windows>\Java\trustlib\msado15\*.Java  
    ```  
  
3.  Para utilizar estos archivos, abra el proyecto de Visual J ++. Desde el **proyecto** menú, elija **agregar al proyecto**. Seleccione **archivos**y agregue todos los. Archivos de JAVA generados en el directorio trustlib\msado15 al proyecto.  
  
## <a name="see-also"></a>Vea también  
 [Contenedores de clase Java de ADO](../../../ado/guide/appendixes/ado-java-class-wrappers.md)   

