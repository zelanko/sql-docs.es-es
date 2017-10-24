---
title: "Aprovisionar una máquina virtual para el aprendizaje automático de Azure | Documentos de Microsoft"
ms.custom: 
ms.date: 10/16/2017
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
ms.sourcegitcommit: 8cc1fcfdeae8742a93916dfb08c9db1215f88721
ms.openlocfilehash: 7cb9e069fc3b537f8aab9d048a152435ad0cc6ac
ms.contentlocale: es-es
ms.lasthandoff: 10/17/2017

---
# <a name="provision-a-virtual-machine-for-machine-learning-on-azure"></a>Aprovisionar una máquina virtual para el aprendizaje automático de Azure

Máquinas virtuales en Azure son una opción adecuada para configurar rápidamente un entorno de servidor completa para las soluciones de aprendizaje automático. Este artículo enumeran algunas imágenes de máquina virtual que contienen R Server, servidor de aprendizaje de máquina o SQL Server con aprendizaje automático.

Esta lista no pretende ser exhaustiva, pero solo proporciona los nombres de las imágenes que están relacionados con servidor de aprendizaje de máquina o servicios de aprendizaje de máquina de SQL Server, para facilitar la detección.

> [!TIP]
> Recomendamos que utilice la nueva versión del portal de Azure y Azure Marketplace. Algunas imágenes no están disponibles al examinar la Galería de Azure en el portal clásico.

## <a name="how-to-provision-a-virtual-machine"></a>Cómo aprovisionar una máquina virtual

Si está familiarizado con el uso de máquinas virtuales de Azure, se recomienda que consulte los siguientes artículos para obtener más información sobre cómo usar el portal y configurar una máquina virtual.

