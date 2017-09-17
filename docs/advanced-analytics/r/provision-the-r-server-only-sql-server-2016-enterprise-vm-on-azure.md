---
title: "Aprovisionar la máquina virtual de R Server Only SQL Server 2016 Enterprise | Microsoft Docs"
ms.custom: 
ms.date: 06/05/2017
ms.prod: r-server
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c8826df7-aa67-4768-baa9-bdc875c4a766
caps.latest.revision: 12
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a3bfca0753984f09220d8ca4e4f6933c949daf2b
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="advanced-analytics-virtual-machines-on-azure"></a>Máquinas virtuales de análisis avanzado en Azure

Máquinas virtuales en Azure son una opción adecuada para configurar rápidamente un entorno de servidor completa para las soluciones de aprendizaje automático. Este tema enumeran algunas imágenes de máquina virtual que contienen R Server, SQL Server con aprendizaje automático u otras herramientas de ciencia de datos de Microsoft.

> [!TIP]
> Recomendamos que utilice la nueva versión del portal de Azure y Azure Marketplace. Algunas imágenes no están disponibles al examinar la Galería de Azure en el portal clásico.

Azure Marketplace contiene varias máquinas virtuales que admiten la ciencia de datos. Esta lista no pretende ser exhaustiva, pero solo proporciona los nombres de las imágenes que incluyen servicios, para facilitar la detección de aprendizaje de automático de Microsoft R Server o SQL Server.

## <a name="how-to-provision-a-vm"></a>Cómo aprovisionar una máquina virtual

Si está familiarizado con el uso de máquinas virtuales de Azure, se recomienda que consulte los siguientes artículos para obtener más información sobre cómo usar el portal y configurar una máquina virtual.

