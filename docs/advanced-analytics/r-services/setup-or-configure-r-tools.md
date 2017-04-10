---
title: "Instalar o configurar herramientas de R | Microsoft Docs"
ms.custom: ""
ms.date: "01/20/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 7c04ae30-d391-4369-9742-d2b275e14c0d
caps.latest.revision: 9
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 8
---
# Instalar o configurar herramientas de R
  Microsoft R Server proporciona todas las bibliotecas de R base, los paquetes de R de escala y herramientas estándar de R que necesita para desarrollar y probar código R. Sin embargo, si desea usar un entorno de desarrollo de R dedicado, hay varios disponibles, incluidos muchas herramientas gratuitas.  
  
## <a name="basic-r-tools"></a>Herramientas de R básica  
 No se requieren herramientas adicionales en una instalación de Microsoft R Server, porque todos lo R estándar de las herramientas que se incluyen en un *base instalación* de R se instalan de forma predeterminada.

-   **RTerm**: una herramienta de línea de comandos para ejecutar scripts de R 
  
-   **RGui.exe**: un simple editor interactivo para R. Los argumentos de línea de comandos son los mismos para RGui.exe y RTerm. 
  
-   **RScript**: una herramienta de línea de comandos para ejecutar código R secuencias de comandos en modo por lotes.  

De forma predeterminada, estas herramientas se instalan en las siguientes carpetas:
- SQL Server 2016: `C:\Program Files\Microsoft SQL Server\130\R_SERVER\bin\x64`  
- VNext de SQL Server: `C:\Program Files\Microsoft SQL Server\140\R_SERVER\bin\x64`  

> [!TIP]  
>  ¿Necesita ayuda? Documentación de las herramientas de R puede encontrarse en la carpeta de instalación: `C:\Program Files\Microsoft SQL Server\R_SERVER\doc` y en `C:\Program Files\Microsoft SQL Server\R_SERVER\doc\manual`.  
>   
>  O bien, simplemente abra **RGui**, haga clic en **Ayuda**, y seleccione una de las opciones.  

## <a name="microsoft-r-client"></a>Cliente de Microsoft R

Cliente de Microsoft R es una descarga gratuita que le permite desarrollar soluciones de R que se pueden ejecutar fácilmente en Microsoft R Server o SQL Server R Services.

Normalmente se instala un entorno de desarrollo de R diferente, como R Tools para Visual Studio o RStudio y, a continuación, especificar que el cliente de Microsoft R se usa como el ejecutable de R. Esto proporciona acceso completo a del paquete RevoScaleR y otras características de Microsoft R Server.

También puede usar herramientas conocidas como RGui y RTerm para ejecutar secuencias de comandos o escribir y ejecutar código de R ad hoc.

[Instalar el cliente de Microsoft R](https://msdn.microsoft.com/microsoft-r/r-client-install)
  
##  <a name="a-namebkmkrtoolsa-r-tools-for-visual-studio"></a> R Tools para Visual Studio  

 Por comodidad cuando se trabaja con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bases de datos, considere el uso de [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)] como entorno de desarrollo. [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)] es un complemento gratuito para Visual Studio que funciona en todas las ediciones de Visual Studio. Visual Studio también proporciona compatibilidad para la integración de Python y F #.  

Para obtener más información, consulte [VisualStudio.com](https://www.visualstudio.com/vs/rtvs/).

 Esta sección describe cómo instalar [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)] con gratuita Community Edition de Visual Studio.  
  
#### <a name="install-visual-studio"></a>Instalar Visual Studio  
  
1.  La edición gratuita Community de Visual Studio está disponible para su descarga desde esta página: [Comunidad de Visual Studio](http://visualstudio.com/products/visual-studio-community-vs.aspx)  
  
2.  Cuando se completa la descarga, haga clic en **ejecutar** y seleccione los componentes que desea instalar.  
  
     Si lo hace una instalación personalizada, tenga en cuenta que los componentes de Microsoft Web Developer son necesarios.  
  
3.  Elija la **General** establecer por el momento. Al instalar [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)], tendrá el toption para cambiar a un diseño personalizado para el desarrollo de R.  

#### <a name="add-the-r-tools"></a>Agregar las herramientas de R

Después de instalar Visual Studio, las extensiones están disponibles para R, Python y muchos otros lenguajes a través de la **opciones** menú.

4. Haga clic en herramientas de la barra de menús y, a continuación, seleccione **extensiones y actualizaciones**.

5. Casi al final de la instalación, las herramientas de R detectará las versiones del runtime de R que están disponibles en el equipo y le preguntará si desea cambiar el entorno de desarrollo para usar el runtime de R para Microsoft R Server o el tiempo de ejecución de R para el cliente de Microsoft R.

Si el programa de instalación no detecta el tiempo de ejecución de R Server que desea usar, puede cambiarlo manualmente en cualquier momento mediante el uso de la **opciones** menú. Para obtener más información, vea [Configurar el IDE](https://msdn.microsoft.com/microsoft-r/r-client-get-started#step-2-configure-your-ide).

## <a name="rstudio"></a>RStudio

Si prefiere usar RStudio, siga estos pasos adicionales para usar las bibliotecas de RevoScaleR:
- Instalar Microsoft R Server o Microsoft R cliente para obtener los paquetes necesarios y las bibliotecas.
- Actualizar la ruta de acceso de R para usar el runtime de R adecuado.

Para obtener más información, vea [Configurar el IDE](https://msdn.microsoft.com/microsoft-r/r-client-get-started#step-2-configure-your-ide).


## <a name="see-also"></a>Vea también  
 [Crear un R Server independiente](../../advanced-analytics/r-services/create-a-standalone-r-server.md)   
 [Introducción a Microsoft R Server &#40; Independiente &#41;](../../advanced-analytics/r-services/getting-started-with-microsoft-r-server-standalone.md)  
  
  