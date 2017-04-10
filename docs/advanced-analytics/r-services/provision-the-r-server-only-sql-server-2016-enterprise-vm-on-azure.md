---
title: "Aprovisionar la m&#225;quina virtual de R Server Only SQL Server 2016 Enterprise | Microsoft Docs"
ms.custom: ""
ms.date: "12/22/2016"
ms.prod: "r-server"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c8826df7-aa67-4768-baa9-bdc875c4a766
caps.latest.revision: 12
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 5
---
# Aprovisionar la m&#225;quina virtual de R Server Only SQL Server 2016 Enterprise

La máquina virtual de R Server Only SQL Server 2016 Enterprise en Azure es una opción nueva de configuración rápida y fácil de un entorno de servidor para admitir soluciones de R. Esta máquina virtual de Azure está preconfigurada con Microsoft R Server (independiente). 

Esta nueva máquina virtual reemplaza RRE para máquina virtual de Windows que anteriormente estaba disponible en Azure Marketplace. 

Esta máquina virtual también incluye DeployR Enterprise, para implementar el análisis de R dentro de las aplicaciones y los sistemas de backend. Para más información, consulte [Acerca de Deploy R](https://msdn.microsoft.com/microsoft-r/deployr-about).


## Aprovisionar la máquina virtual de R Server

Si no conoce las máquinas virtuales de Azure, le recomendamos que lea este artículo para más información sobre cómo usar el portal y configurar una máquina virtual.
[Máquinas virtuales: introducción](https://azure.microsoft.com/documentation/learning-paths/virtual-machines/)

Para crear la máquina virtual de R Server desde Microsoft Azure Marketplace 
1. Haga clic en **Máquinas virtuales** y escriba *R Server* en el cuadro de búsqueda.
2. Seleccione **R Server Only SQL Server 2016 Enterprise**
3. Siga aprovisionando la máquina virtual tal como se indica en este artículo: [https://azure.microsoft.com/documentation/articles/virtual-machines-windows-hero-tutorial/](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-windows-hero-tutorial/) 
7. Una vez que se crea la máquina virtual y entra en ejecución, haga clic en el botón **Conectar** para abrir una conexión e iniciar sesión en la máquina nueva.
8. Cuando se conecta, el **Administrador de servidores** se abre de manera predeterminada, pero no se requiere ninguna configuración de servidor adicional. Cierre el **Administrador de servidores** para ver el escritorio y siga con los pasos siguientes:
    + Instalación de herramientas de desarrollo o herramientas de R adicionales
    + Configuración de DeployR  

Para ubicar la máquina virtual de R Server en el Portal de Azure clásico
1. Haga clic en **Máquinas virtuales** y, luego, en **NUEVO**.
2. En el panel **Nuevo**, ya deben estar seleccionadas las opciones **Proceso** y **Máquina virtual**. 
3. Haga clic en **Desde Galería** para ubicar la imagen de máquina virtual. Puede escribir *R Server* en el cuadro de búsqueda, o bien hacer clic en **Microsoft** y desplazarse hacia abajo hasta ver **R Server Only SQL Server 2016 Enterprise**.


## Instalar herramientas de R
De manera predeterminada, Microsoft R Server incluye todas las herramientas de R que se instalan en una instalación base de R, incluido RTerm y RGui. Se agregó un acceso directo a RGui en el escritorio, en caso de que desee comenzar a usar R de inmediato.

Sin embargo, puede que desee instalar herramientas de R adicionales, como RStudio, Herramientas de R para Visual Studio o Cliente de Microsoft R. Consulte los vínculos siguientes para ver ubicaciones e instrucciones de descarga:
+ [Herramientas de R para Visual Studio](https://www.visualstudio.com/features/rtvs-vs.aspx)
+ [Cliente de Microsoft R](https://msdn.microsoft.com/microsoft-r/install-r-client-windows)
+ [RStudio para Windows](https://www.rstudio.com/products/rstudio/download/)

Una vez que instale estas herramientas, asegúrese de dirigir sus herramientas a las bibliotecas de R Server.

## Uso de DeployR en la máquina virtual

Se requieren algunos pasos adicionales para usar la instancia de DeployR instalada en esta máquina virtual. 

Para configurar la instancia de DeployR:

1. En la máquina virtual, abra la **utilidad Administrador de DeployR**.
2. Establezca la contraseña del administrador de DeployR tal como se describe aquí: [Pasos posteriores a la instalación](https://msdn.microsoft.com/microsoft-r/deployr-install-on-windows).
3. Establezca el contexto web de DeployR. Para más información, consulte [DeployR Admin Installation in the Cloud](https://msdn.microsoft.com/microsoft-r/deployr-admin-install-in-cloud) (Instalación del administrador de DeployR en la nube). 
4. Abra los puestos correspondientes en la máquina virtual tal como se describe aquí: [Configuración de Puntos de conexión de Azure](https://msdn.microsoft.com/microsoft-r/deployr-admin-install-in-cloud#configuring-azure-endpoints). 
4. Actualice el Firewall de Windows tal como se indica aquí: [Actualización del firewall](https://msdn.microsoft.com/microsoft-r/deployr-admin-install-in-cloud#updating-the-firewall). 

## Acceso a los datos de una cuenta de almacenamiento de Azure 

Cuando tenga que usar los datos de su cuenta de almacenamiento de Azure, habrá varias opciones para obtener acceso a los datos o moverlos:


+ Copie los datos de la cuenta de almacenamiento al sistema de archivos local con una utilidad, como [AzCopy](https://azure.microsoft.com/documentation/articles/storage-use-azcopy/#copy-files-in-azure-file-storage-with-azcopy-preview-version-only). 

+ Agregue los archivos a un recurso compartido de archivos en la cuenta de almacenamiento y, luego, monte el recurso compartido de archivos como una unidad de red en la máquina virtual.  Para más información, consulte [Montaje de archivos de Azure](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-files/). 

## Uso de los datos en una cuenta de Azure Data Lake Storage (ADLS)

Puede leer datos desde el almacenamiento ADLS con ScaleR, si hace referencia a la cuenta de almacenamiento tal como lo haría con un sistema de archivos HDFS, es decir, con webHDFS.  Para más información, consulte esta [guía de configuración](http://go.microsoft.com/fwlink/?LinkId=723452).

## Recursos

Puede encontrar información adicional sobre Microsoft R en MSDN: [R Server y Scale R](https://msdn.microsoft.com/microsoft-r)  


Consulte estos recursos adicionales para obtener información sobre R en general: 
+ [DataCamp](http://www.datacamp.com) Ofrece un curso de introducción e intermedio gratuito de R, además de un curso sobre cómo trabajar con macrodatos con Revolution R.
+ [Stack Overflow](http://www.stackoverflow.com) Un excelente recurso para responder preguntas sobre las herramientas de ML y la programación en R. 
+ [Cross Validated](https://stats.stackexchange.com/) Sitio para preguntas sobre temas problemas estadísticos en el aprendizaje automático.
+ [Archivos de listas de distribución de correo de ayuda de R](https://www.r-project.org/mail.html) Excelente recurso con información histórica. 
+ [Sitio web de MRAN](https://mran.microsoft.com/documents/getting-started/) Muchos otros recursos de R.  

## Vea también
[SQL Server R Services](https://msdn.microsoft.com/library/mt604845.aspx)