+ [Máquinas virtuales: introducción](https://azure.microsoft.com/documentation/learning-paths/virtual-machines/)
+ [Introducción a máquinas virtuales de Windows](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-windows-hero-tutorial/)

### <a name="find-an-image"></a>Buscar una imagen

1. En el panel de Azure, haga clic en **Marketplace**.

    - Haga clic en **Intelligence y análisis** o **bases de datos**, y, a continuación, escriba "R" en el **filtro** control para ver una lista de máquinas virtuales del servidor de R.
    - Las cadenas de los otros posibles para la **filtro** control son *ciencia de datos* y *aprendizaje automático*
    - Usar el carácter comodín % en la búsqueda para buscar nombres de máquinas virtuales que contienen una cadena de destino, como *R* o *Julia*.

2. Para obtener R Server para Windows, seleccione **R Server solo SQL Server 2016 Enterprise**.
  
    [R Server](https://msdn.microsoft.com/microsoft-r/rserver-whats-new) tiene licencia como una característica de SQL Server Enterprise Edition, pero la versión 9.1. se instala como un servidor independiente y realizando tareas de mantenimiento en la directiva de soporte técnico de ciclo de vida moderna.

3. Una vez que se crea la máquina virtual y entra en ejecución, haga clic en el botón **Conectar** para abrir una conexión e iniciar sesión en la máquina nueva.

4. Después de conectarse, debe instalar las herramientas de R adicionales o herramientas de desarrollo.

### <a name="install-additional-r-tools"></a>Instalar herramientas de R adicionales

De manera predeterminada, Microsoft R Server incluye todas las herramientas de R que se instalan en una instalación base de R, incluido RTerm y RGui. Se agregó un acceso directo a RGui en el escritorio, en caso de que desee comenzar a usar R de inmediato.

Sin embargo, podría desea instalar las herramientas de R adicionales, como RStudio, las herramientas de R para Visual Studio (RTV) o Microsoft R Client. Consulte los vínculos siguientes para ver ubicaciones e instrucciones de descarga:
+ [Herramientas de R para Visual Studio](https://docs.microsoft.com/visualstudio/rtvs/installation)
+ [Cliente de Microsoft R](https://msdn.microsoft.com/microsoft-r/install-r-client-windows)
+ [RStudio para Windows](https://www.rstudio.com/products/rstudio/download/)

Una vez completada la instalación, asegúrese de cambiar la ubicación en tiempo de ejecución de R predeterminada para que todas las herramientas de desarrollo de R usen bibliotecas de Microsoft R Server.

### <a name="configure-server-for-web-services"></a>Configurar servidor para los servicios web

Si la máquina virtual incluye R Server, hay que configurar más opciones para usar la implementación del servicio web, la ejecución remota o usar R Server como un servidor de implementación en la organización. Para obtener instrucciones, vea [Configure R Server for Operationalization](https://msdn.microsoft.com/microsoft-r/operationalize/configuration-initial) (Configurar R Server para hacerlo operativo).

> [!NOTE]
> No se necesita configuración adicional si desea utilizar paquetes como RevoScaleR o MicrosoftML.

## <a name="r-server-images"></a>Imágenes de servidor de R

### <a name="microsoft-data-science-virtual-machine"></a>Microsoft Data Science Virtual Machine

Viene configurado con Microsoft R Server, así como Python (distribución de Anaconda), un servidor de Jupyter notebook, Visual Studio Community Edition, Power BI Desktop, el SDK de Azure y SQL Server Express edition.

La versión de Windows se ejecuta en Windows Server 2012 y contiene muchas herramientas especiales para el modelado y análisis, incluidos CNTK y mxnet, los paquetes de R populares como xgboost y Vowpal Wabbit.

### <a name="linux-data-science-virtual-machine"></a>Máquina Virtual de ciencia de datos de Linux

También contiene herramientas conocidas para datos informática y desarrollo de actividades, incluidos los blocs de notas de Microsoft R Open, Microsoft R Server Developer Edition, Python Anaconda y Jupyter de Python, R y Julia.

Esta imagen de máquina virtual se ha actualizado recientemente para incluir JupyterHub, software de código abierto que permite el uso por varios usuarios a través de diferentes métodos de autenticación, incluida la autenticación de cuentas de sistema operativo local y la autenticación de cuenta de Github. JupyterHub es una opción útil si desea ejecutar una clase de aprendizaje y desea que todos los alumnos para compartir el mismo servidor, pero usa blocs de notas independientes y directorios.

Las imágenes se proporcionan para Ubuntu, Centos y Centos CSP.

### <a name="r-server-only-sql-server-2016-enterprise"></a>R Server solo SQL Server 2016 Enterprise

Esta máquina virtual incluye un instalador independiente para [R Server 9.1.](https://msdn.microsoft.com/microsoft-r/rserver-whats-new) es compatible con el nuevo modelo de licencia actual del ciclo de vida del Software.

 R Server también está disponible en imágenes para la versión de CentOS Linux 7.2, versión de Linux RedHat 7.2 y Ubuntu versión 16.04.

 > [!NOTE]
 > Estas máquinas virtuales reemplazan a **RRE for Windows Virtual Machine**, que antes estaba disponible en Azure Marketplace.

## <a name="sql-server-images"></a>Imágenes de SQL Server

Para usar R Services (In-Database) o los servicios de aprendizaje de máquina, debe instalar una de las máquinas virtuales de edición SQL Server Enterprise o Developer y agregar el servicio, de aprendizaje automático como se describe aquí: [Installing SQL Server R Services en un Máquina Virtual de Azure](../../advanced-analytics/r-services/installing-sql-server-r-services-on-an-azure-virtual-machine.md).

> [!NOTE]
> Actualmente, los servicios de aprendizaje de máquina no se admiten en las máquinas virtuales de Linux para SQL Server 2017, o en la base de datos de SQL Azure. Debe utilizar SQL Server 2016 SP1 o SQL Server 2017 para Windows.

La máquina Virtual de ciencia de datos también incluye SQL Server 2016 con la característica de servicios de R ya habilitada.


## <a name="other-vms"></a>Otras máquinas virtuales

### <a name="deep-learning-toolkit-for-the-data-science-virtual-machine"></a>Profundidad de aprendizaje Kit de herramientas para la máquina Virtual de ciencia de datos

Esta máquina virtual contiene el mismo equipo aprendizaje herramientas disponibles en la máquina Virtual de ciencia de datos, pero con las versiones GPU de mxnet, CNTK, TensorFlow y Keras. Esta imagen puede usarse solo en las instancias de Azure GPU N-series. 

El Kit de herramientas de aprendizaje profundo también proporciona un conjunto de ejemplo profundo soluciones que usan la GPU, como reconocimiento de imágenes en la base de datos de CIFAR-10 y un ejemplo de reconocimiento de caracteres en la base de datos MNIST de aprendizaje. Instancias GPU están actualmente disponibles en Ee.uu. Central sur, este de EE., Europa occidental y sudeste de Asia.

> [!IMPORTANT]
> Las instancias de GPU solo están disponibles actualmente en el centro y sur de EE. UU.


## <a name="frequently-asked-questions"></a>Preguntas más frecuentes

### <a name="can-i-install-a-virtual-machine-with-sql-server-2017"></a>¿Se puede instalar una máquina virtual con SQL Server 2017?

Las imágenes son disponibles que contienen 2017 CTP 2.0 de SQL Server para entornos de Linux, pero estos entornos no admiten actualmente servicios de aprendizaje de máquina. 

Una máquina de virtual basada en Windows para SQL Server de 2017 Enterprise Edition que incluye servicios de aprendizaje de máquina estará disponible después de la publicación. 

Como alternativa, puede usar la imagen de SQL Server 2016 y actualizar la instancia de R como se describe aquí: [actualizar una instancia con SqlBindR](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md). 

O bien, crear una máquina virtual y descargue la versión de CTP 2.0 preliminar de [SQL Server 2017](https://www.microsoft.com/sql-server/sql-server-2017).

### <a name="how-do-i-access-data-in-an-azure-storage-account"></a>¿Cómo se tiene acceso a los datos de una cuenta de almacenamiento de Azure?

Cuando tenga que usar los datos de su cuenta de almacenamiento de Azure, habrá varias opciones para obtener acceso a los datos o moverlos:

+ Copie los datos de la cuenta de almacenamiento al sistema de archivos local con una utilidad, como [AzCopy](https://azure.microsoft.com/documentation/articles/storage-use-azcopy/#copy-files-in-azure-file-storage-with-azcopy-preview-version-only). 

+ Agregue los archivos a un recurso compartido de archivos en la cuenta de almacenamiento y, luego, monte el recurso compartido de archivos como una unidad de red en la máquina virtual.  Para más información, consulte [Montaje de archivos de Azure](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-files/). 

### <a name="how-do-i-use-data-from-azure-data-lake-storage-adls"></a>¿Cómo se usan los datos de una cuenta de Azure Data Lake Storage (ADLS)?

Puede leer datos desde el almacenamiento ADLS con RevoScaleR, si hace referencia a la cuenta de almacenamiento de sistema de archivos de la misma manera que lo haría con un HDFS utilizando webHDFS.  Para obtener más información, consulte este artículo: [usar R para realizar operaciones de sistema de archivos en el almacén de Azure Data Lake](https://blogs.msdn.microsoft.com/microsoftrservertigerteam/2017/03/14/using-r-to-perform-filesystem-operations-on-azure-data-lake-store/).

## <a name="see-also"></a>Vea también

[SQL Server R Services](https://msdn.microsoft.com/library/mt604845.aspx)


