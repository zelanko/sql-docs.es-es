---
title: "Instalaci&#243;n de componentes de R sin acceso a Internet | Microsoft Docs"
ms.custom: ""
ms.date: "02/10/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0a90c438-d78b-47be-ac05-479de64378b2
caps.latest.revision: 30
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 21
---
# Instalaci&#243;n de componentes de R sin acceso a Internet
  El programa de instalación de los componentes de R usado por [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] requiere una conexión a Internet para el acceso a los archivos que se proporcionan en el Centro de descarga de Microsoft o en otro sitio de confianza. Sin embargo, puede instalar estos componentes en un servidor sin acceso a Internet realizando copias locales, como se describe en este tema.  
  
  > [!TIP]
  > 
  > Para obtener un tutorial detallado del proceso de instalación sin conexión, consulte este blog del [Equipo de asesoramiento al cliente de SQL Server](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/do-it-right-deploying-sql-server-r-services-on-computers-without-internet-access/).
  
## <a name="installation-on-computers-with-no-internet-access"></a>Instalación en equipos sin acceso a Internet  
 Si va a realizar una instalación sin conexión, [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] no tendrá acceso los vínculos para instalar los componentes de R necesarios. Para evitar este problema, puede descargar de forma local una copia de los instaladores y completar la instalación como se describe aquí.
 
 Tenga en cuenta que hay dos instaladores para los componentes de R: uno para Microsoft R Open y otro para Microsoft R Server. Debe descargar e instalar los dos para usar SQL Server R Services. El Asistente para la instalación de SQL Server se asegurará de que se instalen en el orden correcto.


Versión  |Vínculo de descarga  
---------|---------
**SQL Server 2016 RTM**     |           
Microsoft R Open     |[SRO_3.2.2.803_1033.cab](https://go.microsoft.com/fwlink/?LinkId=761266)     
Microsoft R Server     |[SRS_8.0.3.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=735051)      
**SQL Server 2016 CU 1**     |           
Microsoft R Open     |[SRO_3.2.2.10000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=808803)     
Microsoft R Server     |[SRS_8.0.3.10000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=808805)      
**SQL Server 2016 CU 2**     |           
Microsoft R Open     |[SRO_3.2.2.12000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=827398)     
Microsoft R Server     |[SRS_8.0.3.12000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=827399)  
**SQL Server 2016 CU 3**     |           
Microsoft R Open     |[SRO_3.2.2.13000_1033.cab: ](https://go.microsoft.com/fwlink/?LinkId=831785)     
Microsoft R Server     |[SRS_8.0.3.13000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=831676)  |
**SQL Server 2016 SP 1**     |           
Microsoft R Open     |[SRO_3.2.2.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824879)     
Microsoft R Server     |[SRS_8.0.3.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824881)  
**SQL Server 2016 SP 1 GDR**     |           
Microsoft R Open     |[SRO_3.2.2.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836819)     
Microsoft R Server     |[SRS_8.0.3.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836818)  

  
**Cómo actualizar los componentes de R en una instalación sin conexión**     

1. Use los vínculos mencionados anteriormente para descargar la versión adecuada.
2. Copie los archivos CAB en la carpeta del equipo en la que instalará la actualización.
3. Al ejecutar el Asistente para la instalación de SQL Server, haga clic en **Aceptar** en la página de licencia de Microsoft R.  Aparecerá un cuadro de diálogo con los vínculos de las descargas. Escriba la ruta de acceso a la ubicación de los archivos que ha descargado. 
4. Haga clic en **Siguiente** para indicar que los componentes están disponibles y complete el Asistente para la instalación de SQL Server.
5. También puede descargar el código fuente archivado de los componentes de código abierto. Para obtener más información, consulte [Configurar SQL Server R Services](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md).


> [!IMPORTANT] Si descarga los archivos .cab como parte de la instalación de SQL Server en un equipo con acceso a Internet, el Asistente para la instalación detectará el idioma local y cambiará automáticamente el idioma del instalador. 
> 
> Pero si está instalando una de las versiones localizadas de SQL Server en un equipo sin acceso a Internet y descarga los instaladores de R en un recurso compartido local, deberá editar manualmente el nombre de los archivos descargados e insertar el identificador de idioma correcto del idioma que va a instalar. 
> 
> Por ejemplo, si va a instalar la versión en japonés de SQL Server, deberá cambiar el nombre del archivo de SRS_8.0.3.0_1033.cab a SRS_8.0.3.0_1041.cab.    
 
  
## <a name="see-also"></a>Vea también  
 [Introducción a SQL Server R Services](../../advanced-analytics/r-services/getting-started-with-sql-server-r-services.md)   
 [Troubleshooting R Services Setup](../Topic/Troubleshooting%20R%20Services%20Setup.md) (Solución de problemas con el programa de instalación de R Services)  
  
  