+ [Máquinas virtuales: introducción](https://azure.microsoft.com/documentation/learning-paths/virtual-machines/)
+ [Introducción a máquinas virtuales de Windows](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-hero-tutorial/)

## <a name="find-a-machine-learning-image"></a>Buscar una imagen de aprendizaje de máquina

1. En el portal de Azure (portal.azure.com), haga clic en **máquinas virtuales**, o haga clic en **nuevo**.

2. Busque el cuadro de búsqueda en la parte superior de la página, que puede usar para filtrar los recursos por nombre. 

3. Escriba "Servidor de R" (o "Servidor de aprendizaje automático") en el **filtro** control para ver una lista de recursos relacionados. Haga clic en **búsqueda en Marketplace** para ver máquinas virtuales.

    > [!TIP]
    > 
    > Otras cadenas para el control de filtro posibles son "ciencia de datos" y "aprendizaje automático".
    > 
    > Use la `%` comodín en la búsqueda para buscar los nombres de las máquinas virtuales. Por ejemplo, puede escribir `"`% Julia %` or `%%R '.

4. Para obtener R Server para Windows, seleccione **R Server solo SQL Server 2016 Enterprise**.
  
    [R Server](https://msdn.microsoft.com/microsoft-r/rserver-whats-new) se autoriza el uso como una característica de SQL Server Enterprise Edition, pero la versión 9.1 se instala como un servidor independiente y se repara en la directiva de soporte técnico de ciclo de vida moderna.

    > [!NOTE] 
    > 
    > Esto se encuentran, busque en la versión de una máquina virtual nueva que incluya 2017 de SQL Server y el 9.2.1 versión del servidor de aprendizaje de máquina.
    > Hasta entonces, puede actualizar la versión de SQL Server instalada en esta máquina virtual mediante el centro de instalación de SQL Server y elegir la opción de actualización. Para obtener más información, consulte [actualizar SQL Server mediante el Asistente para la instalación](https://docs.microsoft.com/sql/database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup).

5. Después de la máquina virtual se ha creado y se está ejecutando, haga clic en el **conectar** botón para abrir una conexión e iniciar sesión en la nueva máquina.

5. Después de conectarse, puede instalar el paquete de R adicional o la herramienta de desarrollo preferido.

### <a name="install-additional-r-tools"></a>Instalar herramientas de R adicionales

De manera predeterminada, Microsoft R Server incluye todas las herramientas de R que se instalan en una instalación base de R, incluido RTerm y RGui. También se agregó un acceso directo a RGui al escritorio.

Sin embargo, podría desea instalar las herramientas de R adicionales, como RStudio, R Tools para Visual Studio (RTV) o el cliente de Microsoft R. Consulte los vínculos siguientes para ver ubicaciones e instrucciones de descarga:

+ [Herramientas de R para Visual Studio](https://docs.microsoft.com/visualstudio/rtvs/installation)
+ [Cliente de Microsoft R](https://msdn.microsoft.com/microsoft-r/install-r-client-windows)
+ [RStudio para Windows](https://www.rstudio.com/products/rstudio/download/)

Una vez completada la instalación, asegúrese de cambiar la ubicación en tiempo de ejecución de R predeterminada para que todas las herramientas de desarrollo de R usen bibliotecas de Microsoft R Server.

### <a name="configure-r-server-to-support-web-services"></a>Configurar el servidor de R para que admita servicios web

Configuración adicional es necesaria para utilizar la implementación del servicio web, ejecución remota, o para aprovechar R Server como un servidor de implementación en su organización. Para obtener instrucciones, consulte [configuración del servidor de R para hacer operativos los análisis](https://docs.microsoft.com/machine-learning-server/install/operationalize-r-server-one-box-config).

> [!NOTE]
> No se necesita configuración adicional si desea utilizar paquetes como RevoScaleR o MicrosoftML.

## <a name="other-virtual-machines"></a>Otras máquinas virtuales

Las imágenes siguientes están disponibles en Azure Marketplace y son totalmente configuradas equipo herramientas de aprendizaje, pero no necesariamente incluye SQL Server.

### <a name="data-science-virtual-machine"></a>Máquina Virtual de ciencia de datos

Esta imagen está preconfigurada con Microsoft R Server, así como Python (distribución de Anaconda), un servidor de Jupyter notebook, Visual Studio Community Edition, Power BI Desktop, el SDK de Azure y SQL Server Express edition.

La versión de Windows se ejecuta en Windows Server 2012 y contiene muchas herramientas especiales para el modelado y análisis, incluyendo [CNTK](https://www.microsoft.com/cognitive-toolkit/), [mxNet](https://mxnet.incubator.apache.org/), y paquetes de R popular como **xgboost**.

Ediciones de Linux se proporcionan para Ubuntu, Centos y CSP de Centos y contienen muchas herramientas populares para las actividades de desarrollo y la ciencia de datos.

Para obtener más información, consulte [Introducción a Azure Data Science Virtual Machine para Linux y Windows](https://docs.microsoft.com/azure/machine-learning/data-science-virtual-machine/provision-vm).

Esta imagen se ha actualizado recientemente para incluir: 

+ Compatibilidad con Julia, el lenguaje de ciencia de datos escalable y eficaz del futuro 
+ JupyterHub, que es una opción útil cuando desea ejecutar una clase de aprendizaje y desea que todos los alumnos para compartir el mismo servidor, pero usa blocs de notas independientes y directorios.

Para obtener más información sobre herramientas compatibles y marcos de trabajo de aprendizaje de máquina, vea [conocer la máquina Virtual de ciencia de datos](https://docs.microsoft.com/azure/machine-learning/data-science-virtual-machine/dsvm-tools-overview)

### <a name="r-server-virtual-machines"></a>Máquinas virtuales del servidor de R

Además el **R Server solo SQL Server 2016 Enterprise** imagen, puede obtener las máquinas virtuales independientes que contienen R Server. Las imágenes están disponibles para la versión de CentOS Linux 7.2, versión de Linux RedHat 7.2 y Ubuntu versión 16.04.

Para obtener más información, vea [servidor de aprendizaje de máquina en la nube](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-in-the-cloud)

 > [!NOTE]
 > Estas máquinas virtuales reemplazan a **RRE for Windows Virtual Machine**, que antes estaba disponible en Azure Marketplace.

### <a name="sql-server-virtual-machines"></a>Máquinas virtuales de SQL Server

Hay dos opciones para el uso de aprendizaje en Azure automático de SQL Server:

+ Obtener una de las imágenes de máquina virtual que incluye SQL Server R Services preinstalado.
+ Crear una máquina virtual de Azure e instalar SQL Server Enterprise o Developer edition con su propia clave de licencia. 
  
    A continuación, ejecute el programa de instalación de nuevo para agregar y habilitar el servicio, de aprendizaje automático, como se describe aquí: [Installing SQL Server R Services en una máquina virtual de Azure](../r/installing-sql-server-r-services-on-an-azure-virtual-machine.md).
+ Crear una base de datos de SQL Azure con un nivel de servicio que puede admitir el aprendizaje automático y usar la nueva característica de R Services actualmente en vista previa. Para obtener más información, consulte [base de datos de SQL Azure](../r/using-r-in-azure-sql-database.md).

> [!NOTE]
> Actualmente, servicios de aprendizaje de máquina de SQL Server no se admite en las máquinas virtuales de Linux para SQL Server 2017. Sin embargo, puede realizar en un modelo entrenado con la función de PREDICCIÓN de T-SQL de puntuación. Para obtener más información, consulte [puntuación nativo de SQl Server](../sql-native-scoring.md). 

### <a name="virtual-machines-for-deep-learning"></a>Máquinas virtuales para aprendizaje profundo 

Anteriormente, Microsoft proporciona el Kit de herramientas de aprendizaje profundo para los Data Science Virtual Machine, que puede agregar a una existente Data Science Virtual Machine. Este kit de herramientas ahora es reemplazado por la máquina Virtual de aprendizaje profundo, que contiene herramientas de aprendizaje profundo populares:

+ Ediciones de GPU de marcos de trabajo de aprendizaje profundo, como Microsoft cognitivos Toolkit, TensorFlow, Keras y Caffe
+ Controladores integrados de GPU
+ Una colección de herramientas para el procesamiento de texto y de imagen
+ Herramientas de desarrollo empresarial como Microsoft R Server Developer Edition, Python Anaconda, Jupyter blocs de notas para Python y R
+ Herramientas de desarrollo para Python, R, SQL Server y mucho más
+ Ejemplos de-to-end para la imagen y la descripción de texto

La máquina Virtual de aprendizaje profundo está disponible en las plataformas de Ubuntu Linux o Windows 2016. Para obtener más información, consulte [marcos AI y aprendizaje profundo](https://docs.microsoft.com/azure/machine-learning/data-science-virtual-machine/dsvm-deep-learning-ai-frameworks).

> [!IMPORTANT]
> 
> La implementación de esta máquina virtual requiere que las imágenes de máquina virtual de Azure GPU NC-series, que están disponibles en las regiones de Azure limitadas. Para obtener información acerca de la disponibilidad, vea [productos disponibles por región](https://azure.microsoft.com/en-us/regions/services/). Al aprovisionar la máquina virtual, asegúrese de usar **HDD** como el tipo de disco, no **SSD**.

## <a name="frequently-asked-questions"></a>Preguntas más frecuentes

Esta sección contiene algunas preguntas comunes sobre máquinas virtuales de Microsoft de aprendizaje automático.

### <a name="can-i-install-a-virtual-machine-with-sql-server-2017"></a>¿Se puede instalar una máquina virtual con SQL Server 2017?

Una máquina de virtual basada en Windows para SQL Server de 2017 Enterprise Edition que incluye servicios de aprendizaje de máquina estará disponible pronto. Busque anuncios en estos sitios de blogs:

+ [Inteligencia de Cortana y aprendizaje automático](https://blogs.technet.microsoft.com/machinelearning/)
+ [Iniciados de la plataforma de datos](https://blogs.technet.microsoft.com/dataplatforminsider/)

### <a name="how-do-i-access-data-in-an-azure-storage-account"></a>¿Cómo se tiene acceso a los datos de una cuenta de almacenamiento de Azure?

Cuando tenga que usar los datos de su cuenta de almacenamiento de Azure, habrá varias opciones para obtener acceso a los datos o moverlos:

+ Copie los datos de la cuenta de almacenamiento al sistema de archivos local con una utilidad, como [AzCopy](https://azure.microsoft.com/documentation/articles/storage-use-azcopy/#copy-files-in-azure-file-storage-with-azcopy-preview-version-only). 

+ Agregue los archivos a un recurso compartido de archivos en la cuenta de almacenamiento y, luego, monte el recurso compartido de archivos como una unidad de red en la máquina virtual.  Para más información, consulte [Montaje de archivos de Azure](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-files/). 

### <a name="how-do-i-use-data-from-azure-data-lake-storage-adls"></a>¿Cómo se usan los datos de una cuenta de Azure Data Lake Storage (ADLS)?

Puede leer datos desde el almacenamiento ADLS con RevoScaleR, si hace referencia a la cuenta de almacenamiento de sistema de archivos de la misma manera que lo haría con un HDFS utilizando webHDFS.  Para obtener más información, consulte este artículo: [usar R para realizar operaciones de sistema de archivos en el almacén de Azure Data Lake](https://blogs.msdn.microsoft.com/microsoftrservertigerteam/2017/03/14/using-r-to-perform-filesystem-operations-on-azure-data-lake-store/).



