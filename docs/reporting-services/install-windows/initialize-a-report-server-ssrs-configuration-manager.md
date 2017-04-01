---
title: "Inicializar un servidor de informes (Administrador de configuraci&#243;n de SSRS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/13/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "servidores de informes [Reporting Services], inicializar"
  - "proceso de inicialización [Reporting Services]"
  - "comprobar inicializaciones del servidor de informes"
  - "implementaciones escaladas [Reporting Services]"
  - "inicializar servidores de informes [Reporting Services]"
  - "comprobar inicializaciones del servidor de informes"
ms.assetid: 861d4ec4-1085-412c-9a82-68869a77bd55
caps.latest.revision: 10
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
---
# Inicializar un servidor de informes (Administrador de configuraci&#243;n de SSRS)
  En [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], un servidor inicializado es el que puede cifrar y descifrar los datos de una base de datos del servidor de informes. La inicialización es un requisito para la operación del servidor de informes. La inicialización se produce cuando el servicio Servidor de informes se inicia por primera vez. También ocurre cuando se une el servidor de informes a la implementación existente o se vuelven a crear manualmente las claves como parte del proceso de recuperación. Para obtener más información sobre cómo y por qué se usan las claves de cifrado, vea [Configurar y administrar las claves de cifrado &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/configure-and-manage-encryption-keys-ssrs-configuration-manager.md) y [Almacenar datos cifrados del servidor de informes &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/store-encrypted-report-server-data-ssrs-configuration-manager.md).  
  
 Las claves de cifrado se basan en parte en la información de perfil del servicio Servidor de informes. Si cambia la identidad del usuario que se utiliza para ejecutar el servicio Servidor de informes, debe actualizar las claves en consecuencia. Si utiliza la herramienta de configuración de Reporting Services para cambiar la identidad, el sistema controla automáticamente este paso.  
  
 Si por algún motivo se produce un error en la inicialización, el servidor de informes devuelve un error **RSReportServerNotActivated** en respuesta a las solicitudes del usuario y del servicio. En este caso, es posible que deba solucionar el problema de la configuración del sistema o del servidor. Para obtener más información, vea [SSRS: Solucionar problemas y errores con Reporting Services](http://social.technet.microsoft.com/wiki/contents/articles/1633.aspx) (http://social.technet.microsoft.com/wiki/contents/articles/1633.aspx) en la wiki de TechNet.  
  
## Información general sobre el proceso de inicialización  
 El proceso de inicialización crea y almacena una clave simétrica que se utiliza para el cifrado. Los Servicios de cifrado de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows crean la clave simétrica que el servicio Servidor de informes utiliza para cifrar y descifrar los datos. La clave simétrica se cifra con una clave asimétrica.  
  
 Los siguientes pasos describen el proceso de inicialización:  
  
1.  Durante el primer inicio, el servicio Servidor de informes lee el archivo RSReportServer.config para obtener el identificador de instalación e información de conexión con la base de datos.  
  
2.  El servicio Servidor de informes solicita una clave pública a los Servicios de cifrado. Windows crea una clave privada y una pública, y envía esta última al servicio Servidor de informes.  
  
3.  El servicio Servidor de informes se conecta a la base de datos del servidor de informes y almacena los valores del identificador de instalación y la clave pública.  
  
4.  El servicio Servidor de informes llama nuevamente a los Servicios de cifrado, pero esta vez para solicitar una clave simétrica. Windows crea la clave simétrica.  
  
5.  El servicio Servidor de informes se conecta de nuevo a la base de datos del servidor de informes y agrega la clave simétrica a los valores, que se almacenaron en el paso 3, correspondientes al identificador de instalación y de la clave pública. Antes de almacenarla, el servicio Servidor de informes utiliza su clave pública para cifrar la clave simétrica. Una vez almacenada la clave simétrica, se considera que el servidor de informes está inicializado y disponible para su uso.  
  
## Inicializar un servidor de informes para una implementación escalada  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] admite un modelo de implementación escalada que comparte una única base de datos del servidor de informes entre varias instancias del mismo. Para unir una implementación escalada, un servidor de informes debe crear y almacenar su copia de la clave simétrica en la base de datos compartida. Aunque los servidores que utilizan la base de datos emplean una única clave simétrica, cada servidor de informes tiene su copia de la clave. Cada copia es diferente puesto que se cifra de manera exclusiva con la clave pública que tiene.  
  
 Los primeros pasos para la inicialización de un servidor de informes en una implementación escalada son idénticos a los tres primeros pasos que describen la inicialización de una combinación única de servidor y base de datos.  
  
 El proceso de inicialización en una implementación escalada difiere en el modo en que el servidor de informes obtiene la clave simétrica. Cuando se inicializa el primer servidor, éste obtiene la clave simétrica de Windows. Cuando se inicializa el segundo servidor durante la configuración de una implementación escalada, éste obtiene la clave simétrica del servicio Servidor de informes que ya se inicializó. La primera instancia del servidor de informes utiliza la clave pública de la segunda instancia para crear una copia cifrada de la clave simétrica correspondiente a la segunda instancia del servidor de informes. La clave simétrica nunca se expone como texto simple en ningún momento durante este proceso.  
  
## Cómo inicializar un servidor de informes  
  
-   Para inicializar un servidor de informes, utilice la herramienta de configuración de Reporting Services. La inicialización se lleva a cabo automáticamente cuando se crea y configura la base de datos del servidor de informes. Para obtener más información, vea [Configurar una conexión a la base de datos del servidor de informes &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md).  
  
-   Para inicializar un servidor de informes en una implementación escalada, puede usar la página Inicialización de la herramienta de configuración de Reporting Services o la utilidad **RSKeymgmt**. Para seguir las instrucciones paso a paso, vea [Configurar una implementación escalada horizontalmente del servidor de informes en modo nativo &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/configure a native mode report server scale-out deployment.md).  
  
> [!NOTE]  
>  **RSKeymgmt** es una aplicación de consola que se puede ejecutar desde una línea de comandos del equipo que hospeda la instancia del servidor de informes que ya forma parte de una implementación escalada. Cuando ejecute la utilidad, especifique argumentos para seleccionar la instancia del servidor de informes remoto que desea inicializar.  
  
 Solo se inicializará un servidor de informes si el identificador de instalación y la clave pública coinciden. Si coinciden, se crea una clave simétrica que permite el cifrado reversible. Si no coinciden, el servidor de informes se deshabilita, en cuyo caso es posible que se le solicite al usuario que aplique una clave de copia de seguridad o elimine los datos cifrados si no se encuentra disponible una clave de seguridad o si ésta no es válida. Para obtener más información sobre las claves de cifrado que usa un servidor de informes, vea [Configurar y administrar las claves de cifrado &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/configure-and-manage-encryption-keys-ssrs-configuration-manager.md).  
  
> [!NOTE]  
>  También puede utilizar el proveedor de Instrumental de administración de Windows (WMI) de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para inicializar un servidor de informes mediante programación. Para obtener más información, vea [Obtener acceso al proveedor WMI de Reporting Services](../../reporting-services/tools/access-the-reporting-services-wmi-provider.md) en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## Cómo confirmar la inicialización de un servidor de informes  
 Para confirmar la inicialización del servidor de informes, haga ping al servicio web del servidor de informes escribiendo **http://\<nombreDeServidor>/reportserver** en la ventana de comandos. Si se produce el error **RSReportServerNotActivated** , no se produce la inicialización.  
  
## Vea también
[Configurar y administrar claves de cifrado (Administrador de configuración de SSRS)](../../reporting-services/install-windows/configure-and-manage-encryption-keys-ssrs-configuration-manager.md)
  
  